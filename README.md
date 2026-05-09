# sns-infographic

社内SE転職アフィリエイト向けに、Instagram の 9:16 縦長 1枚図解を作成するためのコンテンツ制作パイプラインです。

タイトル案の作成、深掘りリサーチ、SNS投稿文への展開、画像生成までを Cursor/Claude の agent と bash スクリプトでつなぎます。

## できること

- 社内SE・情シス・IT転職向けの図解テーマを発案する
- 一次情報や転職市場データを調べて、図解用のリサーチMDを作る
- Instagram図解MD、Reelsキャプション、Threads投稿文に展開する
- `CONTENT_DATA` から Instagram向け PNG を生成する

## 全体フロー

| Step | 担当 | 出力 |
| --- | --- | --- |
| 1 | `naibu-se-content-ideator` | タイトル候補 |
| 2 | `internal-se-content-researcher` | `data/research/manual/YYYY-MM-DD_<slug>.md` |
| 3 | `sns-multi-format-creator` | SNS3成果物 + `CONTENT_DATA` |
| 4 | `script/generate_instagram_infographic.sh` | `infographic_1024x1536.png` / `infographic_1088x1920.png` |

標準の入口は Cursor/Claude skill の `/instagram-infographic` です。

```text
/instagram-infographic
```

タイトルを指定して開始する場合:

```text
/instagram-infographic title: 社内SE 職務経歴書で落ちる7項目
```

ジャンルや候補数を指定する場合:

```text
/instagram-infographic genre=年収・待遇 N=5
```

## セットアップ

プロジェクトルートに `.env` を作成し、OpenAI APIキーを設定します。

```bash
OPENAI_API_KEY=your_api_key_here
```

画像生成スクリプトは以下のコマンドを使います。

- `curl`
- `jq`
- `python3`
- `sips`（macOS標準）

## CONTENT_DATA フォーマット

画像生成スクリプトに渡すテキスト形式です。区切りには半角 `|` ではなく、全角の `｜` を使います。

```text
テーマ：（一言で、20字以内）
タイトル：（最大20字）
サブタイトル：（30〜45字）
カード：
1. 見出し｜説明文｜補足ラベル
2. 見出し｜説明文｜補足ラベル
3. 見出し｜説明文｜補足ラベル
4. 見出し｜説明文｜補足ラベル
まとめタイトル：（10〜15字）
まとめ文：（30〜50字）
保存促進テキスト：（10〜15字）
```

この文言がそのまま画像に載るため、短く・誤字なく・スマホで読める文字量にします。

## 画像だけ生成する

既存の `CONTENT_DATA` から画像だけ作る場合は、プロジェクトルートで実行します。

```bash
./script/generate_instagram_infographic.sh \
  -f "data/images/manual/YYYY-MM-DD_<slug>/content.txt" \
  -o "data/images/manual/YYYY-MM-DD_<slug>"
```

主なオプション:

| オプション | 内容 |
| --- | --- |
| `-f <file>` | `CONTENT_DATA` をファイルから読む |
| `-o <dir>` | 出力先ディレクトリ |
| `-m <model>` | OpenAI 画像モデル |
| `-q <quality>` | `low` / `middle` / `high` / `auto` |

出力先にはタイムスタンプ付きディレクトリが作られます。

```text
data/images/manual/YYYY-MM-DD_<slug>/<YYYYMMDD_HHMMSS>/
├── infographic_1024x1536.png
└── infographic_1088x1920.png
```

## ディレクトリ構成

```text
.
├── .claude/
│   ├── agents/                 # 各工程の agent 定義
│   ├── agent-memory/           # agent ごとの永続メモリ
│   └── skills/
│       └── instagram-infographic/
├── data/
│   ├── research/               # リサーチ成果物
│   ├── drafts/                 # SNS展開・図解草案
│   └── images/                 # CONTENT_DATA と生成画像
└── script/
    └── generate_instagram_infographic.sh
```

## 単発実行レシピ

| やりたいこと | 方法 |
| --- | --- |
| 最初から1枚作る | `/instagram-infographic` を実行 |
| タイトル指定で作る | `/instagram-infographic title: <タイトル>` |
| 既存リサーチMDからSNS3種を作る | `sns-multi-format-creator` にMDパスを渡す |
| 既存CONTENT_DATAから画像だけ作る | `generate_instagram_infographic.sh -f <content.txt> -o <out_dir>` |

## 注意点

- `.env` や `.mcp.json` は認証情報を含む可能性があるため git 管理しません。
- `data/research/manual/` のリサーチMDは、YAMLフロントマターに `title` / `audience` / `format` / `sources` を含める形式で揃えます。
- agent memory は工程ごとに分離されています。実行ログは memory ではなく `data/` 配下の成果物を正本として扱います。
