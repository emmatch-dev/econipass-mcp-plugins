# EcoNiPass MCP のプラットフォーム別配布

プラットフォーム仕様の確認日: 2026-10-08。機械可読の正本は
[platform-support.json](platform-support.json)です。配布版1.1.0の検証は
[VALIDATION.md](VALIDATION.md)を参照してください。

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
| Windsurf Cascade | `SKILL.md` と `mcpServers.<name>.serverUrl`。現公式は Devin Desktop 文書へ移転し、旧 `.windsurf/skills` も扱います。[skills](https://docs.devin.ai/desktop/cascade/skills)、[MCP](https://docs.devin.ai/desktop/cascade/mcp) |
| JetBrains Junie | `.junie/skills` 等の skills と IDE の MCP 設定。HTTP JSON は `mcpServers.<name>.url`。IDE/Junie の版を確認します。[skills](https://www.jetbrains.com/help/air/skills.html)、[MCP](https://www.jetbrains.com/help/ai-assistant/mcp.html) |
| Zed Agent | `.agents/skills` と `context_servers.<name>.url`。外部 ACP agent や terminal thread の設定は別です。[skills](https://zed.dev/docs/ai/skills)、[MCP](https://zed.dev/docs/ai/mcp) |
| goose | `.agents/skills` または skills プラグイン。MCP は別の YAML `extensions` に `type: streamable_http` と `uri`。[公式](https://goose-docs.ai/docs/getting-started/using-extensions/) |
| Amazon Q Developer CLI | agent の prompt/context と `mcpServers` の `type: http`、`url`。Kiro の設定形式と混同しません。[公式](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-mcp-config-CLI.html) |
| Cline | `.cline/skills` と `mcpServers` の `type: streamableHttp`、`url`。現公式は native OAuth を案内しています。[skills](https://docs.cline.bot/customization/skills)、[MCP](https://docs.cline.bot/mcp/mcp-overview) |
| Roo Code | `.roo/skills` 等と `.roo/mcp.json`。native OAuth は今回の公式資料で確立していないため、下記の無効状態の bridge テンプレートと導入条件を用意します。[公式](https://roocodeinc.github.io/Roo-Code/features/mcp/using-mcp-in-roo/) |

共通 Agent Plugins は、ルート `plugin.json` と `mcp.json` の同じ版の schema 宣言、
`skills/<name>/SKILL.md` を使います。互換 manifest の単純なファイル名変更ではありません。
Claude 用と Gemini 用はそれぞれの形式を維持します。goose の skills プラグインを入れただけで
MCP extension も登録されたとは判断しません。

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
| Gemini Enterprise | agent/task の指示にカードを取り込む | 管理画面の exact callback と固定 confidential client の事前登録。CLI extension とは別経路。[公式](https://docs.cloud.google.com/gemini/enterprise/docs/connectors/custom-mcp-server/set-up-custom-mcp-server) |
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
| n8n | AI Agent の指示と MCP Client Tool の Bearer/Header credential。導入版の Streamable HTTP 対応を確認。[公式](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp) |
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
  配布物はPAT発行やサーバー設定変更を行いません。利用環境の管理者に、
  PATの有効化と許可scopeを確認してください。
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
