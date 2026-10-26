# DEV 1.2.0候補の受入・公式掲載状況

確認日: 2026-10-25 JST。接続先は `https://api.dev.app.econipass.com/mcp`。
**CFP受信互換性・依存修正後の1.2.0候補を検証中です。未配備・未公開で、総合受入は0／29です。**

## 現在のソースと配布物

実装ソースは `5ee1435c84bbc6761c7a7041d4b62b8568e87576`、プラグイン対応表・説明のcommitは
`e54eb669130a349d6c24ef894d55ba4eb7cb92be`。最終CIと配備SHAはまだ確定していません。

| 対象 | 現在の結果と範囲 |
| --- | --- |
| ソース登録 | FastMCP 3.4.10のLinux実登録で通常239／共有法定帳票252／最大254／固定PRD参照30 |
| tool→skill | 254ツールを7スキルへ明示割当。14ソースのbyte hashと4profileを照合 |
| 対応表 | SHA-256 `bf7ad8d50fdff1910797f9896cbfc173451acdea9aef6d761a4e48455bd7837e` |
| 配布候補 | 7スキル・29キット・37 ZIP、999エントリ。全ZIPのhash／CRC・14ソース束縛を確認 |
| 更新中の公開原本との一致 | common30ファイルは候補と完全一致。現公開原本・matrix／adapterと、e54固定のbuilder／SDKサンプル入力から再生成した全37 ZIP・999エントリも一致。公開Gitの旧834commitとの一致や公開済みは主張しない |
| release.json | SHA-256 `5c4c9c591aacfce254b36139748f62033e1a0345ad9fc319f7b15d53d68fc033`。未公開 |
| ライセンス | 利用者指示で適用保留。LICENSEは0件、旧MIT候補は採用しない |
| 新runtime検証 | 独立OAuth21件成功、変換後toolの認可拒否を確認。本番Dockerfileのローカルimage起動・合成CFP応答は成功。全MCP suite・E2Eは進行中で、実OAuth／tenant受入は未実施 |
| CI／DEV | 新sourceのCI・配備は未実施。既承認の旧監査差分は反映済みで、新sourceの監査提案は別に検証中 |

[配布物とhashの記録](../candidate-package-v1.2.0-cfp-security-license-held-20261025.json)と
[機械可読の受入記録](acceptance-summary-v1.2.0-candidate-5ee-5c4-20261025.json)を正本とします。配布物の構造・生成は実接続の受入ではありません。

追加した8ツールは`update_task`、`get_activity`、`create_activity`、`update_activity`、
`create_activity_comment`、`get_measure_custom_fields`、`get_task_custom_fields`、`get_activity_custom_fields`です。
独自項目の値更新と定義そのもののCRUDを区別し、後者は本人ブラウザーに残します。
現在状態／ETagと確認tokenの束縛、nullable活動項目のclear、競合時の再取得を維持します。

## CFPで実機から判明した問題と修正

既存DEVのClaude接続で、事業所参照とCFP master取得を読み取りだけで確認しました。
サーバー側の応答には約2.15 MBのXLSXメタデータが表示されましたが、モデルには
XLSX resource非対応のメッセージだけが届きました。これはHTTP 500の観測ではありません。
ファイル本文の受領・保存、投入、置換、既存データ保持の成功には数えていません。

新候補では`download_cfp_input_template`の既定を`delivery_mode="metadata"`とし、
ファイル名・サイズ・hashと返却状態を同じ小さなJSON text／structured contentへ返します。
ファイル本体は同梱せず、resource URIはnullです。本人のCFP算定→データ入力→Excel入力画面で
別途取得する手順を示します。観測した正規画面はマスタ・原単位・活動量・CFP認証期間の4種で、
AIST-IDEAの画面経路は未確認です。別取得したファイルを同じsnapshotと推定しません。

XLSX resourceを受信できるhost／SDKだけが明示的に`delivery_mode="embedded"`を選び、
実際のbytes・サイズ・hashと保存結果を確認します。サーバー取得と本体同梱はクライアント受領の証明ではありません。
Base64のtext化、公開リンク、新OAuth、通常認証やIP検査の迂回は追加していません。
CFPのupload処理と出力schema、32 MiBの取得上限、native認可と上流エラー分類は維持しています。

旧3.4.7環境ではCFP／Workbook113件・関連境界207件、独立60ケースを確認しました。
これは新3.4.10での全試験へ継承せず、別に検証します。依存はFastMCP／slim 3.4.10と
opentelemetry-api 1.45.1へ固定し、[公式の認可修正](https://github.com/PrefectHQ/fastmcp/releases/tag/v3.4.10)を含めています。

## 29環境の受入範囲

公開版としての部分確認は0／29、認証済み総合受入も0／29です。
今回の37 ZIPで13製品の限定native試験を新たに実行しました。新規13件、過去の成功継承0件です。
[今回の記録](../candidate-native-load-v1.2.0-cfp-security-license-held-20261025.json)には
全29行の状態、元証跡hash、各ZIPと14ソースの束縛、更新中の公開原本との照合結果を収録しています。
設定・metadata・スキル読込と合成SDK fixtureは、実認証・業務操作・Desktop／IDE／Webの受入と区別します。
この13件はremote CFPの実取得や新しいMCP security runtimeを呼び出した試験ではありません。

| 限定的に確認した段階 | 対象 |
| --- | --- |
| native package／manifest／metadata | Codex Linux arm64 CLI、Claude Code、Copilot CLI、Gemini CLIの4製品 |
| CLIのMCP設定のみ | Cursor、VS Codeの2製品 |
| 設定と7スキルの読み込み | Goose、Clineの2製品 |
| スキルmetadataのみ | Roo Codeの1製品 |
| 合成fixtureでのSDK検証 | OpenAI Responses／Agents、Anthropic Messages、LangChain／LangGraphの4製品 |

Codexの証跡をMac Desktop／IDEへ転記せず、旧候補の13件も今回の成功として継承しません。
全37 ZIP・999エントリの再生成一致は、公開Gitにすべての生成済みエントリが直接あることを意味しません。
公開原本と、公開Gitへ収録していない固定builder／配布SDKサンプルを区別して由来を記録しています。

総合受入には、実catalog、参照、事業所／scope拒否、専用grantの更新・失効を含めます。
更新公開時はpreview・確認・1回実行・readback・token再利用拒否、CFP公開時は実ファイル受領と
専用fixtureでの投入・置換・保持を確認します。既存利用者のgrantや既存の業務データを試験のために失わせません。
新規MCP OAuth、ChatGPT受入、配布LICENSE適用は利用者の指示で保留しています。

## 既存DEVと過去の証跡

既存`8c578bac`の[backend配備](https://github.com/emmatch-dev/econipass-backend/actions/runs/40171982330)と
[Kong配備](https://github.com/emmatch-dev/econipass-backend/actions/runs/40174506917)は成功しましたが、今回の候補は含みません。
既存Claude UIの244ツール（interactive15・参照119・更新110）はraw全ページの`tools/list`や稼働SHAの証明ではありません。

以前のCFP共通500は一時領域の権限修正後の`fde1cffb`で、2026-10-21に5種類の取得を確認しました。
[backend](https://github.com/emmatch-dev/econipass-backend/actions/runs/39525015891)／
[Kong](https://github.com/emmatch-dev/econipass-backend/actions/runs/39526711825)の配備結果も過去のものです。
当時はMIME・サイズ・基本OPC構造を確認し、CRC実体・セル内容、投入・置換は未検証でした。

[旧5909候補の状況](ACCEPTANCE-v1.2.0-candidate-5909-20261025.md)、
[旧LICENSE非同梱13試験](../candidate-native-load-v1.2.0-license-held-20261025.json)、
[旧MIT候補13試験](../candidate-native-load-v1.2.0-20261025.json)、
[1.1.0の履歴](ACCEPTANCE-v1.1.0-20261021.md)はそれぞれ保存し、今回へ継承していません。

## 公式掲載

| 公開先 | 状況 |
| --- | --- |
| GitHub | DEV 1.1.0公開済み、1.2.0は未公開 |
| MCP Registry | namespace未登録。remote-only案はsoftware LICENSE不要だが、metadataのCC0許諾を含むTermsへの同意は未実施。組織namespace用の認証も未設定 |
| OpenAI | 公開者の本人・法人確認がZIPアップロード前に必要。未申請 |
| Claude | LICENSE適用保留により掲載条件を満たさず未申請。新候補のCLIでもmanifestエラー・警告0、directoryはLICENSE_MISSINGのblocking1。限定読込成功を掲載準備完了とは扱わない |

Registryの[認証仕様](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/authentication.mdx)と
[Terms](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/terms-of-service.mdx)を確認します。
GitHub配布、Registry登録、各社の掲載承認は別の結果です。DEV URLを本番URLとして申告せず、審査用認証情報は公開しません。
