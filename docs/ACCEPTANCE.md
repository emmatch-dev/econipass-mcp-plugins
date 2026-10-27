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
2026-10-27のClaude hosted追加観測1を加え、限定確認12と記録します。既存EMSスキルをv3からv4へ一回置換し、他6スキルの実ダウンロードと現在状態も確認しました。このスキル取込の試行では、新OAuth・remote MCP・実モデル・業務更新は0です。
環境条件未解消2（Linux Codex、QueryPie/Aru）は新候補未ロードです。残り15は新候補未実施で、ChatGPT保留1を含みます。
Rooの旧候補での失敗とMCP無効の別診断、Claude hostedの旧候補でのスキル取込は履歴に残し、今回の新候補受入へ継承しません。

Claude Webの取得ZIPには`skills/` prefixとhost生成の`.claude-plugin/plugin.json`が加わります。7スキルの元source全20エントリを個別に照合し、ZIP全体のbyte一致は主張しません。独立レビューは指摘0です。確認範囲はWebのスキル保存・読戻しで、Desktop／mobile／Coworkや認証済み業務受入は未確認です。

同日の既存DEVコネクタ画面では271件（interactive15／readonly129／write-delete127）と追加EMS17操作のタイトルを確認しました。権限変更・新OAuth・tool実行は0です。これはUIタイトルの可視性に限る確認で、schema・業務実行・最大273件の照合を示しません。

その後の既存Claude Web接続では、ToolSearchに`delivery_mode`（省略可、`metadata|embedded`、既定`metadata`）が露出しました。EMS XLSX（SIMPLE_KWH）と、同じ会話で確認済みの対象に対するCFP masterを、明示的な`metadata`で各1回取得しました。metadataは会話で利用でき、両応答の`server_fetched=true`、`file_embedded=false`、`client_receipt_confirmed=false`、`resource_uri=null`とXLSX MIMEを確認しました。
通常MCP呼出しは計2、model promptは計3、新OAuth・業務更新・embedded・業務ファイル保存・自動再試行は0です。これは新しいschemaと明示modeでのmetadata受領の改善で、ファイル本体の受領や保存を示しません。既に数えたClaude hostedを二重加算せず、限定12・総合0／29を維持します。この受入はsource38adに限定し、20fや後続DEVへ継承しません。
以前のroot側接続宣言では`delivery_mode`が未露出でしたが、このClaude接続の実schemaは別の観測です。全hostでの露出や全273件のschema検証へ拡張しません。公開記録は許可した非機密項目だけとし、地理・顧客識別子・値・ファイル名・サイズ・digest・生の画面画像は含めません。

## 現在のDEVと残る配備

DEV source20fは[通常配備run40425777373](https://github.com/emmatch-dev/econipass-backend/actions/runs/40425777373)のattempt1で14 job成功、配備・外部検証・finalizeが完了しました。必須jobはdeploy121934023314、external verify121935546910、finalize121935678645で、finalizeは2026-10-27T00:34:31Zに終了しました。
新しい[連動Kong40427278443](https://github.com/emmatch-dev/econipass-backend/actions/runs/40427278443)はsource20f・attempt1で失敗しました。job121936295410のstep12で「Kong TLS certificateは失効済み、または7日以内に失効します。」を実行時に確認し、新resource作成・Kong切替へ未到達です。後続step13〜18のsnapshot・切替・capsuleはskip、step19〜23のtail cleanupは成功しました。push起点40425667397のskipやtail cleanupの成功をrollout成功へ読み替えず、完全なrolloutは未完了です。
以前の38adでは[通常配備40285257680](https://github.com/emmatch-dev/econipass-backend/actions/runs/40285257680)が成功し、[連動Kong40290693074](https://github.com/emmatch-dev/econipass-backend/actions/runs/40290693074)は候補証明書の残存7日条件で停止しました。この履歴を新runの結論へ継承しません。
公開中のAPI証明書は2027-01-01まで有効です。Secretの候補とpublic leafの同一性は未確認です。共有TLSの隔離済み旧更新経路を再開せず、適格な証明書ペアを待ちます。
repository-levelの候補証明書ペアは更新metadataが2026-08-16のままです。既存DEV 2台へのSSHは各1回timeoutとなり、接続経路の確認が残っています。証明書・秘密鍵の読取やhost変更は行っていません。
TLS metadata読取の追加案v2はprotected 2ファイルの人間承認待ちで、共有sourceへ未適用です。

配布物生成source dd389と現在のDEV source20fはapp／MCP sourceが同じです。対応表14ファイルもGit source bytesの一致を確認し、通常DEV配備の受入を別に束縛しました。
サーバー2箇所の説明修正に必要な監査3ファイルは、利用者の明示承認後に適用しました。protected validatorは60778、対応する監査文書状態も適用済みです。[PR #1806](https://github.com/emmatch-dev/econipass-backend/pull/1806)はhead88ccの7 CI成功を経て2026-10-26T23:41:57Zにmergeし、sourceは`20f4bd2ecd3dc3bd4cb27c8feb8d31192882599e`です。
ff0b・梱包入力33ファイル・公開38資産は変更していません。[統合CI40421511292](https://github.com/emmatch-dev/econipass-backend/actions/runs/40421511292)の全7 jobと[image build40421511490](https://github.com/emmatch-dev/econipass-backend/actions/runs/40421511490)の非skip 9 jobは成功し、通常DEV配備source20fにサーバー説明修正を含みます。
配備後の既存Claude画面の読取は、ブラウザー制御がWork設定で無効のため停止しました。EcoNiPassツールも現セッションでは利用できず、20fの認証済みUATは未実施です。別UI経路の迂回・再試行や配備後のmodel／MCP呼出しは0で、以前の38adのmetadata受領を20fへ継承しません。

以前のsource38adの公開API／MCP／OAuth metadata／CORSの契約検証は成功しました。20fの配備後認証済みUATへ継承しません。
既存接続で組織・対象月・EMS取込一覧を確認し、CFP5種・EMS CSV/XLSXのサーバー取得とmetadata応答が成功しました。今回の7件で500は観測していません。
この7件は以前のroot側接続での観測です。当時の`delivery_mode`入力は未露出で、embedded受信・業務ファイル保存・投入・置換は0でした。今回選んだ事業所は新しい認可済み一覧の直接所属先であり、旧記録とのデータ比較は行っていません。後続のClaude Web 2件のmetadata受領とは分けて記録します。
顧客ID・名称・値・ファイル・顧客ファイルdigest・資格情報は公開しません。

LICENSE適用・新OAuth・ChatGPT受入は保留、公式ディレクトリ掲載とSTG/PRD配備は未完了です。
[以前のa113時点の記録](https://github.com/emmatch-dev/econipass-mcp-plugins/blob/661361786a2202ca256cced6e044255615b2438e/docs/ACCEPTANCE.md)と[機械可読の記録](acceptance-summary.json)を参照してください。
