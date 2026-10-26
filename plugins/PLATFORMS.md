# EcoNiPass MCP のプラットフォーム別配布

初版の製品仕様確認日: 2026-10-08、初版ソース: `7ca723a1e877500f4df7f49a3c76a46a48dbb9bd`。
2026-10-26の配布候補は `dd389bd50ba75a280dedb207b75c52434a6a5b5a` を生成元とし、最大273ツールの対応表へ同期しています。
機械可読の正本は [platform-support.json](platform-support.json)、今回の確認範囲は[受入記録](../docs/ACCEPTANCE.md)です。
初版の日付や今回の同期は、未実施環境の製品仕様・実機受入を再確認した意味ではありません。

ここでいう対象は、既存の EcoNiPass 接続ガイドに設定経路があるクライアントです。
**29 種類すべてで実機受入が済んだという意味ではありません。**
接続方式、指示の取込方式、導入条件を区別し、各項目に公式資料とリポジトリ内の根拠を記録しています。

スキルは、公開されたツールをどの順番で使うかを説明します。MCP の URL を登録するだけでは
`SKILL.md` は読み込まれません。ネイティブの読み込み機構がないクライアントでは、配布物の
指示カードをエージェントの指示欄、アプリケーションの system/developer context、または
利用者のタスクへ明示的に取り込みます。必要な参照資料も一緒に渡してください。

## 配布形式

| 対象 | 指示の取込と MCP 設定 |
| --- | --- |
| Codex | 共通 Agent Plugins パッケージ。互換形式は `.codex-plugin/plugin.json` と `.mcp.json`。直接設定時は `config.toml` の `mcp_servers`。[公式](https://developers.openai.com/plugins/build/plugins) |
| ChatGPT / Work | 共通プラグインの skills と remote MCP。利用できるアップロード・組織配布・ディレクトリ掲載経路は利用面と管理方針で異なります。[公式](https://developers.openai.com/plugins/deploy/submission) |
| Claude Code | `.claude-plugin/plugin.json`、`skills/`、`.mcp.json`。HTTP の MCP 設定は `type: http` と `url`。[公式](https://code.claude.com/docs/en/plugins-reference) |
| Claude hosted | 対応する Customize 画面でカスタムプラグイン、または個別 skill ZIP と remote connector を設定。Web/Desktop/Cowork と mobile の設定面は個別確認が必要です。[公式](https://support.claude.com/en/articles/13837440-use-plugins-in-claude) |
| GitHub Copilot CLI | 共通 Agent Plugins。直接設定は `mcpServers`、`type: http`、`url`。[公式](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-plugin-reference) |
| GitHub Copilot in VS Code | 共通 Agent Plugins。直接設定は `.vscode/mcp.json` の `servers`、`type: http`、`url`。プラグイン機能の設定・管理ポリシーも確認します。[公式](https://code.visualstudio.com/docs/agent-customization/agent-plugins) |
| Cursor Desktop | 共通 Agent Plugins または `.cursor-plugin/plugin.json`。直接設定は `.cursor/mcp.json` の `mcpServers` と `url`。[公式](https://cursor.com/docs/reference/plugins) |
| Gemini CLI | `gemini-extension.json` の `mcpServers` と `contextFileName`、`skills/`。リポジトリで確認した認証手順を維持します。[公式](https://geminicli.com/docs/extensions/reference/) |
| Gemini Code Assist / VS Code | Gemini 設定 JSON の MCP と Markdown context。Agent mode で利用可能な拡張・コマンドを個別に確認します。[公式](https://docs.cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer) |
| Windsurf / Devin Desktop | 旧Cascadeは `serverUrl` / `disabledTools` と100ツール以内の業務別設定。新Devin Localは専用 `.devin/mcp_config.json` の `url` / `transport: http`。選択したagentごとに設定・受入を分けます。[Cascade](https://docs.devin.ai/desktop/cascade/mcp)、[Local](https://docs.devin.ai/cli/extensibility/mcp/configuration) |
| JetBrains Junie | skills を `.junie/skills/<name>/` または共有 `.agents/skills` へ配置。native plugin/CLI は `.junie/mcp/mcp.json`（user scope は `~/.junie/mcp/mcp.json`）の `mcpServers.<name>.url`。IDE は Tools > Junie > MCP Settings。AI Assistant/ACP 経路とは分けて受入します。[skills](https://junie.jetbrains.com/docs/agent-skills.html)、[native MCP](https://junie.jetbrains.com/docs/junie-cli-mcp-configuration.html)、[IDE](https://junie.jetbrains.com/docs/junie-ide-plugin.html) |
| Zed Agent | `.agents/skills` と `context_servers.<name>.url`。外部 ACP agent や terminal thread の設定は別です。[skills](https://zed.dev/docs/ai/skills)、[MCP](https://zed.dev/docs/ai/mcp) |
| goose | `.agents/skills` または skills プラグイン。MCP は別の YAML `extensions` に `type: streamable_http` と `uri`。[公式](https://goose-docs.ai/docs/getting-started/using-extensions/) |
| Amazon Q Developer CLI / Kiro CLI | 旧 Q の agent prompt/context と `type: http`/`url` を維持。Kiro successor alias は同じ配布キットの専用断片を `.kiro/settings/mcp.json` へマージし、skills を `.kiro/skills/<name>/` へ配置。新 Kiro のみ server 名 `ep`、`oauthScopes: [mcp:read]`。Q/Kiro の受入は別記し、29 target を増やしません。[旧 Q](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-mcp-config-CLI.html)、[Kiro MCP](https://kiro.dev/docs/mcp/configuration/)、[skills](https://kiro.dev/docs/skills/) |
| Cline | `.cline/skills` と `mcpServers` の `type: streamableHttp`、`url`。現公式は native OAuth を案内しています。[skills](https://docs.cline.bot/customization/skills)、[MCP](https://docs.cline.bot/mcp/mcp-overview) |
| Roo Code | `.roo/skills` 等と `.roo/mcp.json`。native OAuth は今回の公式資料で確立していないため、下記の無効状態の bridge テンプレートと導入条件を用意します。[公式](https://roocodeinc.github.io/Roo-Code/features/mcp/using-mcp-in-roo/) |

Junie native と Q/Kiro successor の上記経路は 2026-10-26 の公式資料に合わせた導入案です。クライアントの実行・ログイン・認可は行っていません。キットの `skills/` 自体をネイティブ探索先へ重ねず、その直下の7つのスキルフォルダーと参照文書を配置します。

Kiro では旧 Q と新 Kiro の設定断片を同じ接続先へ重複登録しません。同梱の Kiro 設定は既定 OIDC scope の代わりに `mcp:read` を指定し、新しい認可を自動実行しません。短い `ep` は、公式の `@server/tool` 形式で登録273操作の最長 selector を60文字に抑えます。内部モデル名の変換式まではこの静的確認で保証せず、任意 report-v2 を含む実際の全 tool catalog を導入版で確認します。新 Kiro の成功を旧 Q の成功に数えたり、その逆に流用したりしません。

共通 Agent Plugins は、ルート `plugin.json` と `mcp.json` の同じ版の schema 宣言、
`skills/<name>/SKILL.md` を使います。互換 manifest の単純なファイル名変更ではありません。
Claude 用と Gemini 用はそれぞれの形式を維持します。goose の skills プラグインを入れただけで
MCP extension も登録されたとは判断しません。

### Legacy Cascade の業務別ツール設定

Windsurf用キットの `configuration/mcp_config.json` は、接続確認と所属組織の確認に使う
`get_my_organizations` だけを有効にします。業務を始める前に
`configuration/legacy-cascade-presets.json` の一覧から該当する
`configuration/presets/<業務>.mcp_config.json` を**一つ**選び、既存設定の
`econipass` エントリだけを入れ替えます。設定全体を上書きしたり、複数プリセットを
別サーバー名で並べたりしないでください。13プリセットで現行最大273ツールを網羅し、
各設定は最大78ツールです。他の有効MCPサーバーを含む合計を100以内にします。

EMSの7分類は同梱の `skills/ems-operations/references/workflows.md` に沿います。
取込・復旧、マスタ・実測、監視、費用・アラート、監督・タスク、共有分析、M&Vに分け、
各設定に所属組織の確認と9種類の読み取り専用マスタ参照を含めます。分類根拠、担当ツール、
共通参照、有効数はJSON一覧に記録します。業務をまたぐ場合は同じサーバーの設定を
切り替え、権限・確認・`dry_run` の条件を維持します。

接続を使う前に、フィルター前の実 `tools/list` を最終ページまで取得し、重複がないこと、
全論理名が一覧の `catalog_tools` に含まれること、件数とソート済み名前のSHA-256が
`registered_profiles` のいずれかと完全一致することを照合します。ハッシュの入力は
ソート済み名前を改行で連結し、末尾にも改行を一つ付けたUTF-8です。
Cascade画面でも有効数と他サーバーを含む合計を確認します。画面の件数だけでは名前の照合に
なりません。実カタログが違う場合は接続の利用を止め、更新したソース一覧から設定を再生成し、
レビュー後に再確認します。

`disabledTools` は除外リストなので、将来増えた未知のツールを自動で隠せません。
生成処理は未知の分類・不整合な一覧・100超過を拒否しますが、実行中のカタログ制限や
サーバー側の認可を代行しません。既存の認証・利用者確認は維持します。
この設定は旧Cascade用です。新しいDevin Localへ100ツール上限を流用しません。

### Devin Local / CLI の設定

[新しいタブの既定agentはDevin Local](https://docs.devin.ai/desktop/devin-local)です。
同じキットの `configuration/.devin/mcp_config.json` は、Devin CLI v3000.3以降と
それを使うDevin Local向けです。プロジェクトの `.devin/mcp_config.json` へ
`econipass` エントリをマージします。`url` と `transport: http` だけを設定し、
旧Cascadeのプリセットとは併用しません。旧版のメイン `config.json` にあった設定は
[製品側が専用ファイルへ自動移行](https://docs.devin.ai/cli/extensibility/mcp/configuration)します。
同梱skillsはプロジェクトの `.devin/skills` または `.agents/skills` へコピーします。
[スキル配置の公式仕様](https://docs.devin.ai/cli/extensibility/skills/overview)も確認してください。

認可が承認された後の手順は `devin mcp login econipass --scopes mcp:read` です。
`--scopes` はログイン時の指定で、JSONへ未定義のscope項目を追加しません。
新規OAuthが保留の間は実行せず、認証情報・自動承認・resource上書きを設定に含めません。
旧Cascadeでの受入をLocalの成功へ継承せず、それぞれの版・設定・実カタログ・認証・業務操作を
個別に検証します。

### Roo Code の OAuth bridge

[roo-code-bridge.json](adapters/roo-code-bridge.json) は、利用者が明示的に導入する
`mcp-remote@0.14.3` をローカルの Node で起動する設定です。生成時にはインストールも起動も
行わず、`disabled: true` と絶対パスのプレースホルダーを残します。導入者はこの版と依存関係を
確認して専用ディレクトリへ固定し、`package.json` の版と lockfile を確認したうえで、Node と
`dist/proxy.js` の実際の絶対パスを設定して有効にしてください。`econipass` の remote 設定と
bridge 設定は併用せず、利用する方を一つ選びます。

公開パッケージの SHA-512、版、実行入口、引数の存在を静的に確認しました。
完全な依存関係のセキュリティ監査や EcoNiPass との実機接続は実施していません。
`http-only` で `/mcp` に接続し、public client の OAuth metadata に `mcp:read` を指定します。
利用者によるブラウザー認証、loopback callback、refresh/revoke は導入環境で確認します。
確認した版と integrity は機械可読の正本にも記録しています。
[固定ソースの引数仕様](https://github.com/punkpeye/mcp-remote/blob/6a06aca546a8fd3b7beb040f39761b364893198d/README.md)、
[公開パッケージ情報](https://registry.npmjs.org/mcp-remote/0.14.3)。

## 管理画面で設定する接続先

これらの `connection.json` は入力値をまとめるための**導入資料**です。
各製品にそのままインポートできるアプリ manifest、solution、workflow とは扱いません。

| 対象 | 操作手順の取込 | 接続条件 |
| --- | --- | --- |
| QueryPie AIP | Agent の Instruction / Skills と MCP Integrations | 利用者本人の OAuth。EcoNiPass 側は DEV/dev-lite の `/sse` 互換経路。[公式](https://aip-docs.app.querypie.com/en/user-guide/agents) |
| Copilot Studio | Agent Instructions と個別に選んだ MCP tools | OAuth Dynamic discovery、環境の callback 方針、generative orchestration。初期 profile は read-only。[公式](https://learn.microsoft.com/en-us/microsoft-copilot-studio/mcp-add-existing-server-to-agent) |
| Microsoft 365 Copilot | declarative agent の指示と MCP action/connector | テナント固有の agent/app を Agents Toolkit で構成。更新可否は別途受入。[公式](https://learn.microsoft.com/en-us/microsoftteams/platform/m365-apps/agent-connectors) |
| Gemini Enterprise | agent/task の指示にカードを取り込みます。 | confidential OAuth と Streamable HTTP。data store の Actions で Reload custom actions 後、必要な参照 actions を選択し Enable actions。同時有効化は最大100件、初期はすべて無効です。Active 表示だけを tool 受入と数えません。再認証・scope追加の同意は別です。[公式](https://docs.cloud.google.com/gemini/enterprise/docs/connectors/custom-mcp-server/set-up-custom-mcp-server#enable-actions) |
| Cursor Web / Cloud / Automations | hosted agent/project 指示またはカード | hosted callback の実測と環境 allowlist。Desktop の plugin 導入が伝播するとは仮定しません。[公式](https://cursor.com/docs/mcp) |
| Perplexity | task や利用可能な指示欄へカードを取り込む | remote connector URL と OAuth。callback、アカウント、surface を実機確認。[公式](https://www.perplexity.ai/en-GB/changelog/what-we-shipped---march-13-2026) |

## API・自動化クライアント

EcoNiPass PAT は本人が発行する期限付き・scope 限定・失効可能なトークンです。
**backend と MCP の両方で機能を有効にする必要があり、既定は無効、許可 scope の既定は
`mcp:read` です。** プラグインの生成や導入は、この設定を有効にせず、token も発行しません。
アプリが持つ secret store / 実行時の環境変数を参照します。

| 対象 | 指示の取込と認証情報の受渡し |
| --- | --- |
| OpenAI Responses API | `instructions` / developer context にカードを読み込み、MCP tool の `authorization` に実行時 PAT を渡す。[公式](https://developers.openai.com/api/docs/guides/tools-connectors-mcp) |
| OpenAI Agents SDK | Agent instructions と `HostedMCPTool` の `authorization` / read-only allowlist。APIサンプルはprovider-hosted接続を使います。[公式 overview](https://developers.openai.com/api/docs/guides/agents) |
| Anthropic Messages API | system context と `mcp_servers[].authorization_token`。現 beta の tool selection は `mcp_toolset` で設定する。[公式](https://platform.claude.com/docs/en/agents-and-tools/mcp-connector) |
| LangChain / LangGraph | system prompt と MCP adapter。旧 `MultiServerMCPClient` と新 `MCPAdapter` の設定を混ぜない。[公式](https://docs.langchain.com/oss/python/migrate/langchain-mcp-adapters) |
| n8n | AI Agent の指示と MCP Client Tool の Bearer/Header credential。node の typeVersion1.2以上で HTTP Streamable を選択し `/mcp` へ接続します。workflow parameter は `serverTransport=httpStreamable` と `endpointUrl` で、導入資料のJSONを workflow として取り込むものではありません。旧 typeVersion1 の SSE 専用欄を使いません。[公式](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp)、[固定source](https://github.com/n8n-io/n8n/blob/cfbd9a56cba2e73901dc1962e47727adbea0b23e/packages/%40n8n/nodes-langchain/nodes/mcp/McpClientTool/McpClientTool.node.ts) |
| Dify | Agent 指示と MCP tool の Custom Headers。別 workspace では同じ server identifier の設定が必要。[公式](https://docs.dify.ai/en/cloud/use-dify/workspace/tools) |
| GitHub Copilot cloud / code review | repository skills/instructions と MCP 設定の `COPILOT_MCP_` secret 参照。remote OAuth とは別経路。明示的な read-only tool allowlist を使う。[公式](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/configure-mcp-servers) |

非対話型の処理が確認トークンを自動的に発行・消費する設計は、この配布物の対象ではありません。
更新には EcoNiPass の権限、scope、監査、`dry_run` と一回限りの確認を維持する必要があります。
プロンプトやクライアントの tool allowlist は、サーバー側の認可に代わりません。

### GitHub Copilot cloud の初期設定

[github-copilot-cloud.json](adapters/github-copilot-cloud.json) をリポジトリの
Settings → Copilot → MCP servers の既存設定へマージします。
`COPILOT_MCP_ECONIPASS_PAT` は Agents secret として設定し、値には `Bearer ` を付けず
EcoNiPass の `mcp:read` PAT 本体だけを保存します。設定中の
`Bearer $COPILOT_MCP_ECONIPASS_PAT` は GitHub による実行時の展開用で、認証情報は含みません。

初期 allowlist は組織一覧、入力状況、省エネ法・温対法データ、EMS dashboard・site・point の
参照 7 件です。環境で公開されるツールとの差は実際の catalog で確認してください。
cloud agent はツールを自律実行でき、remote OAuth と MCP resources/prompts は未対応です。
code review は `readOnlyHint: true` のツールに限られます。更新とファイル取得はこの初期設定に
含めず、ファイル添付の受信は別途受入します。
[GitHub の設定・secret 展開仕様](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/configure-mcp-servers)。

## 既存資料との差分と受入

- 古い Copilot/Gemini ガイドの「持ち込み token は対象外」は、現在の PAT 実装とは分けて読みます。
  配布物の利用は[導入手順](../README.md)と[接続確認スキル](econipass/skills/setup/SKILL.md)に従い、現在の接続schema・権限を確認します。
  PAT発行や新scope付与は今回の受入に含めません。
- Cline の bridge-only、Perplexity の macOS-only、古い tool 件数は今回の対応条件へ転載しません。
  現公式資料と実際の `tools/list` で確認します。
- Gemini CLI の `type: http` と `url` は
  [v0.55.1 の公式設定ソース](https://github.com/google-gemini/gemini-cli/blob/v0.55.1/packages/core/src/config/config.ts#L475-L480)
  に合わせています。`httpUrl` と `url` を別 transport と説明する旧 Web 文書との混在を避け、
  導入版の設定仕様を確認します。
- Google は個人向け Gemini Code Assist / CLI の提供変更を案内しています。
  [対象プランの現行条件](https://docs.cloud.google.com/gemini/docs/codeassist/code-overview)を確認し、
  Standard/Enterprise と個人向けを一括して扱いません。
- Azure Foundry、Bedrock AgentCore、Open WebUI、LibreChat、Slack AI、Agentforce、Devin cloud、
  Manus、consumer Gemini、Amazon Q Business、exaBase は別の候補一覧です。ベンダーの現在の
  MCP 有無を否定する表ではなく、EcoNiPass の接続受入を今回確立していない対象です。

受入はプラットフォームごと・環境ごとに、認証/refresh/revoke、実際の tool catalog、参照操作、
scope 拒否、対象組織の境界を確認します。更新を提供する構成では dry-run の表示と人の確認、
一回限り token の再利用拒否まで確認します。ファイル機能では添付・バイナリ受取と上限も対象です。
静的な配布物の検証、MCP サーバーのテスト、クライアント実機受入を別々に記録してください。
