# EcoNiPass MCP プラグイン

この文書は **日付検証修正候補の配備・公開前の観測時点（2026-10-26T00:38:56.122704+00:00）の記録** です。旧f831のDraftと新83f9候補を区別します。後続の現行状況は[PR #5](https://github.com/emmatch-dev/econipass-mcp-plugins/pull/5)と[Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)で確認してください。

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

## クライアント別の設定補完

旧Cascadeでは他MCPを含む100ツール上限に合わせ、既定を組織確認1ツールとし、
業務別13設定から一つ選びます。各設定は1〜64ツールで、全256ツールを横断してカバーします。
`disabledTools` は未知の追加ツールを隠せないため、実catalogの全ページ・名前・件数・hashを照合し、
差分があれば利用を止めて再生成します。Devin Localの専用設定は旧Cascadeと分けます。
Junie専用MCP配置、旧Qを維持したKiro設定と明示scope、Gemini Enterpriseの初期全Actions無効・
最大100の選択、n8n v1.2以降のHTTP Streamable選択も補完しました。
設定補完はそのクライアントでの実機受入を意味しません。[詳細](plugins/PLATFORMS.md)を参照してください。

## 配備・受入・公開の状況

タスク・活動・独自項目の日付について、Pythonが受け付ける`20261026`やISO週日付を
native APIへ送る前に拒否するよう修正しました。確認トークンを発行してから422になる不一致を防ぎます。
修正を含む確認対象commitは`6f09904ba5eedc0805b3895341b032f0770f807b`（日付実装e79417e3）、release SHAは`83f900b69c53acea93f5dbdee7ddc1d7611acd324f23bae77790b40576e952bc`、対応表SHAは`224f3ae9b21e1f3ea594b85d2d0e7cc161d593d36dd75ed6679e5aa6f7381065`です。
既存日付・確認境界471テスト、配布65テストはいずれもskip0で成功しました。
監査95cは`1169e186`、日付修正後の94378は利用者の明示承認を受け`6f09904b`へ反映済みです。
別作業の実行中CI・配備が終わるのを待っており、新候補のCI・image build・DEV配備・一般公開は未実施です。

37 ZIP・1,016エントリを生成し、全CRC・安全パス・LICENSE/PDF混入0を確認しました。
旧f831比10 ZIPの各1エントリが変わり、他27 ZIPは同一です。変更は対応表9コピーと
Windsurfの対応表hash1件だけで、ソース14件中の差は日付helper1件、業務スキルと認証設定は不変です。
現在の公開原本と固定generatorから全37 ZIP・1,016entryを再生成し、全hash・CRC・entry bytesが新候補と一致しました。公開commit／pushの成功とは区別します。

旧13nativeのうち8限定成功とRoo1失敗は実入力の一致を確認でき、Claude Webの7個別スキル・
保存済み20ソースも同一です。入力pluginのmapが変わった4環境のうち、Claude Code／Gemini CLI／Copilot CLIは新候補を実機で再検証済みです。
CodexはLinux試験環境の準備が180秒でtimeoutし、package／runtime／image／container／native実行の前段でblockedです。原因未確定・自動再試行なしで、旧成功を継承しません。
現候補は **限定確認12／Roo失敗1／package load前blocked2（Linux Codex＋QueryPie/Aru）／他未実施14、総合受入0／29** です。
今回Claude Code／Gemini CLI／Copilot CLIの3環境で15件のnative metadata操作を新規実行し、7スキルとMCP設定の認識を確認しました。新たなhostedスキルimport・認証済みremote呼び出しは0。Cursor／VS Codeは設定だけ、SDKは合成fixture、Webはスキルだけです。

既存Codex接続では前駆環境の組織・EMS読み取り、CFP5種類とEMSテンプレートCSV／XLSXの原本受領・保存・応答SHA一致・構造を確認しました。
更新scopeのない接続による投入previewは拒否され、token発行・投入・置換はありません。
この前駆環境の結果を、未配備の新候補や29環境の総合受入へ加算しません。顧客ファイルは公開しません。

QueryPie系Aruはimport前のUIでblockedとなり、完了import0・原因未確定です。


新83f9の38資産stageとGET専用helperは用意済みで、386項目の独立レビューは指摘0です。
これはローカル準備と合成metadata14対照の確認で、新候補のDraft upload・live metadata・公開後匿名取得は未実施です。

GitHubの既存1.2.0 Draftは旧f831候補の38資産で、新83f9候補は未uploadです。
[入力一致の記録](docs/candidate-native-equivalence-v1.2.0-canonical-date-license-held-20261026.json)、[候補hash](docs/candidate-package-v1.2.0-canonical-date-license-held-20261026.json)、
[受入記録](docs/ACCEPTANCE.md)と[機械可読記録](docs/acceptance-summary.json)を確認してください。
新OAuth、ChatGPT受入、LICENSE適用は保留し、公式掲載は未申請です。
