# DEV 1.1.0 の実機受入・公式掲載状況

確認日: 2026-10-21 JST。接続先は `https://api.dev.app.econipass.com/mcp`。
配布物1.1.0のbackendソースは `37284f6c8f17175984ded533bea471693443aada`。
今回確認したDEV稼働版は `fde1cffb48d9c4be297c622087335df5177dbd3d` です。
[backend配備](https://github.com/emmatch-dev/econipass-backend/actions/runs/39525015891)と
[Kong配備](https://github.com/emmatch-dev/econipass-backend/actions/runs/39526711825)の公開検証・最終確定を確認しました。
2026-10-21 01:25–01:26 UTCに、既存接続でCFP入力Excelの5種類を認証付きで取得できました。
このページに記載したクライアント・操作以外の実機成功を意味しません。

**全29環境の総合受入は0件です。** 現時点で、4クライアントのネイティブ読み込み、
4 API SDKのオフライン互換性、CursorとVS CodeのCLI設定読み込み、
gooseとCline CLIのスキル認識・MCP設定読み戻し、Claude Webへの7スキルの取り込みを確認しました。
これらの結果と、既存Codex接続による認証済み参照を分けて記録しています。

## 確認できたこと

| 対象 | 実施内容 | 結果 |
| --- | --- | --- |
| Claudeの既存EcoNiPass接続 | `get_fields_spec(report_type="freon", language="jp")`の実ツール応答をWebで確認 | フロン3様式・項目数4/1/2。この応答の実行起点がDesktopとWebのどちらかは未確定。後述のスキル取り込みより前の観測 |
| Claude Webの既存接続・追加EMS操作 | `estimate_ems_management_cost`を架空の対象IDで1回実行 | HTTP 404 / EEMS40460の実応答を確認。対象なしの拒否確認で、正常な料金試算・別事業所fixtureの受入は未確認。更新なし |
| Claude Webの7スキル | 公開1.1.0の7個の`.skill.zip`を取り込み、My Skillsと各詳細画面を確認 | 7スキルすべて有効。公開ZIPのハッシュと19ファイルの同一性を確認。MCP設定の追加・新規OAuth認可なし。Claude内部の初回版表示`v1`は配布版1.1.0とは別 |
| Claude Webの`cfp-input`実行時読み込み | `/cfp-input`で実データを使わない説明試験 | スキルと`workbooks.md`の読み込みを実行履歴で確認。5カテゴリ・権限・置換保護・プレビューと反映・再確認の説明を確認。MCP実行なし。他6スキルのモデル実行や業務投入は未試験 |
| Codex desktopの既存EcoNiPass接続 | 認証済み組織一覧・EMSサイト一覧の取得 | 成功。業務データは本リポジトリに保存しない |
| 同じ接続の更新scope不足 | EMSサイト作成の`dry_run=true`を要求 | 更新権限不足として拒否。確認tokenの発行・更新実行なし |
| Codex CLI 0.163.0-alpha.10.2 | 専用設定ディレクトリでmarketplace登録、plugin導入、native一覧・詳細の照会 | 1.1.0、7スキル有効、MCP設定1件を確認。通信を遮断した読み込み検証 |
| Claude Code 2.1.299 | 専用設定・`--plugin-dir`でnative検証と詳細照会 | エラー0、警告0、1.1.0、7スキル、MCP設定1件。通信を遮断した読み込み検証 |
| GitHub Copilot CLI 1.0.100 | 専用設定でmarketplace登録、plugin導入、skill・MCP一覧の照会 | 1.1.0、7スキル有効、HTTPのMCP設定1件。通信を遮断した読み込み検証 |
| Gemini CLI 0.64.0 | 専用設定でextensionの検証・link・一覧、skills・MCP一覧の照会 | 1.1.0、7スキル、`GEMINI.md`、HTTPのMCP設定1件。通信を遮断し、最終確認では対象MCPを設定で除外 |
| Cursor Desktop 3.25.9 | 専用ユーザープロファイルで`--add-mcp`と設定の読み戻し | CLIの設定解析のみ成功。CursorのUI・プラグイン・7スキルの読み込みと実接続は未確認 |
| VS Code 1.142.0の付属CLI | 公式配布・署名を検証した隔離コピーで`--add-mcp`、専用profileの保存内容を照会 | CLIはMCP名の追加を表示し、保存ファイルは公開キットと同じHTTP種別・DEV URL。通信・Keychain・既存homeを遮断。7スキル・Copilot・エディターUI・実接続は未確認 |
| goose 1.55.0 | 専用設定・workspaceで`skills list`と`info --verbose` | EcoNiPassの7スキルとMCP設定1件を確認。通信を遮断した設定・スキル読込で、プラグイン識別・版確認、認証、MCP接続は未実施 |
| Cline CLI 3.0.73 | 専用設定・workspaceで`config skills --json`と`config mcp --json` | 公開キットと同一の7スキル、MCP設定名・streamableHttp・有効状態を読み戻し。通信・Keychain・browser openを遮断。CLIが出力しないURLは保存ファイルの一致のみ確認。VS Code拡張・実接続は未確認 |
| Roo CLI 0.1.17（公式pre-release） | 専用workspaceで`list commands --format json` | 公開キットと一致する7スキルの名前・説明・projectパスを認識。本文のactivation・MCP設定・VS Code拡張・実接続は未確認。現リポジトリは2026-05-15からarchived |
| JetBrains Junie CLI 3659.7 | 公式配布を検証した隔離コピーで起動・ACP初期化 | 起動と初期化は成功。セッション作成が認証要求で停止し、キットのスキル・MCP認識には未到達。新規認証・モデル実行なし。部分受入には加算しない |
| Codex desktopのCFP入力Excel取得（旧稼働版`37284f6`） | master / base_unit / activity_amount / pcf_certification_period / aist_idea | 5種類ともbackend HTTP 500。ファイルの受領なし |
| DEV Web画面のCFPマスタ取得（旧稼働版`37284f6`） | 既存ログインで標準ダウンロード操作 | HTTP 500 / E000003。同じ問題を再現 |
| Codex desktopのCFP master再取得（診断版`94ae94f`） | 2026-10-20 19:11:50 UTCに既存接続でmasterのみ再試験 | HTTP 500を再確認。新規OAuth認可なし。他4種類は診断版で未再試験 |
| Codex desktopのCFP入力Excel取得（修正版`fde1cffb`） | 2026-10-21 01:25:54–01:26:36 UTC、同じ認証済み組織・日本語設定で5種類を順番に取得 | 全5種類で埋め込みファイルを受領。MIME・メタデータのサイズ一致・ZIPヘッダー対応・必須OPCパーツを確認。CRC実体・XML・セル内容は未検証。新規OAuth認可・アップロード・業務更新なし |

CLIの読み込み検証は公開配布ソースとファイルハッシュを照合して実施しました。
既存ユーザー設定・認証情報を変更していません。MCP接続済みのCodex desktopでの
参照成功と、配布プラグインのCLI読み込みは別の証跡です。

Codex CLIの新規MCP OAuth接続は、利用者の選択で認可前に保留しました。
Claude Codeは同意を実施せず、待機処理を終了しました。
新しいaccess token・refresh tokenは取得しておらず、両CLIでの認証済み参照は未実施です。
GitHub Copilot CLIとGemini CLIでもprovider認証・MCP OAuth・モデルAPIを実行していません。
Geminiの初回skills一覧はMCP検出を試みましたが、通信遮断によって接続は成立していません。
CursorのCLI設定保存が、Cursor Agentの実行時設定にも反映されるかは未確認です。
gooseは公式配布のハッシュと公開キットの同一性を確認し、既存ホーム設定・Keychainへの
アクセスも遮断しました。provider認証・モデル実行・MCP OAuthは行っておらず、
プラグインを識別した上記4クライアントとは別の「設定・スキル読込」段階に数えます。
Cline CLIも同じ段階で、公開キットのファイル同一性と7スキルの本文を確認しました。
Roo CLIの確認は7スキルのメタデータだけを読む別段階です。
[公式0.1.17 pre-release](https://github.com/RooCodeInc/Roo-Code/releases/tag/cli-v0.1.17)を使用し、
現リポジトリのarchived状態を記録しています。
VS CodeもCLIの設定保存だけを確認し、既存のアプリ・ユーザー設定・資格情報は変更していません。
Claude Webは公開スキルの取り込みを別段階として数えます。Webでの確認をDesktop・mobile・Coworkへ転記しません。
部分検証したキットは14件ですが、全体の受入完了は0/29のままです。

旧版での`INVALID_ARGUMENT`表示は上流HTTP 500であり、利用者の入力ミスとは断定していません。
修正版では一時領域への書き込み権限を修正し、上記の5種類の再取得で500は再発していません。
取得できたファイルの本文・内容ハッシュ・顧客ID・名称・ファイル名は検証記録に保存していません。
この結果はファイル取得の受入であり、投入・置換、サイズ上限や全エラー条件の実機受入は未完了です。

## ツール公開数の観測

| 観測元 | 件数・状態 |
| --- | --- |
| 1.1.0のソース登録 | 最大243ツール。うち法定レビュー2件は条件付き登録 |
| 旧稼働版`37284f6`のDEV配備readiness記録 | 2026-10-20 11:45:07 UTCに`ready=true`、`published_tools=241` |
| 診断版`94ae94f`のDEV配備canary | 241ツール。認証済み`tools/list`の全件照合とは別の観測 |
| 既存Codex接続に表示されたメタデータ | 診断版の配備後、2026-10-20 19:15:50 UTCに再取得して183ツール。配備前の記録とツール名の集合は一致。EMSはソース167件のうち109件が表示され、58件（参照25・更新33）が未観測 |
| Claude Webの既存接続カタログ | 14 interactive＋119 read-only＋108 write/delete＝241ツール。ソースのEMS追加58操作（参照25・更新33）すべての表示名を確認。「ツールリストを更新」後も241件。権限設定の変更・新規OAuth認可なし |

配備時のreadiness／canary件数、記録済みのクライアントメタデータ、現在の認証済みMCP
`tools/list`は別の観測です。最後の`tools/list`は未確認で、法定レビューの実環境フラグ値も
確認していません。ソースにあるツールが現在呼び出せるとは断定せず、件数差の原因を
キャッシュ・配備・権限のいずれかに決めつけていません。

Claude Webの既存接続では再検出を完了しました。UI表示名の照合はraw `tools/list`の
取得や、各EMS操作の実行成功とは区別します。Codex側は引き続き既存接続の再検出経路を
確認したうえで、実配備ソースに対応する
認証済み`tools/list`の全ページと、クライアント側の表示を照合する必要があります。
ChatGPTへ直接接続したcustom MCPには、Refresh → メタデータの変更確認 → 新しい会話で
再検証する[OpenAI公式手順](https://developers.openai.com/plugins/deploy/connect-chatgpt#refresh-metadata)があります。
Business/Enterprise/Eduの管理者は、有効な既存接続とアプリ管理権限があれば再作成せず更新できます。
Enterprise/Eduのaction controlsでは新しいactionsは初期無効です。[管理手順](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt)を確認してください。
これはChatGPT向けの案内で、現在のCodex desktop接続への適用・成功は未確認です。
現在のCodex desktop接続でのRefreshは未実施です。
この観測では新規OAuth grantを取得していません。ツール名の公開確認と、
CFPファイル取得やEMS操作の機能受入は別に記録します。

## API SDKのオフライン互換性

公開ZIP内のサンプルファイルは変更せず、実行時の設定と外部通信・実行処理を試験用に
差し替え、専用のPython環境で次を確認しました。
認証情報には架空の値だけを使い、通信を遮断しています。
実際のprovider API、モデル推論、EcoNiPassへの接続・ツール実行は行っていません。

| 対象・SDK版 | 確認した範囲 |
| --- | --- |
| OpenAI Responses API — `openai 3.35.1` | サンプルのSDKリクエスト生成をメモリ内の試験用HTTP応答で確認。組織一覧1ツールのallowlistと`store=false`を確認 |
| OpenAI Agents SDK — `openai-agents 0.24.0`、`openai 3.35.1` | native `Agent`・`HostedMCPTool`の構築と1ツールのallowlistを確認。`Runner`の実行は試験用処理に置換 |
| Anthropic Messages API — `anthropic 1.15.0` | サンプルのSDKリクエスト生成をメモリ内の試験用HTTP応答で確認。既定のツール無効化と組織一覧だけの有効化を確認 |
| LangChain / LangGraph — `langchain 1.4.6`、`langgraph 1.2.16`、`fastmcp 4.1.2`、`langchain-openai 1.7.2` | 同一プロセス内の試験用MCPからの検出、allowlist外ツールの除外、nativeモデルの構築とグラフのコンパイルを確認。グラフ実行は試験用処理に置換 |

4件とも、このローカル互換性確認の範囲で成功しています。リモートAPIの受理、
モデルの利用権、認証、実データの参照成功は未確認です。PATの発行や機能の有効化、
既存grantのコピー、顧客データの試験入力は行っていません。

## 29環境の受入範囲

29件は[配布キットの製品別エントリ](../../plugins/platform-support.json)です。
desktop / CLI / IDE / web / mobile / cloudで設定や実行経路が異なる場合、
それぞれの証跡が必要です。1つのsurfaceの成功を製品全体へ転記しません。

完了条件は、導入・7スキル読込、認証済みの実際のtool catalog、参照結果、
OAuth更新またはPAT rotation、専用grantの失効、scopeと事業所境界の拒否です。
更新を提供する構成では、専用fixtureでdry-run、対象と置換範囲の確認、
1回の実行・読み戻し・確認token再利用拒否まで確認します。
CFPは5種のファイル、添付受領、サイズ上限、既存データ保持も対象です。

全29環境の総合受入は未完了です。既存ユーザーの認証を失効させたり、
既存の業務データを置換したりして受入を成立させることはありません。
専用fixture・各サービスの利用可能なアカウント・必要な実機が準備できた範囲で続行します。

[環境ごとの確認状況](acceptance-summary-v1.1.0-20261021.json)は、ローカルクライアントの所在と
実施済みの検査を分けて記録します。「未検出」は今回調べた端末の範囲であり、
製品がMCPに非対応であるという意味ではありません。

## 公式ディレクトリ

| 公開先 | 状況 |
| --- | --- |
| GitHub公開リポジトリ・Release | DEV 1.1.0を公開済み |
| MCP公式Registry | DEV専用の`io.github.emmatch-dev/econipass-dev`、`1.1.0-dev.1`を準備。公式CLIの検証成功。公開操作は未完了 |
| OpenAIのChatGPT / Codex公式ディレクトリ | 公開者確認が未完了のためZIP下書き作成前で停止。本番HTTPS URL、審査専用アカウント、動画等も必要 |
| Claudeディレクトリ | 申請ポータルへのログイン、専用審査環境、plugin内README・配布ライセンス等の準備が必要。申請未完了 |

MCP Registryの登録はOpenAIやClaudeの審査承認を意味しません。
現在のDEV URLを、本番URLや全29環境での受入完了として申告しません。
公開用アカウント・認証情報・審査用秘密情報は本リポジトリへ保存しません。

公式の申請要件:
[OpenAI](https://developers.openai.com/plugins/deploy/submission-errors)、
[Claude](https://code.claude.com/docs/en/plugins/publish)、
[MCP Registry](https://github.com/modelcontextprotocol/registry/tree/main/docs).
