# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo does

社内SE転職アフィリエイト向けに、**Instagram の 9:16 縦長 1 枚図解**を量産するためのコンテンツ制作パイプライン。コードは最小限で、**実体は Claude Code の agent / skill 定義と、画像生成の bash スクリプト 1 本**。

## Primary entrypoint

```
/instagram-infographic
```

このスキルが 4 ステップを 1 サイクルで回す:

| Step | 担当 | 出力 |
| ---- | ---- | ---- |
| 1 | `naibu-se-content-ideator` | タイトル候補（JSON） → ユーザー選定 |
| 2 | `internal-se-content-researcher` | `data/research/manual/YYYY-MM-DD_<slug>.md` |
| 3 | `sns-multi-format-creator` | SNS3成果物 + `=== CONTENT_DATA START/END ===` ブロック |
| 4 | `script/generate_instagram_infographic.sh` | `data/images/manual/<...>/infographic_{1024x1536,1088x1920}.png` |

詳細手順・引数・エラー対応は `.claude/skills/instagram-infographic/SKILL.md` にある。

## Architecture: なぜこの構成か

- **agents は工程ごとに完全分離**。各 agent は独立した persistent memory（`.claude/agent-memory/<agent-name>/`）を持ち、ideator は過去タイトルの重複回避、researcher は数値・出典の使い回し、creator はフック・配色の効きどころを蓄積する。**メモリは agent ごとに孤立**しており、横断参照しない設計。
- **Step 3 が CONTENT_DATA フォーマットを強制出力**することで、Step 4 の bash スクリプトに渡す独自フォーマット（`テーマ：/タイトル：/カード：1.見出し｜説明文｜補足ラベル...`）への変換を Claude 側に閉じ込めている。スクリプトは「**入力テキストを画像に書く**」だけに専念する。
- **データの正本はファイルシステム**: `data/research/`, `data/drafts/`, `data/images/` に全出力が残る。memory には実行ログを書かない（git とファイルシステムが authoritative）。

## CONTENT_DATA フォーマット（Step 3→4 の契約）

```
テーマ：（一言で、20字以内）
タイトル：（最大20字）
サブタイトル：（30〜45字）
カード：
1. 見出し｜説明文｜補足ラベル
2. 見出し｜説明文｜補足ラベル
...（4〜8個）
まとめタイトル：（10〜15字）
まとめ文：（30〜50字）
保存促進テキスト：（10〜15字）
```

- 区切りは**全角縦棒「｜」**（半角 `|` ではない）
- 文言はそのまま画像に焼かれるので、誤字なく簡潔に
- スクリプト内 SYSTEM_PROMPT に「CONTENT_DATA の文言だけを使い、新しい日本語を追加しない」厳格ルールあり

## 画像生成スクリプト

```bash
./script/generate_instagram_infographic.sh -f <content.txt> -o <out_dir>
```

オプション:
- `-f <file>`: CONTENT_DATA をファイルから読む（推奨）
- `-o <dir>`: 出力先（既定: `./out`）
- `-m <model>`: OpenAI 画像モデル（既定: `gpt-image-2-2026-04-21`、失敗時は `gpt-image-2` で再試行）
- `-q <quality>`: `low` / `middle` / `high` / `auto`（既定: `middle`）

依存コマンド: `curl`, `jq`, `python3`, `sips`（macOS 標準）。

実行は**プロジェクトルートから**（`./.env` を `source` するため）。スクリプトは API で `1024x1536` を生成 → `sips` で 9:16 (`1088x1920`) に crop+resize して 2 サイズを書き出す。

## Environment

- `.env` （プロジェクトルート、git 管理外）に `OPENAI_API_KEY` が必須
- `OPENAI_IMAGE_MODEL` 等の追加変数は不要（スクリプト引数で指定）

## Data layout

```
data/
├── research/        # researcher の出力 MD（YAMLフロントマター付き）
│   ├── manual/      # 手動 RUN（/instagram-infographic はここに書く）
│   └── <RUN_ID>/    # 旧自動パイプラインの遺産
├── drafts/          # 旧パイプラインの diagrammer 出力（参考用に残置）
└── processed/       # トレンド分析用 JSON（任意・現状未使用）
```

`research/manual/` の既存 MD は **YAMLフロントマターに `title / audience / format / sources` を含む**書式で統一されている。新規 researcher はこの構造に揃えること。

## Agent memory の運用

各 agent の memory は `.claude/agent-memory/<agent-name>/` に独立配置:
- `MEMORY.md` がインデックス（150字×行で簡潔に）
- 各メモリは frontmatter 付き個別ファイル（type: user / feedback / project / reference）
- **数字・出典の事実メモは researcher が積極的に貯める**（`trending_facts_*.md`, `*_facts.md` 等の命名）→ 同種テーマの再リサーチ時に再利用される

agent 詳細仕様は `.claude/agents/*.md` のフロントマター + 本文を参照。書き換えは可能だが、**入出力契約（CONTENT_DATA フォーマット等）を変える場合は SKILL.md も同時更新**すること。

## 単発実行のレシピ

| やりたいこと | コマンド |
| --- | --- |
| 既存 CONTENT_DATA から画像だけ作る | `./script/generate_instagram_infographic.sh -f path/to/content.txt -o out_dir` |
| 既存リサーチMDから SNS3種だけ作る | `sns-multi-format-creator` agent を直接起動し、MD パスを渡す |
| タイトル案だけ量産する | `naibu-se-content-ideator` agent を起動（`N=20` 等で本数指定） |
| 1 トピックを深掘りリサーチ | `internal-se-content-researcher` agent にタイトルとターゲットを渡す |

複数本まとめて作る場合は agent を**並列起動**できる（同時 3〜5 本が目安、それ以上は WebSearch / API レート制限で詰まりやすい）。
