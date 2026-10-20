# EcoNiPass MCP プラグイン

EcoNiPassの排出量分析、EMS、CFP入力、削減対策、法定報告を支援する7スキルと、
29の利用環境向け導入キットを配布します。現在の配布版は **1.1.0**、
接続先は **DEV** の `https://api.dev.app.econipass.com/mcp` です。

利用者のEcoNiPassアカウント、対象事業所の権限、必要なOAuth scopeが必要です。
このリポジトリはクライアント用の配布物を収録し、業務データや認証情報を含みません。

## ダウンロード

[GitHub Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)から、
利用環境に合うZIPと`release.json`を取得してください。

| 配布物 | 内容 |
| --- | --- |
| `econipass-plugin.zip` | 7スキルとMCP設定を含む共通プラグイン |
| `<skill>.skill.zip` | 個別スキルとその参照文書 |
| `econipass-<platform>.zip` | 各環境の導入手順、設定断片、業務指示書 |
| `release.json` | 37 ZIPのSHA-256、対象環境、バージョン |

29環境それぞれの配布形式と条件は[プラットフォーム一覧](plugins/PLATFORMS.md)を参照してください。
すべてが同じネイティブプラグイン形式ではありません。指示欄やSDKを使う環境も含みます。

## Codex

```bash
codex plugin marketplace add emmatch-dev/econipass-mcp-plugins
codex plugin add econipass@econipass-plugins
```

インストール後、Codexの接続画面でEcoNiPassにログインし、`setup`スキルを選びます。
既に`econipass-plugins`マーケットプレイスやEcoNiPass接続を登録している場合は、
既存の接続先と版を確認し、同じ接続を重複登録しないでください。

## Claude Code

```bash
claude plugin marketplace add emmatch-dev/econipass-mcp-plugins
claude plugin install econipass@econipass-plugins
```

インストール後、EcoNiPassへの接続を認証し、`/econipass:setup`から開始します。
他の環境では対応ZIPの`README.md`に従い、設定断片を既存設定へマージしてください。

## 業務スキル

| スキル | 対象 |
| --- | --- |
| `setup` | 接続先・利用事業所・公開ツールの確認 |
| `emissions-analysis` | 排出量、原単位、Scope 3、製品／設備別分析 |
| `activity-input` | エネルギー、Scope 3、入力状況、取込履歴 |
| `ems-operations` | 計測、取込、マスター、料金／目標、監視、共有分析／報告、M&V |
| `cfp-input` | 5種のCFP Excelの取得、置換範囲の確認、投入 |
| `measures-targets` | 削減目標、予測、対策、タスク |
| `statutory-reports` | 報告の不足項目、入力、保存帳票、旧XML経路 |

1.1.0のソース登録では243ツールを7スキルに割り当てています。
実際に使えるツールは接続先の版、公開フラグ、利用者の権限とscopeによって異なります。
DEV配備のreadiness／canaryでは241ツール、診断版の配備後に再取得した
Codex接続メタデータは183ツールでした。
EMSの58ツールが後者に現れていません。現在の認証済み`tools/list`は未観測で、
件数差の原因は未確定です。[観測の区別](docs/ACCEPTANCE.md#ツール公開数の観測)を参照してください。

参照は`mcp:read`、更新は`mcp:write`等の適切なscopeと業務権限を使います。
スキルを導入しても権限は付与されません。更新はdry-runで対象と内容を確認し、
利用者の承認と一致するpayload・一回限りの確認tokenで実行します。
結果が不明な更新を自動再試行せず、既存の状態を読み戻してください。

## 検証と公開範囲

配布形式、ツール対応表、テストの検証結果は[VALIDATION.md](plugins/VALIDATION.md)、
配布経路と公開範囲は[PUBLISHING.md](plugins/PUBLISHING.md)に記録しています。

全29環境でのインストール、OAuth更新・失効、認証済みの参照／更新、添付ファイル受入は
未完了です。APIサンプルは組織一覧を読む接続確認用であり、更新処理のサンプルではありません。
外部プラグインディレクトリへの審査・掲載と、このGitHub配布は別です。

2026-10-21の実機確認では、Codexからの組織一覧・EMSサイト一覧の取得に成功しました。
Codex CLI、Claude Code、GitHub Copilot CLI、Gemini CLIの4クライアントは、
通信を遮断した隔離環境で1.1.0の7スキルとMCP設定を読み込めました。
API向け4キットは、架空の試験データでSDKオブジェクトの構築やリクエスト生成など、
各サンプルに応じたオフライン検証を行いました。このSDK検証では、実際のモデルAPIや
EcoNiPassへの接続は行っていません。CursorはMCP設定の
CLI読み込みのみ確認し、プラグイン・スキルの実行時読み込みは未確認です。
goose 1.55.0では、通信を遮断して7スキルの認識とMCP設定の読み戻しを確認しました。
これはプラグインの識別・版確認や認証済み接続とは別の検証です。
これらを認証済みの総合受入には数えず、**完了は0/29環境**です。

配布物1.1.0のbackendソースは`37284f6`のまま、DEV稼働版は診断用の`94ae94f`へ更新しました。
CFP入力Excelは旧稼働版`37284f6`で5種類ともHTTP 500を確認し、Webのマスタ取得も失敗しました。
診断版ではmasterのみHTTP 500を再確認し、他4種類は未再試験です。実行時の修正は未適用で、
CFPのファイル取得・投入の受入は未完了です。
現在の結果と公式掲載状況は[受入・公開状況](docs/ACCEPTANCE.md)に記録します。
