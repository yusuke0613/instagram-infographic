---
title: 社内SE志望者の必須スキル 2026年版マップ — 「2020年の表」はもう半分使えない
audience: 社内SE志望（20代後半〜30代、SIer/SES在籍 or 第二新卒）
format: 1枚図解（縦長グリッド：6カテゴリ×規模差×優先度）
researched_at: 2026-05-09
sources:
  - { name: IPA「DX動向2025」, url: "https://www.ipa.go.jp/digital/chousa/dx-trend/dx-trend-2025.html", accessed: "2026-05-09" }
  - { name: IPA「DX動向2025-AI時代のデジタル人材育成」, url: "https://www.ipa.go.jp/digital/chousa/discussion-paper/dx2025_digital_talent_ai_era.html", accessed: "2026-05-09" }
  - { name: ITmedia 久松剛「DX動向2025の裏側 便利屋化問題」, url: "https://www.itmedia.co.jp/enterprise/articles/2512/10/news013.html", accessed: "2026-05-09" }
  - { name: レバテックキャリア 社内SE求人ページ, url: "https://career.levtech.jp/engineer/offer/occ-16/", accessed: "2026-05-09" }
  - { name: レバテック「IT人材白書2026」, url: "https://levtech.jp/files/doc/levtech_research_2026.pdf", accessed: "2026-05-09" }
  - { name: Sky株式会社 クラウドエンジニア(情報システム部)求人, url: "https://www.sky-career.jp/jobs/se08.html", accessed: "2026-05-09" }
  - { name: Sky株式会社 セキュリティエンジニア(情報システム部)求人, url: "https://www.sky-career.jp/jobs/se03.html", accessed: "2026-05-09" }
  - { name: パイオニア株式会社 社内SE(M365管理)求人, url: "https://hrmos.co/pages/pioneer01/jobs/0050005", accessed: "2026-05-09" }
  - { name: クラウドキャリア ゼロトラスト人材需要, url: "https://cloud-career.jp/articles/market-03/", accessed: "2026-05-09" }
  - { name: gxo ゼロトラスト中小実装ガイド2026, url: "https://www.gxo.co.jp/column/zero-trust-security-implementation-guide-sme-2026", accessed: "2026-05-09" }
  - { name: doda 社内SE転職トレンド, url: "https://doda.jp/engineer/guide/inhousese/trend.html", accessed: "2026-05-09" }
  - { name: レバテック 社内SE後悔6理由, url: "https://career.levtech.jp/guide/knowhow/article/91021/", accessed: "2026-05-09" }
  - { name: レバテック 社内SEに必要なスキル一覧, url: "https://career.levtech.jp/guide/knowhow/article/130/", accessed: "2026-05-09" }
  - { name: パーソルクロステクノロジー 社内SEおすすめ資格13選, url: "https://staff.persol-xtech.co.jp/corporate/security/article.html?id=204", accessed: "2026-05-09" }
  - { name: R35 社内SEスキル大全ロードマップ, url: "https://r35-se.com/archives/822", accessed: "2026-05-09" }
  - { name: NRI ユーザー企業のIT活用実態調査2025(生成AI57.7%), url: "https://www.nri.com/jp/news/newsrelease/20250218_1.html", accessed: "2026-05-09" }
  - { name: JUAS 企業IT動向調査2025, url: "https://juas.or.jp/library/research_rpt/it_trend/", accessed: "2026-05-09" }
  - { name: 総務省 令和5年版情報通信白書(クラウド利用72.2%), url: "https://www.soumu.go.jp/johotsusintokei/whitepaper/", accessed: "2026-05-09" }
  - { name: AWS認定資格ガイド2025, url: "https://cloudassist.jp/knowledge/aws-intro/qualification/", accessed: "2026-05-09" }
  - { name: PMP転職評価(JAC), url: "https://www.jac-recruitment.jp/market/consulting/project-management-professional/", accessed: "2026-05-09" }
---

# 社内SE志望者の必須スキル 2026年版マップ — 6カテゴリで「自分の陳腐化度」を測る

## 結論（一言で）
2020年の必須表は半分死んだ。今は「クラウド×SaaS統合×AI×ゼロトラスト」が共通言語。

## なぜ今これを知るべきか（why_now）
クラウド利用企業は72.2%(総務省2024)、生成AI導入57.7%/「スキル不足」70.3%(NRI 2025)、DX人材「大幅/やや不足」85.1%(IPA DX動向2025)。需要は5年で激変したのに、SIer/SESで磨いたスキルが社内SEの土俵で評価されないケースが続出。**2020年の「Java+Oracle+ネットワーク」中心スキル表は、半分が陳腐化済み**。今アップデートしないと面接で「で、AWSは？SaaS統合は？」で詰む。

## 図解構成（推奨レイアウト）
- レイアウト案: **縦長グリッド型**。上段に「2020→2026のシフト」帯、中段に「6カテゴリ×3規模(大手/中堅/中小)」のスキルマップ、下段に「優先順位TOP5+資格対応」。図解1枚で「自分のスキル棚卸し」と「次に学ぶ順番」が両方見える設計
- 視線誘導: 上(変化の概観) → 中(自分の現在地マッピング) → 下(行動計画)
- カラー配色案: 「消えた/減った」スキル=グレー、「増えた」スキル=オレンジ、「変わらない基礎」=ブルー。優先度TOP5は赤帯で強調
- アイコン: クラウド、SaaS、AI、シールド(セキュリティ)、歯車(自動化)、人(マネジメント)の6アイコンでカテゴリを視覚化

## ブロック設計（図解の各パーツ）

### Block 0: 上段帯「2020→2026 必須スキルのシフト」
- ポイント: 5年でスキル要件は半分入れ替わった
- 詳細:
  - **減った/消えた**: オンプレADサーバ運用／物理サーバ調達・キッティング／単体業務システムの保守ベタ／Excelマクロ職人芸／VPN前提の境界型セキュリティ
  - **変わらない基礎**: ネットワーク/TCP-IP/Linux/SQL/プロジェクト推進力/ベンダーコントロール
  - **新しく必須化**: クラウド(AWS/Azure/GCP)／SaaS統合(Salesforce/Workday/M365)／生成AI活用(Copilot/RAG)／ゼロトラスト(Entra ID/Intune/MFA)／IaC(Terraform)／ローコード(Power Platform)
- 出典: 総務省情報通信白書2024、レバテックキャリア社内SE求人、Sky株式会社求人

### Block 1: クラウド基盤スキル（最優先カテゴリ）
- ポイント: 「AWS or Azure 1年以上」が大手・中堅の事実上の足切り
- 詳細:
  - **大手**: AWS/Azure/GCPいずれかでLambda/RDS/CloudWatch等の運用経験、IaC(Terraform/CloudFormation)、マルチアカウント設計
  - **中堅**: AWSまたはAzureの構築or運用1年以上(Sky株式会社の必須要件原文)、Linuxサーバ運用、スクリプト自動化
  - **中小**: Azure(M365とセット)中心、SaaS連携の理解、必ずしも構築までは不要
  - 推奨資格: **AWS SAA(ソリューションアーキテクト アソシエイト)** or **Azure AZ-104**(コスパ最良ライン)
- 出典: Sky株式会社求人、レバテック社内SE求人、AWS認定資格ガイド2025

### Block 2: SaaS統合・業務システムスキル
- ポイント: 「作る」より「つなぐ・選ぶ」が主戦場
- 詳細:
  - **大手**: SAP S/4HANA(ECC→S/4移行は2027年問題)、Salesforce(Apex/Lightning)、Workday、ServiceNow、API連携設計
  - **中堅**: Microsoft 365(Exchange Online/SharePoint)、kintone、Salesforce基礎、SaaS間連携(iPaaS)
  - **中小**: M365全般管理、freee/マネーフォワード、Slack運用、SaaSライセンス管理
  - 1,000名以上の大企業は**平均207サービス利用、19%は500超**(参考)→「SaaS統合力」が中核業務化
- 出典: レバテック社内SE求人、SAP導入求人(リクルートエージェント等)、パイオニア社内SE求人

### Block 3: セキュリティ・ゼロトラストスキル
- ポイント: 境界型→ゼロトラストへ。MFA・Entra ID・Intuneが基本語彙
- 詳細:
  - **大手**: ゼロトラスト設計、ISMS/Pマーク、特権ID管理(PAM)、SOC連携、CASB/SASE
  - **中堅**: Entra ID(旧Azure AD)、Intune、MFA、EDR、SAML/OIDC認証基盤
  - **中小**: MFA(月500円/人〜)、EDR、SaaSの権限管理、フィッシング対策
  - **求人倍率**: セキュリティ人材42.6倍(レバテック2025年12月・全職種で最も希少)
  - 推奨資格: **情報処理安全確保支援士**、**CISSP**(管理職目指すなら)、ベンダー資格より国家資格優位
- 出典: クラウドキャリア、gxoゼロトラスト2026ガイド、Sky株式会社セキュリティエンジニア求人

### Block 4: 生成AI・データ活用スキル（2026新カテゴリ）
- ポイント: 「使える」「設計できる」「ガバナンスできる」の3層
- 詳細:
  - **使える層(全規模で最低限)**: Copilot for M365、ChatGPT Enterprise、プロンプト設計
  - **設計できる層(中堅以上)**: RAG構築(Azure AI Search/Bedrock)、社内ナレッジ連携、Power Platform×AI
  - **ガバナンスできる層(大手)**: AI利用ポリシー策定、PII漏洩防止、モデル評価、データレイク(Snowflake/BigQuery)
  - **背景データ**: NRI生成AI導入57.7%、課題「スキル不足」70.3%(2025)。「使うだけ」ではすぐ陳腐化
  - 学び方: Microsoft Learn(無料)→Copilot Studio→AZ-900/AI-900で土台
- 出典: NRI調査2025、レバテック社内SE求人、Microsoft Learn

### Block 5: 自動化・ローコードスキル
- ポイント: 「市民開発の旗振り」が中堅以下の必須要件化
- 詳細:
  - **共通**: Power Platform(PowerApps/Power Automate)、UiPath、GAS、Python基礎
  - **中堅特有**: 業務部門の市民開発支援、ガバナンス設計、内製化推進
  - **中小特有**: ノーコードSaaS(Notion/Airtable/Zapier)中心
  - 求人原文例:「ローコード(Power Platform)/RPA(UiPath)など市民開発ツールを用いてアプリ・フローを設計・開発したご経験」が必須化(マイナビ転職、レバテック)
- 出典: マイナビ転職社内SE求人、レバテック2026求人傾向

### Block 6: ヒューマン・マネジメントスキル（AI時代に重要度UP）
- ポイント: AIで陳腐化したのは「実務」、価値が上がったのは「調整・意思決定」
- 詳細:
  - **共通必須**: 業務部門ヒアリング、要件整理、プロジェクト推進、ベンダーコントロール
  - **大手特有**: 経営層へのIT企画提案、複数ベンダー横断のガバナンス、英語(海外拠点連携)
  - **AI時代の変化**: レバテック調査で「重要度低下スキルTOP3」=資料作成29.7%/予算管理21.8%/データ抽出20.8%。逆に「上流意思決定・社内外調整」の重要度が上昇
  - 推奨資格: **PMP**(大手で評価高)、**IPA プロジェクトマネージャ**(国内コスパ最良)
- 出典: レバテックIT人材白書2026、JAC PMP転職評価、パーソルクロステクノロジー資格13選

### Block 7: 学ぶ優先順位TOP5（最下段の行動指針）
- ポイント: 全部やる必要はない。コスパ順に5つだけ
- 詳細:
  1. **AWS SAA or Azure AZ-104**(クラウド土台・1-3ヶ月・全規模で評価)
  2. **Microsoft 365 + Entra ID + Intune**(SaaS統合とゼロトラストの入口・中堅以下の必須言語)
  3. **Copilot/RAG実装経験**(社内PoCを1つ自分で回す・職務経歴書に書ける唯一のAIネタ)
  4. **Power Platform**(市民開発の旗振り役で社内ポジション確立・転職時の差別化)
  5. **情報処理安全確保支援士 or PMP**(管理職トラックの足切り資格・30代後半までに)
- 出典: レバテック社内SE求人、AWS認定資格ガイド、JAC PMP評価、パーソル社内SE資格13選

## キーメッセージ（図解の周辺テキスト用）
- 2020年の必須表は半分死んだ
- クラウド+SaaS+AIが共通言語
- 「作る」より「選ぶ・つなぐ」
- 便利屋化は防御スキルで回避
- 全部やるな、TOP5から始めろ

## 落とし穴・注意点
- **「資格を取れば転職できる」は誤り**: 実務経験1年が圧倒的に強い。資格は「同条件の応募者の中で勝つ」材料。Sky株式会社のようにAWS/Azure実務1年以上を必須に明記する求人が標準化
- **「便利屋化」リスク**: スキルが揃ってもポジションが「ヘルプデスク兼資料作成兼DX」になる企業は多数(ITmedia久松氏指摘)。**面接で必ず「DX人材の評価制度はあるか」「専任配置か兼任か」を確認**
- **規模別の罠**: 中小=ひとり情シスで全部できる人材を求める→広く浅くで疲弊。大手=分業細かすぎて経験積めない→専門特化。**自分のキャリア軸との相性確認が必須**
- **AI関連スキルの賞味期限**: ツール自体は1年で陳腐化。学ぶべきは「ツール名」ではなく「業務にAIをどう組み込むかの設計力」
- **データ前提**: NRI/IPA/レバテック等の調査は調査対象や定義が異なる(母集団・規模・回答方法)。本図解は「複数ソースで方向性が一致する事実」のみ採用

## 次のアクション（CTA候補）
- 自分の現スキルを6カテゴリで○△×評価→「△」が一番多いカテゴリから着手
- まず無料で: Microsoft Learn(M365/Azure/AI)+ AWS Skill Builder で土台習得
- 1ヶ月以内に **AWS SAA or AZ-104** の試験日を予約(締切ドリブンで学習)
- 副業/個人プロジェクトで **Copilot+RAG社内PoC**を1個作り、職務経歴書に書ける材料を準備
- 求人を週5件チェック→「必須/歓迎」欄に頻出する単語を自分のスキルとマッピング

## 研究メモ（図解には載せないが diagrammer/reviewer が参考にする情報）

### 一次データ補強
- IPA「DX動向2025」: DX人材「大幅/やや不足」85.1%(日本) vs 米23.8%/独44.6%。日本のスキルギャップは突出
- NRI「ユーザー企業のIT活用実態調査2025」: 生成AI導入57.7%、課題1位「スキル不足」70.3%
- JUAS「企業IT動向調査2025」: 言語系生成AI導入41.2%(前年+14.3pt)
- 総務省「令和5年版 情報通信白書」: クラウド利用企業72.2%
- レバテック「IT人材白書2026」: AIで重要度低下スキル1位「資料作成」29.7%、2位「予算管理」21.8%、3位「データ抽出・分析」20.8%
- セキュリティ求人倍率42.6倍(レバテック2025年12月、3年で求人2.5倍)
- 1,000名以上大企業のSaaS利用平均207サービス、19%は500超(SaaS統合力の必要性)

### 求人票実例(具体的な必須要件・原文ベース)
- **Sky株式会社(中堅IT)**: AWSまたはAzureの構築or運用1年以上 / Linuxサーバ経験 / IaC自動化経験
- **パイオニア(大手メーカー)**: M365管理、Exchange Online、Entra ID統合認証基盤管理
- **レバテック社内SE求人ページ頻出技術**: AWS(Lambda/RDS/CloudWatch)、Azure、GCP、Salesforce(Apex/Lightning)、Workday、Slack、kintone、Entra ID、Intune、Jamf、Cisco Meraki、Terraform、Ansible、GitHub、Python、Go

### 規模別の差(まとめ)
- **大手(従業員1,000人〜)**: 専門分業。「○○基盤担当」のように特化スキルを深く。SAP/Salesforce/Workdayなど業務系SaaSの上流設計、グローバル/多拠点ガバナンス
- **中堅(300-1,000人)**: 「クラウド+M365+セキュリティ+AI企画」を兼任できるT字型人材が刺さる。Sky/パイオニアレベルの求人がここ
- **中小(300人未満)**: ひとり情シス比率高(50-500名で32%、100名未満は約4割)。広く浅く、ベンダー管理力とSaaS活用力が中核

### 「便利屋化」防御の論点
- 久松剛(ITmedia 2025/12/10)指摘: DX人材が「ヘルプデスク+資料作成+雑務」に流れる構造的問題
- 主因: 30年前のままの人事制度、評価制度の不備、「お手並み拝見」現象
- 防御策(個人サイド):
  1. 入社前に「DX人材の評価制度・KPIは?」を必ず質問
  2. 専任配置か兼任か、業務範囲の明文化を契約時に確認
  3. ヘルプデスク比率が職務時間の50%超なら警戒
  4. 経営層への定期報告ラインがあるか確認

### 差別化メモ(既存4本との切り分け)
- 本案の独自性: 「個人が今日から学ぶ具体的なツール名・資格名」に絞り込み。既存③(生成AI市場動向)は「業界の数値」中心、本案は「学習者の行動指針」中心
- 6カテゴリ分類は他になし(クラウド/SaaS/セキュリティ/AI/自動化/マネジメントの構造化)
- 規模別×ロール別の差を1枚で見せるのは独自フレーム
- 優先順位TOP5を明示することで「で、何から始めれば？」に直接回答

### 未検証/限界
- 各規模の「必須スキル」は求人サンプルから抽出した傾向値。すべての企業に当てはまるわけではない
- 「2020年の必須表は半分死んだ」は定量的根拠なくレトリック。求人票比較で大筋は支持されるが厳密な定量比較は困難
- AWS SAA/AZ-104がコスパ最良という評価は複数キャリア記事の合意ベース。個人の状況により変動
- ロール別(インフラ/業務/セキュリティ/DX企画)の細分化は今回は規模別を優先。ロール別深掘りは別図解で扱うべき
