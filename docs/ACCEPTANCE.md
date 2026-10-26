# v1.2.0 クライアントDEV previewの受入

この版は7スキル・29環境向けのクライアント配布物です。公開状態は[GitHub Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)で確認してください。総合受入は0／29です。

生成sourceは`dd389bd50ba75a280dedb207b75c52434a6a5b5a`、release SHAは`ff0b309c334bb2878ae5585e0de15d90ae96833eb9ce8f5d02d96f5507d4dbef`です。
37 ZIP・1,016エントリのCRC・SHA・安全パス・LICENSE/PDF混入0を確認しました。公開後匿名取得は別の検証です。

## 新候補の限定確認

| 分類 | 確認結果 |
| --- | --- |
| Claude Code／Gemini CLI／Copilot CLI | 7スキルとMCP設定のネイティブ認識。15 metadata操作成功 |
| Goose／Cline | 7スキルとMCP設定のネイティブ読取。6 metadata操作成功 |
| Cursor／保持済みVS Code | 隔離profileへのMCP設定保存と読戻し。4 metadata操作成功。スキル本文の認識・IDE業務操作は未確認 |
| OpenAI Responses／Anthropic Messages／OpenAI Agents SDK／LangChain-LangGraph | 実SDKを使う4つのローカル合成fixtureが成功。実モデル・remote MCPは未実行 |

CLI7環境25操作とSDK4環境の合成fixtureを限定確認11と記録します。ネットワーク・Keychain・既存ユーザー設定を隔離し、新OAuth・実モデル・業務更新は0です。
環境条件未解消2（Linux Codex、QueryPie/Aru）は新候補未ロードです。残り16は新候補未実施で、ChatGPT保留1を含みます。
Rooの旧候補での失敗とMCP無効の別診断、Claude hostedの旧スキル取込は履歴に残し、新候補の受入へ加算しません。

## 現在のDEVと残る配備

DEV backend38adは[通常配備・外部検証・finalize](https://github.com/emmatch-dev/econipass-backend/actions/runs/40285257680)に成功しました。
[連動Kong40290693074](https://github.com/emmatch-dev/econipass-backend/actions/runs/40290693074)は、GitHub Secretから渡る候補証明書が残存7日の条件を満たさず停止しています。新Kong resource作成と切替は未到達で、完全なrolloutは未完了です。
公開中のAPI証明書は2027-01-01まで有効です。Secretの候補とpublic leafの同一性は未確認です。共有TLSの隔離済み旧更新経路を再開せず、適格な証明書ペアを待ちます。

配布物生成source dd389とbackend38adは、MCPのdocstringを除くAST・引数・tool名が一致しています。
サーバー2箇所の説明修正は監査3ファイルの人間承認・CI・配備が残っています。対応表14ソースのbyte一致やserved説明の更新を主張しません。

現在の公開API／MCP／OAuth metadata／CORSの契約検証は成功しました。
既存接続で組織・対象月・EMS取込一覧を確認し、CFP5種・EMS CSV/XLSXのサーバー取得とmetadata応答が成功しました。今回の7件で500は観測していません。
接続のdelivery_mode入力は未露出のため、embedded受信・ファイル保存・投入・置換は0です。今回選んだ事業所は新しい認可済み一覧の直接所属先であり、旧記録とのデータ比較は行っていません。
顧客ID・名称・値・ファイル・顧客ファイルdigest・資格情報は公開しません。

LICENSE適用・新OAuth・ChatGPT受入は保留、公式ディレクトリ掲載とSTG/PRD配備は未完了です。
[以前のa113時点の記録](https://github.com/emmatch-dev/econipass-mcp-plugins/blob/661361786a2202ca256cced6e044255615b2438e/docs/ACCEPTANCE.md)と[機械可読の記録](acceptance-summary.json)を参照してください。
