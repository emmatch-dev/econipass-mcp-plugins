# EcoNiPass MCP プラグイン（DEV preview）

> [v1.2.0のクライアントDEV preview](https://github.com/emmatch-dev/econipass-mcp-plugins/releases/tag/econipass-mcp-plugin-v1.2.0)をprereleaseとして公開しました。公開日時は2026-10-27 07:18:52 JST（2026-10-26T22:18:52Z）です。Authorization headerなしの匿名GETで38資産のSHA・sizeと37 ZIP・1,016エントリのCRC、LICENSE混入0を確認しました。旧v1.1.0のtag・資産は保持しています。
>
> 公開tagは公開時の原本`df81a01051bb662cef1c4af87b181b087f05e9ed`に固定します。この追加観測を反映するmainの更新対象は文書5件だけで、梱包入力33ファイルと38公開資産を変更しません。配布物の生成source dd389と、この公開tag・後続の文書更新を区別します。

排出量分析、EMS、CFP入力、削減対策、法定報告を支援する7スキルと29環境向け導入キットです。
接続先は **DEV** の `https://api.dev.app.econipass.com/mcp` です。版と公開状態は[GitHub Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)で確認してください。

この版はクライアント配布物のpreviewです。EMSの17操作追加を取り込みました。
DEV backendは20fの通常配備・外部検証・finalizeに成功しました。連動Kongの新runは候補TLS証明書の残存7日検査で停止し、完全なrolloutは未完了です。
サーバー説明修正の監査3ファイルは利用者の承認後に適用し、PR #1806の7 CI成功を経て20fへmergeしました。統合CIの全7 jobとimage buildの非skip 9 jobも成功しています。配備後の認証済みUATはアクセス制約で未実施です。全操作・全29環境の受入やGAは未完了です。
利用にはEcoNiPassアカウント、事業所の権限と必要なOAuth scopeが必要です。
LICENSE適用・新OAuth認可・ChatGPT受入は保留中で、MIT等の利用許諾は追加していません。

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
追加17操作にはマスター更新、再集計、非エネルギー指標の時系列、GHG入力用月別電力量、サイトカレンダー、報告配送などを含みます。配送は外部送信先と権限を個別に確認してください。

CFP取得は既定でファイル情報だけを返し、本人の入力画面で別途取得する手順を案内します。
XLSXを受信できるhost／SDKは明示的にembeddedを選び、実ファイルを確認してから編集・投入します。

ソース登録は通常258、共有法定帳票有効時271、法定レビューも有効な最大構成273、
固定PRD参照タグ構成30ツールです。これらはソースのprofile別登録数で、実環境の公開数ではありません。
[対応表](plugins/econipass/tool-skill-map.json)は14ソースファイルのbyte hashと4profileの登録を束縛します。
接続先の実catalog・権限・scope・機能フラグが、利用できる操作を決めます。

更新はdry-runで具体的な対象と変更を確認し、既存の利用者承認に一致するpayloadと
一回限りの確認tokenで実行します。結果が不明な更新は自動再試行せず、現在状態を読み戻します。
スキルの導入によって権限や新しいOAuth grantが付与されることはありません。

## クライアント別の設定補完

旧Cascadeでは他MCPを含む100ツール上限に合わせ、既定を組織確認1ツールとし、
業務別13設定から一つ選びます。各設定は最大78ツールで、全273ツールを横断してカバーします。
`disabledTools` は未知の追加ツールを隠せないため、実catalogの全ページ・名前・件数・hashを照合し、
差分があれば利用を止めて再生成します。Devin Localの専用設定は旧Cascadeと分けます。
Junie専用MCP配置、旧Qを維持したKiro設定と明示scope、Gemini Enterpriseの初期全Actions無効・
最大100の選択、n8n v1.2以降のHTTP Streamable選択も補完しました。
設定補完はそのクライアントでの実機受入を意味しません。[詳細](plugins/PLATFORMS.md)を参照してください。

## 配布物・実装・受入

37 ZIP＋`release.json`の計38資産、1,016エントリを生成し、SHA・CRC・安全なパス・LICENSE/PDF混入0を確認しました。
release SHA-256は `ff0b309c334bb2878ae5585e0de15d90ae96833eb9ce8f5d02d96f5507d4dbef`、対応表SHA-256は `d4663c7e2819586125b942a180bce689ada706dc975975fa4ded49fd0c36d003` です。
配布・カタログの既存65テスト、7スキルの正式検査、CI同版lintが成功しています。

| 対象 | 確認状態 |
| --- | --- |
| 配布物の生成source | `dd389bd50ba75a280dedb207b75c52434a6a5b5a`。20fのapp／MCP sourceと同じ。梱包入力33ファイル・ff0b・公開38資産は不変 |
| DEV backend | `20f4bd2ecd3dc3bd4cb27c8feb8d31192882599e`。[通常配備run40425777373](https://github.com/emmatch-dev/econipass-backend/actions/runs/40425777373)はattempt1、14 job成功。配備・外部検証・finalizeを完了し、finalizeは2026-10-27 09:34:31 JSTに終了 |
| 承認済みbackend source | [PR #1806](https://github.com/emmatch-dev/econipass-backend/pull/1806)を2026-10-27 08:41:57 JSTにmerge。[統合CI](https://github.com/emmatch-dev/econipass-backend/actions/runs/40421511292)の全7 jobと[image build](https://github.com/emmatch-dev/econipass-backend/actions/runs/40421511490)の非skip 9 jobが成功。対応表14ファイルのGit source bytesも公開候補と一致 |
| 連動Kong | [新run40427278443](https://github.com/emmatch-dev/econipass-backend/actions/runs/40427278443)はsource20f・attempt1で失敗。step12の候補TLS証明書の残存7日検査で停止し、新resource作成・Kong切替へ未到達。push起点40425667397のskipとは別のrun |
| 以前の38ad配備 | [通常配備40285257680](https://github.com/emmatch-dev/econipass-backend/actions/runs/40285257680)は成功。[当時の連動Kong40290693074](https://github.com/emmatch-dev/econipass-backend/actions/runs/40290693074)は候補TLS証明書の残存7日条件で停止した履歴 |
| 以前の公開API／MCP／OAuth／CORS | source38ad時点の2026-10-26の既存公開経路の契約検証成功。20fの配備後UATやKongの新規配備成功へ継承しない |
| CFP／EMS（38ad） | 既存接続でCFP5種・EMS CSV/XLSXのサーバー取得とmetadata応答が成功。当時7件で500なし。MCP業務ファイルの保存・投入・置換は未受入 |
| Claude Web | 2026-10-27、7スキルの実ダウンロードで元source全20エントリが候補と一致。EMS v4は保存後の再読込と有効状態、他6スキルはv2の有効状態を確認 |
| 29環境 | CLI7環境の25 metadata確認、SDK4合成fixture、Claude hostedのスキル保存・読戻し1環境を限定確認12として記録。環境条件未解消2、未実施15（ChatGPT保留を含む）、総合受入0／29 |

Claude Webの取得ZIPには`skills/` prefixとhost生成の`.claude-plugin/plugin.json`が加わるため、元sourceの一致を確認し、ZIP全体のbyte一致は主張しません。
同日の既存DEVコネクタ画面では271件（interactive15／readonly129／write-delete127）と追加EMS17操作のタイトルを確認しました。権限変更・新OAuth・tool実行は0で、schema・業務実行・最大273件の照合は未確認です。

その後、既存Claude Web接続ではToolSearchに`delivery_mode`が露出し、EMS XLSXとCFP masterを明示的な`metadata`で各1回取得しました。metadataは会話へ届き、`server_fetched=true`、`file_embedded=false`、`client_receipt_confirmed=false`、`resource_uri=null`を確認しました。通常MCP呼出し計2・model prompt計3、新OAuth・業務更新・embedded・業務ファイル保存は0です。この追加観測は38adに限定し、20fのDEV受入や全hostのschemaへ継承せず、限定12・総合0／29を維持します。

生成source dd389と現在のDEV source20fはapp／MCP sourceが同じで、対応表の14ファイルもGit source bytesが一致しています。Git sourceの一致と通常配備の受入は別に確認しました。
差分となるサーバー2箇所のdocstringは、ダッシュボードの5種の軽量応答と3種の明示選択の説明を訂正します。
監査3ファイルの承認・適用、CI・image buildと20fの通常DEV配備を完了しました。この配備sourceにサーバー説明修正を含みます。配備後の既存Claude画面確認はブラウザー制御がWork設定で無効のため停止し、EcoNiPassツールも現セッションでは利用できません。20fの認証済みUATは未実施で、以前の38adでのmetadata受領を継承しません。

公開中のAPI証明書は2027-01-01まで有効です。配備が拒否したのはGitHub Secretから渡る候補証明書で、両者の同一性は未確認です。
期限検査は維持しています。新しい連動Kong runではsnapshot・切替・capsuleの後続工程がskipし、tail cleanupの成功をrollout成功へ読み替えません。
repository-levelの候補証明書ペアは更新metadataが2026-08-16のままです。隔離済みの共有旧更新経路は再開していません。既存DEV 2台へのSSHは各1回timeoutとなり、接続経路の確認が残っています。証明書・秘密鍵の読取やhost変更は行っていません。
TLS metadata読取の追加案v2はprotected 2ファイルの人間承認待ちで、共有sourceへ未適用です。

新OAuth、ChatGPT受入、LICENSE適用は保留し、公式ディレクトリ申請とSTG/PRD配備は未完了です。
[受入記録](docs/ACCEPTANCE.md)と[機械可読の概要](docs/acceptance-summary.json)、[以前の配備時点の記録](https://github.com/emmatch-dev/econipass-mcp-plugins/blob/661361786a2202ca256cced6e044255615b2438e/README.md)を確認してください。
