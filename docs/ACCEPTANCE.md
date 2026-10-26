# DEV向けMCP配布物の検証・受入

配布版・公開状態は [GitHub Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)、公開日時とtagの対象commitはRelease metadataで確認してください。
この文書は **2026-10-26T06:35:11.051765+00:00** の確認範囲を示します。

実装sourceは `a113b01cb250c9d57c225e7c487570d99783bc22`。全必須CIとimage build／promoteが成功しています。
[CI](https://github.com/emmatch-dev/econipass-backend/actions/runs/40270099289)と[image workflow](https://github.com/emmatch-dev/econipass-backend/actions/runs/40270099317)を参照してください。
配布物のsource bindingは`release.json`で確認できます。MCP実装84ファイルと配布source14は83f9の束縛と同一です。アプリは更新を含み、旧6f099／0d80との全体同一性は主張しません。新sourceのアプリ監査：fadbfebaで再監査したアプリ2,196ファイル（digest 24487902…）とMCP84ファイル（digest daa9dd60…）の束縛がa113に一致。
新しい台帳source_row投影の実tenant受入は未実施です。今回のmetadata応答確認からその成功は推定しません。

1.2.0の38資産（37 ZIP＋`release.json`）は2026-10-26T01:13:13Zに認証済みGETで実bytesを受領し、size／SHA／CRC・1,016エントリを確認しました。
release SHA-256: `83f900b69c53acea93f5dbdee7ddc1d7611acd324f23bae77790b40576e952bc`。対応表SHA-256: `224f3ae9b21e1f3ea594b85d2d0e7cc161d593d36dd75ed6679e5aa6f7381065`。
この確認は、公開後匿名GETやクライアントの業務受入を意味しません。

| 実行環境・機能 | 確認結果 |
| --- | --- |
| DEV backend／MCPの配備 | [成功：a113・attempt1、deploy／verify／finalize](https://github.com/emmatch-dev/econipass-backend/actions/runs/40274300029) |
| Kongの配備 | [成功：a113・attempt1、deploy／verify／finalize](https://github.com/emmatch-dev/econipass-backend/actions/runs/40275773734) |
| 公開API／MCP／OAuth／CORS | full API／MCP／OAuth／CORS helperの1回検証が成功。frontendは200・非空HTML（画面操作の受入とは別） |
| 新sourceでの認証済みCFP | 5種類でサーバー取得＋metadata応答成功、500なし。embedded受領・保存・投入／置換は未受入 |
| 新sourceでの認証済みEMS | CSV／XLSXのサーバー取得＋metadata応答成功、500なし。embedded受領・保存・更新は未受入 |

## クライアント受入の範囲

| 状態 | 環境数・範囲 |
| --- | --- |
| 限定確認 | 12。過去入力一致9と、新しいnative metadata確認3 |
| 元失敗を保持 | Roo1 |
| package load前blocked | 2。Linux Codexの環境準備、QueryPie/Aruのimport前UI |
| 他未実施 | 14。ChatGPT保留を含む |
| 総合受入 | 0／29 |

Claude Code／Gemini CLI／Copilot CLIの3環境では15件のmetadata操作で7スキルとMCP設定を認識しました。
Cursor／VS Codeは設定だけ、SDKは合成fixture、Claude Webは7個別スキルの過去入力一致です。
Rooは元の0スキル検出を保持し、TEMP設定のMCPを無効にした別診断では7スキルのmetadataを確認しました。
別診断は配布ZIPと入力が異なり、スキル本文の利用・MCP接続・認証済み業務の受入へ加算していません。
Linux Codexのstartup失敗後、専用VMの停止と元設定の復元は完了しました。native受入は未実行です。

前駆環境のCFP5種・EMS CSV／XLSX取得や読み取りを、上表の新source結果へ流用しません。
CFP投入・置換・更新の受入は読み取り・ファイル受領と分けます。権限のない操作は成功へ加算しません。
今回の既存読み取り接続では組織アクセス・月次ゲート・EMS取込一覧を確認しました。接続の入力定義にはdelivery_modeが露出しておらず、embedded呼出し・保存・preview・投入・置換は0です。新しいmetadata応答を受信できた事実と、ファイル本体の受領・業務更新は分けます。
sourceの束縛は完了したDEV／Kong workflowによるもので、health応答自体がsource SHAを提示したわけではありません。
顧客値・事業所ID・名称・原本ファイル・顧客ファイルdigest・資格情報は公開しません。

今回のLICENSE適用、追加OAuth認可、ChatGPT受入は保留です。公式ディレクトリ申請は未完了です。
固定PRD参照profileは30操作・8タグの監査境界を維持し、STG／PRD配備は進めていません。
[機械可読概要](acceptance-summary.json)と[a72時点の履歴](https://github.com/emmatch-dev/econipass-mcp-plugins/blob/a72fb24fa8ca97db94091e9452a07d5a69195cbf/docs/ACCEPTANCE.md)を参照してください。
