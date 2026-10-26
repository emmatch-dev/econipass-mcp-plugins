# EcoNiPass MCP プラグイン（DEV prerelease）

EcoNiPassの排出量分析、EMS、CFP入力、削減対策、法定報告を支援する7スキルと、29環境向け導入キットです。
接続先は **DEV** の `https://api.dev.app.econipass.com/mcp` です。
配布版・公開状態・取得可能な資産は [GitHub Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases) で確認してください。
公開日時とtagの対象commitはRelease metadataを参照します。

利用にはEcoNiPassアカウント、対象事業所の権限、必要なOAuth scopeが必要です。
配布物に業務データや認証情報は含みません。今回のLICENSE適用、追加OAuth認可、ChatGPT受入は保留中です。
公式ディレクトリの掲載申請は未完了で、MIT等の利用許諾は追加していません。

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

取得する版と接続先を確認して導入します。

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

## クライアント別の設定補完

旧Cascadeでは他MCPを含む100ツール上限に合わせ、既定を組織確認1ツールとし、
業務別13設定から一つ選びます。各設定は1〜64ツールで、全256ツールを横断してカバーします。
`disabledTools` は未知の追加ツールを隠せないため、実catalogの全ページ・名前・件数・hashを照合し、
差分があれば利用を止めて再生成します。Devin Localの専用設定は旧Cascadeと分けます。
Junie専用MCP配置、旧Qを維持したKiro設定と明示scope、Gemini Enterpriseの初期全Actions無効・
最大100の選択、n8n v1.2以降のHTTP Streamable選択も補完しました。
設定補完はそのクライアントでの実機受入を意味しません。[詳細](plugins/PLATFORMS.md)を参照してください。

## 検証・配備・受入

実装source `a113b01cb250c9d57c225e7c487570d99783bc22` は全必須CIとimage build／promoteを通過しました。
[CI](https://github.com/emmatch-dev/econipass-backend/actions/runs/40270099289)と
[image workflow](https://github.com/emmatch-dev/econipass-backend/actions/runs/40270099317)は、DEV配備・業務受入とは別の結果です。
MCP実装84ファイルと配布source14の同一性、更新を含むアプリの新監査を分けて記録します。アプリ監査：fadbfebaで再監査したアプリ2,196ファイル（digest 24487902…）とMCP84ファイル（digest daa9dd60…）の束縛がa113に一致。

1.2.0の37 ZIP＋`release.json`、計38資産を認証済みGETで受領し、size／SHA・全CRC・1,016エントリを確認しました。
`release.json` SHA-256は `83f900b69c53acea93f5dbdee7ddc1d7611acd324f23bae77790b40576e952bc` です。配布状態はReleasesで確認してください。

| 確認項目 | 結果 |
| --- | --- |
| DEV backend／MCP | [成功：a113・attempt1、deploy／verify／finalize](https://github.com/emmatch-dev/econipass-backend/actions/runs/40274300029) |
| Kong | [成功：a113・attempt1、deploy／verify／finalize](https://github.com/emmatch-dev/econipass-backend/actions/runs/40275773734) |
| 公開API／MCP／OAuth／CORS | full API／MCP／OAuth／CORS helperの1回検証が成功。frontendは200・非空HTML（画面操作の受入とは別） |
| 新sourceでの認証済みCFP | 5種類でサーバー取得＋metadata応答成功、500なし。embedded受領・保存・投入／置換は未受入 |
| 新sourceでの認証済みEMS | CSV／XLSXのサーバー取得＋metadata応答成功、500なし。embedded受領・保存・更新は未受入 |

29環境の状況は **限定確認12／Rooの元失敗1／package load前blocked2／他未実施14、総合受入0／29** です。
限定確認には設定読取・合成fixture・スキルだけの確認が含まれます。
RooはMCPを無効にした別の隔離診断で7スキルのmetadataを読めましたが、配布ZIP全体・MCP接続・業務受入には加算していません。
Linux Codexの試験環境準備とQueryPie/Aruのimport前UIはblockedです。

[受入の範囲](docs/ACCEPTANCE.md)と[機械可読の概要](docs/acceptance-summary.json)を確認してください。
[以前の観測記録](https://github.com/emmatch-dev/econipass-mcp-plugins/blob/a72fb24fa8ca97db94091e9452a07d5a69195cbf/README.md)は固定commitの履歴です。
