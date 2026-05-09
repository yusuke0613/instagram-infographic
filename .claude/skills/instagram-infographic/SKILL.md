---
name: instagram-infographic
description: 社内SE転職向けInstagram図解（9:16）を1コマンドで作成するパイプライン。タイトル発案→深掘りリサーチ→SNS整形→画像生成までを4ステップで実行する。
---

# Instagram Infographic Pipeline

社内SE転職アフィリエイト向けの「1枚図解（9:16, Instagramフィード）」を1コマンドで完成させるスキル。

## パイプライン全体像

| Step | 担当 | 入力 | 出力 |
|------|------|------|------|
| 1 | `naibu-se-content-ideator` | ジャンル | タイトル候補3本（JSON） |
| — | ユーザー選定 | 候補3本 | 採用タイトル1本 |
| 2 | `internal-se-content-researcher` | 採用タイトル | リサーチMD |
| 3 | `sns-multi-format-creator` | リサーチMD | SNS3成果物 + CONTENT_DATA |
| 4 | `script/generate_instagram_infographic.sh` | CONTENT_DATA | 9:16 PNG (1024x1536, 1088x1920) |

## 引数の解釈

ユーザーが `/instagram-infographic <args>` と入力した場合:

- **引数なし**: 「どのジャンルで作る？」をAskUserQuestionで聞き、Step 1から実行
- **「タイトル: 〜」 or 「title: 〜」を含む**: Step 1をスキップ、そのタイトルで Step 2 に直行
- **「N=<数>」を含む**: 候補生成本数を上書き（デフォルト3本）
- **「genre=<ジャンル>」を含む**: ジャンル質問をスキップ

---

## Step 1: タイトル発案（`naibu-se-content-ideator`）

### 1-1. ジャンル確認

引数で `genre=` 指定がなければ、AskUserQuestion で以下から選んでもらう（複数選択可）:

- 年収・待遇
- スキル・キャリアパス
- 転職プロセス・選び方
- 業務・組織のリアル
- トレンド/未来予測（生成AI・規制）
- お任せ（混合）

### 1-2. ideator 起動

Agent ツールで `subagent_type: naibu-se-content-ideator` を起動。プロンプトに以下を含める:

- 選択ジャンル
- 「**3本**生成してください」（または引数のN）
- 「過去案と重複しないこと（メモリを参照）」
- 「JSON配列で出力」
- 「各案にtitle/hook/category/target/save_reason/affiliate_angle/trend_tieを含める」

### 1-3. ユーザー選定

ideator の出力JSONをパースし、AskUserQuestion で**1本選定**してもらう。

選択肢には title をラベル、hook を description に表示。

---

## Step 2: 深掘りリサーチ（`internal-se-content-researcher`）

### 2-1. スラグ生成

採用タイトルから英数小文字+ハイフンの slug を作る（30字以内）。例:
- 「社内SE 年収レンジ早見表 7階層」 → `shanai-se-salary-range-7tiers`

### 2-2. researcher 起動

Agent ツールで `subagent_type: internal-se-content-researcher` を起動。プロンプトに以下を含める:

- 採用タイトル
- ターゲット読者（20代後半〜30代、SIer/SES在籍 or 第二新卒、社内SE志望）
- ideator で出した hook / save_reason / category も渡す
- **出力先**: `data/research/manual/YYYY-MM-DD_<slug>.md`
- 既存研究MD（`data/research/manual/`配下）と重複しないよう差別化
- 一次情報優先、数字には出典URL必須

### 2-3. 出力確認

Bash で `ls data/research/manual/<日付>_<slug>.md` を確認。ファイルが無ければ researcher を SendMessage で継続させて再出力依頼。

---

## Step 3: SNS用整形（`sns-multi-format-creator`）

### 3-1. creator 起動

Agent ツールで `subagent_type: sns-multi-format-creator` を起動。プロンプトに以下を含める:

- リサーチMDの絶対パス
- 通常の3成果物（Instagram図解MD / Reelsキャプション / Threads投稿）に**加えて**、以下のCONTENT_DATAフォーマットを **Deliverable 4** として必ず出力すること:

```text
=== CONTENT_DATA START ===
テーマ：（一言で、20字以内）
タイトル：（最大20字、強いフック）
サブタイトル：（30〜45字、補足説明）
カード：
1. 見出し｜説明文｜補足ラベル
2. 見出し｜説明文｜補足ラベル
3. 見出し｜説明文｜補足ラベル
4. 見出し｜説明文｜補足ラベル
（カードは4〜8個、内容に応じて選定）
まとめタイトル：（10〜15字）
まとめ文：（30〜50字、行動喚起）
保存促進テキスト：（10〜15字、「保存して見返そう」等）
=== CONTENT_DATA END ===
```

**ルール**:
- 区切りは全角縦棒「｜」を使用
- 各セルは画像で読める短文（見出し10字以内、説明文25字以内、補足ラベル8字以内）
- カード数は研究MDの構造から最適なパターン（チェックリスト/比較/ランキング/STEPロードマップ等）を選択
- CONTENT_DATA内の文言は画像に**そのまま**載るので、誤字なく簡潔に

### 3-2. CONTENT_DATA 抽出

creator のレスポンスから `=== CONTENT_DATA START ===` と `=== CONTENT_DATA END ===` の間のテキストを抽出。

抽出に失敗したら creator を SendMessage で継続させて再出力依頼。

### 3-3. CONTENT_DATA 保存

抽出した CONTENT_DATA を Write ツールで以下に保存:

`data/images/manual/YYYY-MM-DD_<slug>/content.txt`

---

## Step 4: 画像生成（`generate_instagram_infographic.sh`）

### 4-1. スクリプト実行

Bash ツールで以下を実行:

```bash
cd "/Users/satouyuusuke/Library/Mobile Documents/com~apple~CloudDocs/cc/it-news-collector" && \
./script/generate_instagram_infographic.sh \
  -f "data/images/manual/YYYY-MM-DD_<slug>/content.txt" \
  -o "data/images/manual/YYYY-MM-DD_<slug>"
```

**注意**:
- スクリプトは `cd` 先の `./.env` を読むので、必ずプロジェクトルートで実行
- timeout は 300000ms (5分) を指定。画像生成は数十秒かかる
- `-q` オプションで quality を指定可能（low / middle / high / auto）。デフォルトは middle。高品質にしたい場合は `-q high` を追加

### 4-2. 出力確認

スクリプトが成功すると `data/images/manual/YYYY-MM-DD_<slug>/<TIMESTAMP>/` 配下に以下が生成される:

- `infographic_1024x1536.png` （API直出力、2:3比）
- `infographic_1088x1920.png` （9:16にcrop+resize）

両方のパスをユーザーに報告し、`Read` ツールで `infographic_1088x1920.png` をプレビュー表示する。

---

## Step 5: 完了レポート

ユーザーへの最終報告には以下を含める:

1. **採用タイトル**
2. **リサーチMDパス**
3. **SNS3成果物**:
   - Instagram図解MD（コードブロックで全文）
   - Reelsキャプション（全文）
   - Threads投稿（全文）
4. **生成画像のパス**（2サイズ）
5. **画像プレビュー**（Read ツールで表示）

報告はマークダウンの見出しと表で構造化。長文だが必要な情報は全て本文に含めること（後でコピペで使うため）。

---

## エラーハンドリング

| 状況 | 対応 |
|------|------|
| ideator が JSON で返さない | レスポンスをそのままユーザーに見せ、手動で1本選んでもらう |
| researcher が出力ファイルを作らない | SendMessage で「指定パスに保存して」と再依頼 |
| creator が CONTENT_DATA フォーマットを出さない | SendMessage で「Deliverable 4 (CONTENT_DATA) のみ追加出力して」と依頼 |
| スクリプトが OPENAI_API_KEY エラー | `.env` の有無を確認、無ければユーザーに設定を促す |
| スクリプトが `gpt-image-2-2026-04-21` モデルで失敗 | `-m gpt-image-2` で再試行 |
| sips/jq/curl がない | macOSでは標準のはず。エラー時はユーザーに homebrew で導入を促す |

---

## バリエーション運用

- **同じトピックで複数バリエーション**: Step 3 を **並列で複数起動**（角度違い）→ Step 4 を順次実行
- **既存リサーチMDから画像だけ作りたい**: Step 1-2 をスキップし、Step 3 から開始
- **既存CONTENT_DATAから画像だけ作りたい**: Step 1-3 をスキップし、Step 4 のみ実行

---

## 進捗トラッキング

実行中は TaskCreate で各 Step を追跡し、Step 開始時に `in_progress`、完了時に `completed` に更新する。これにより並列実行や中断再開が容易になる。

## 実行結果の永続化

このパイプラインで生成した成果物は全て `data/` 配下に残るため、メモリには**書かない**（パイプライン実行ログは git/ファイルシステムが正本）。

ただし、ユーザーから「このフックは効いた」「この配色が良かった」等の**フィードバック**があれば、各エージェントのメモリに保存して次回以降に活かす。
