# v1.2.0 クライアントDEV previewの受入

> [v1.2.0のクライアントDEV preview](https://github.com/emmatch-dev/econipass-mcp-plugins/releases/tag/econipass-mcp-plugin-v1.2.0)をprereleaseとして公開しました。公開日時は2026-10-27 07:18:52 JST（2026-10-26T22:18:52Z）です。Authorization headerなしの匿名GETで38資産のSHA・sizeと37 ZIP・1,016エントリのCRC、LICENSE混入0を確認しました。旧v1.1.0のtag・資産は保持しています。
>
> 公開tagは公開時の原本`df81a01051bb662cef1c4af87b181b087f05e9ed`に固定します。この追加観測を反映するmainの更新対象は文書5件だけで、梱包入力33ファイルと38公開資産を変更しません。配布物の生成source dd389と、この公開tag・後続の文書更新を区別します。

この版は7スキル・29環境向けのクライアント配布物です。公開状態は[GitHub Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)で確認してください。総合受入は0／29です。

生成sourceは`dd389bd50ba75a280dedb207b75c52434a6a5b5a`、release SHAは`ff0b309c334bb2878ae5585e0de15d90ae96833eb9ce8f5d02d96f5507d4dbef`です。
37 ZIP・1,016エントリのCRC・SHA・安全パス・LICENSE/PDF混入0を確認しました。公開後の匿名取得でも38資産のSHA・sizeと37 ZIP・1,016エントリのCRC、LICENSE混入0が一致しました。

## 新候補の限定確認

| 分類 | 確認結果 |
| --- | --- |
| Claude Code／Gemini CLI／Copilot CLI | 7スキルとMCP設定のネイティブ認識。15 metadata操作成功 |
| Goose／Cline | 7スキルとMCP設定のネイティブ読取。6 metadata操作成功 |
| Cursor／保持済みVS Code | 隔離profileへのMCP設定保存と読戻し。4 metadata操作成功。スキル本文の認識・IDE業務操作は未確認 |
| OpenAI Responses／Anthropic Messages／OpenAI Agents SDK／LangChain-LangGraph | 実SDKを使う4つのローカル合成fixtureが成功。実モデル・remote MCPは未実行 |
| Claude hosted（Web） | 2026-10-27、7スキルの実ダウンロードで元source全20エントリが候補と一致。EMS v4の保存後再読込・有効状態、他6スキルのv2・有効状態を確認 |

CLI7環境25操作とSDK4環境の合成fixtureは、ネットワーク・Keychain・既存ユーザー設定を隔離した限定確認11です。
2026-10-27のClaude hosted追加観測1を加え、限定確認12と記録します。今回は既存EMSスキルをv3からv4へ一回置換し、他6スキルの実ダウンロードと現在状態も確認しました。新OAuth・remote MCP・実モデル・業務更新は0です。
環境条件未解消2（Linux Codex、QueryPie/Aru）は新候補未ロードです。残り15は新候補未実施で、ChatGPT保留1を含みます。
Rooの旧候補での失敗とMCP無効の別診断、Claude hostedの旧候補でのスキル取込は履歴に残し、今回の新候補受入へ継承しません。

Claude Webの取得ZIPには`skills/` prefixとhost生成の`.claude-plugin/plugin.json`が加わります。7スキルの元source全20エントリを個別に照合し、ZIP全体のbyte一致は主張しません。独立レビューは指摘0です。確認範囲はWebのスキル保存・読戻しで、Desktop／mobile／Coworkや認証済み業務受入は未確認です。

同日の既存DEVコネクタ画面では271件（interactive15／readonly129／write-delete127）と追加EMS17操作のタイトルを確認しました。権限変更・新OAuth・tool実行は0です。これはUIタイトルの可視性に限る確認で、schema・業務実行・最大273件の照合を示しません。

## 現在のDEVと残る配備

DEV backend38adは[通常配備・外部検証・finalize](https://github.com/emmatch-dev/econipass-backend/actions/runs/40285257680)に成功しました。
[連動Kong40290693074](https://github.com/emmatch-dev/econipass-backend/actions/runs/40290693074)は、GitHub Secretから渡る候補証明書が残存7日の条件を満たさず停止しています。新Kong resource作成と切替は未到達で、完全なrolloutは未完了です。
公開中のAPI証明書は2027-01-01まで有効です。Secretの候補とpublic leafの同一性は未確認です。共有TLSの隔離済み旧更新経路を再開せず、適格な証明書ペアを待ちます。

配布物生成source dd389とbackend38adは、MCPのdocstringを除くAST・引数・tool名が一致しています。
サーバー2箇所の説明修正は監査3ファイルの人間承認・CI・配備が残っています。対応表14ソースのbyte一致やserved説明の更新を主張しません。

現在の公開API／MCP／OAuth metadata／CORSの契約検証は成功しました。
既存接続で組織・対象月・EMS取込一覧を確認し、CFP5種・EMS CSV/XLSXのサーバー取得とmetadata応答が成功しました。今回の7件で500は観測していません。
この既存MCP接続のdelivery_mode入力は未露出のため、embedded受信・業務ファイル保存・投入・置換は0です。今回選んだ事業所は新しい認可済み一覧の直接所属先であり、旧記録とのデータ比較は行っていません。
顧客ID・名称・値・ファイル・顧客ファイルdigest・資格情報は公開しません。

LICENSE適用・新OAuth・ChatGPT受入は保留、公式ディレクトリ掲載とSTG/PRD配備は未完了です。
[以前のa113時点の記録](https://github.com/emmatch-dev/econipass-mcp-plugins/blob/661361786a2202ca256cced6e044255615b2438e/docs/ACCEPTANCE.md)と[機械可読の記録](acceptance-summary.json)を参照してください。
