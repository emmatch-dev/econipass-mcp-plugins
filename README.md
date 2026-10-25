# EcoNiPass MCP プラグイン

EcoNiPassの排出量分析、EMS、CFP入力、削減対策、法定報告を支援する7スキルと、
29の利用環境向け導入キットを配布します。接続先は **DEV** の
`https://api.dev.app.econipass.com/mcp` です。

公開済みのReleaseは **1.1.0**、このブランチの **1.2.0は公開準備中**です。
1.2.0のサーバー変更は未配備で、ソース登録・配布物の検証を実機受入と分けて記録しています。
利用にはEcoNiPassアカウント、対象事業所の権限、必要なOAuth scopeが必要です。
配布物は業務データや認証情報を含みません。

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

ソース登録は通常239、共有法定帳票有効時252、法定レビューも有効な最大構成254、
固定PRD参照タグ構成30ツールです。これらはソースのprofile別登録数で、実環境の公開数ではありません。
[対応表](plugins/econipass/tool-skill-map.json)は14ソースファイルのbyte hashと4profileの登録を束縛します。
接続先の実catalog・権限・scope・機能フラグが、利用できる操作を決めます。

更新はdry-runで具体的な対象と変更を確認し、既存の利用者承認に一致するpayloadと
一回限りの確認tokenで実行します。結果が不明な更新は自動再試行せず、現在状態を読み戻します。
スキルの導入によって権限や新しいOAuth grantが付与されることはありません。

## 配備・受入・公開の状況

2026-10-25には既存ソース`8c578bac`のbackend／Kong配備が成功しました。
これは1.2.0候補の新8ツール・不具合修正を配備した結果ではありません。
Claude Webの既存接続UIでは244ツール（interactive 15・参照119・更新110）を確認しましたが、
raw `tools/list`、正確な稼働SHA、各操作の機能受入とは別の観測です。

**公開版としての1.2.0は部分確認0／総合完了0です。**
未公開のレビュー候補では13製品の限定的な読み込み・metadata・設定・SDK確認を行いました。
6製品を再実行し、7製品はZIP全byte一致を条件に検証済み試験を参照しています。
これは認証済みremote MCPや業務操作の総合受入ではありません。
10月21日の1.1.0に対する部分確認14／総合完了0は[履歴](docs/history/ACCEPTANCE-v1.1.0-20261021.md)へ保存し、
新版の成功件数へ継承していません。新規MCP OAuthとChatGPTの受入は利用者の指示で保留中です。

CFPの以前の500は一時領域の権限修正後、10月21日の認証済み再試験で再発せず、5種類のExcel取得に成功しました。
この結果は当時の`fde1cffb`での取得と基本構造確認であり、1.2.0の再試験・投入・置換・既存データ保持の完了を意味しません。

[受入・公式掲載状況](docs/ACCEPTANCE.md)、[機械可読の受入記録](docs/acceptance-summary.json)、
[配布物の検証](plugins/VALIDATION.md)、[公開手順](plugins/PUBLISHING.md)を参照してください。
GitHub配布とOpenAI／Claude等の公式ディレクトリ審査・掲載は別の手続きです。
