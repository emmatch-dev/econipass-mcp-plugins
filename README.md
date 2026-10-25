# EcoNiPass MCP プラグイン

EcoNiPassの排出量分析、EMS、CFP入力、削減対策、法定報告を支援する7スキルと、
29の利用環境向け導入キットを配布します。接続先は **DEV** の
`https://api.dev.app.econipass.com/mcp` です。

公開済みのReleaseは **1.1.0**、このブランチの **1.2.0は公開準備中**です。
1.2.0のサーバー変更は未配備で、ソース登録・配布物の検証を実機受入と分けて記録しています。
利用にはEcoNiPassアカウント、対象事業所の権限、必要なOAuth scopeが必要です。
配布物は業務データや認証情報を含みません。

ライセンスの適用は保留しています。1.2.0候補にはLICENSEを同梱せず、MIT等の利用許諾を
追加していません。以前作成したMITレビュー候補は公開せず、Claude公式掲載はLICENSE条件で停止しています。

## ダウンロード

[GitHub Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)から、
利用環境に合うZIPと、その版の`release.json`を取得してください。
旧版のtag・ZIPは変更せず、新しい版は別のReleaseとして公開します。

| 配布物 | 内容 |
| --- | --- |
| `econipass-plugin.zip` | 7スキルとMCP設定を含む共通プラグイン |
| `<skill>.skill.zip` | 個別スキルと参照文書 |
| `econipass-<platform>.zip` | 各環境の導入手順、設定断片、業務指示書・SDKサンプル |
| `release.json` | 37 ZIPのSHA-256、対象環境、版、対応表とソースhashの束縛 |

29環境の配布形式と条件は[プラットフォーム一覧](plugins/PLATFORMS.md)を参照してください。
指示欄やSDKを使う環境もあり、全製品が同じネイティブプラグイン形式ではありません。

## Codex / Claude Code

公開済みの版と接続先を確認して導入します。

```bash
codex plugin marketplace add emmatch-dev/econipass-mcp-plugins
codex plugin add econipass@econipass-plugins
```

```bash
claude plugin marketplace add emmatch-dev/econipass-mcp-plugins
claude plugin install econipass@econipass-plugins
```

導入後は接続画面で認証し、Codexの`setup`またはClaude Codeの`/econipass:setup`を使います。
既存のマーケットプレイスやEcoNiPass接続がある場合は、版と接続先を確認し、重複登録を避けてください。
他の環境ではZIP内の`README.md`に従い、設定断片を既存設定へマージします。

## 業務スキルと1.2.0の変更

| スキル | 対象 |
| --- | --- |
| `setup` | 接続先・利用事業所・公開ツールの確認 |
| `emissions-analysis` | 排出量、原単位、Scope 3、製品／設備別分析 |
| `activity-input` | エネルギー、Scope 3、入力状況、取込履歴 |
| `ems-operations` | 計測、取込、マスター、料金／目標、監視、共有分析／報告、M&V |
| `cfp-input` | 5種のCFP Excel取得、置換範囲の確認、投入 |
| `measures-targets` | 削減目標、対策、タスク・活動・コメント、独自項目の値 |
| `statutory-reports` | 不足項目、提案、保存帳票、旧XML、本人ブラウザーへの引継ぎ |

1.2.0ではタスク更新、活動の参照・登録・更新・コメント、施策／タスク／活動の独自項目定義の
参照という8ツールを追加しました。定義そのものの作成・変更・削除はブラウザーで行います。
更新では現在状態を確認previewへ束縛し、競合を検出すると再取得を要求します。
EMSではCSV取込トランザクション、保存報告の再生成、サイト有効開始日の繰上げと利用条件を補完しました。
上流のCSV受付集計 `list_ems_import_summaries` と原本出力 `export_ems_import_transactions` も保持します。

CFP取得は既定でファイル情報だけを返し、本人の入力画面で別途取得する手順を案内します。
XLSXを受信できるhost／SDKは明示的にembeddedを選び、実ファイルを確認してから編集・投入します。

ソース登録は通常241、共有法定帳票有効時254、法定レビューも有効な最大構成256、
固定PRD参照タグ構成30ツールです。これらはソースのprofile別登録数で、実環境の公開数ではありません。
[対応表](plugins/econipass/tool-skill-map.json)は14ソースファイルのbyte hashと4profileの登録を束縛します。
接続先の実catalog・権限・scope・機能フラグが、利用できる操作を決めます。

更新はdry-runで具体的な対象と変更を確認し、既存の利用者承認に一致するpayloadと
一回限りの確認tokenで実行します。結果が不明な更新は自動再試行せず、現在状態を読み戻します。
スキルの導入によって権限や新しいOAuth grantが付与されることはありません。

## 配備・受入・公開の状況

実装ソース`6d3fc5d6`、metadata`3775093d`、基点develop`06ee31fb`の統合候補です。
CFPとEMS12操作で、既定metadata／明示embeddedを使い分けます。
サーバー取得・ファイル本体同梱・クライアント受領／保存を分離し、通常返却に本体は含めません。
旧監査0a691の承認・10f反映と旧CIは履歴です。新統合ソースの監査は未承認・未反映、
CIは未push・未実施で、DEV候補も未配備・未公開です。

新候補のMac12環境を一つずつ試験し、11環境で限定成功、Rooでスキルmetadata列挙が未合格でした。
Rooの初期化raceを疑っていますが、原因は確定していません。初回失敗を保存し、再試行していません。
Linux Codexではローカル導入2操作・metadata RPC3件が成功しました。Mac Desktop／IDEは未確認です。
Claude WebではEMSスキルv3を新規導入・3ソースのroundtripを確認し、
他6スキルはZIPのbyte同一性と現在の有効状態を再確認しました。6スキルの再importは行っていません。
ローカル13試行は12限定成功・Roo1未合格です。Claude Webを加えた合計は
**限定成功13／未合格1／未実施15、認証済み総合受入0／29** です。
公開版の部分確認は0／29で、過去のnative13成功は継承しません。

[今回の限定試験記録](docs/candidate-native-load-v1.2.0-merged-ems-license-held-20261026.json)と[候補hash](docs/candidate-package-v1.2.0-merged-ems-license-held-20261026.json)は、
ソース14ファイル・37 ZIP・999エントリへ束縛しています。
Cursor／VS Codeは設定のみ、4 SDKは合成fixture、Claude hostedはWebのスキル導入だけです。
remote MCPの接続成功、新OAuth、実モデル、顧客業務操作は0で、認証済みCFP／EMS取得・保存・投入／置換の受入は含みません。
新OAuth、ChatGPT受入、LICENSE適用の保留は維持します。

[受入・公式掲載状況](docs/ACCEPTANCE.md)、[機械可読記録](docs/acceptance-summary.json)、
[検証記録](plugins/VALIDATION.md)、[公開手順](plugins/PUBLISHING.md)を参照してください。
