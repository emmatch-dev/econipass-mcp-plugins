# DEV 1.2.0候補の受入・公式掲載状況

確認日: 2026-10-26 JST。CFP・EMSファイル受信互換性と依存修正後の候補です。
実装ソースは`275a21cda3b89ebadaf722b3eadff55e9e2e8775`、metadata commitは`0a04e8ee6d1cdee7eb2f50f490d0190769a43cdb`。
**未配備・未公開で、認証済み総合受入は0／29です。**

通常239／共有法定帳票252／最大254／固定PRD参照30を7スキルへ対応付けます。
対応表SHA-256は`ec2295c64c3781032cb684b367dab521d8781c4d037aae34d6b3da347c8701ad`、release.jsonは
`6cc85e69298ea6c983ab8036f64681ed4223312c417f197728403ebec76f5647`です。新規候補は37 ZIP・999エントリ・14ソース束縛です。
更新中の公開原本common30ファイルと候補が一致し、公開matrix／adapter＋275a固定builder／SDK入力から
全37 ZIP・999エントリを再生成してbyte一致を確認しました。公開Gitの旧834commitとの一致や
公開済みを主張するものではありません。新候補のnative13限定試験は完了し、旧成功継承は0です。

[配布候補のhash](../candidate-package-v1.2.0-cfp-ems-security-license-held-20261025.json)と[機械可読記録](acceptance-summary-v1.2.0-candidate-275a-6cc85-20261026.json)を正本とします。
旧928673監査は承認後7f631へ反映済みです。今回の監査差分SHA `0a691b47…`も
2026-10-26に利用者が承認し、`10f599241e4c791d6a9b58a2295957d1c53c82f0`へ反映しました。
通常DEV配備の承認は、LICENSE適用・新OAuth・ChatGPT受入や公式規約への同意を変更しません。
監査反映後`10f59924`のCIは実行中です。DEV配備・公開も未完了で、旧sourceの成功は継承しません。

## CFP・EMSで実機から判明した問題と修正

既存DEVのClaude接続で、CFPは2,150,326bytes、EMSテンプレートは76,117bytesの
XLSX情報がUIに表示されても、モデルはXLSX resource非対応の1行だけを受け取りました。
HTTP 500は観測せず、ファイル本体の受領・保存・投入の成功には数えていません。

CFP取得とEMSの11ファイルdownload/export照会は`delivery_mode="metadata"`を既定とし、
同じ小さなJSONをTextContentとstructured contentへ返します。本体は同梱せずURIはnullです。
対応host／SDKのみ明示的に`delivery_mode="embedded"`を選び、元のbytes・サイズ・SHA-256と
保存結果を確認します。サーバー取得・本体同梱・クライアント受領を分け、応答の受領確認はfalseです。
EMSのnative認可・監査・書込・HTTP契約・32MiB上限を維持し、内部署名URLや新endpointは公開しません。

CFPの本人画面はCFP算定→データ入力→Excel入力画面の製品別入力フォーマットです。
確認済みはマスタ・原単位・活動量・CFP認証期間の4種で、AIST-IDEAの経路は未確認です。
EMSの画面経路は未確認のため案内を作らず、対応クライアントで実ファイルを受け取ります。
metadataだけで保存・投入・置換・保持・業務受入を完了扱いにしません。

## 検証と29環境の範囲

新sourceのローカルEMS影響2suiteは旧FastMCP3.4.7で496件成功しました。
合成2,315,740bytes／最大200文字の非ASCII名でも通常textは最大1,350 UTF8bytesでした。
これはLinux3.4.10・実SDKファイル保存・認証済み業務受入とは別です。
旧5ee候補のLinux全suite5,225件成功／6skip（plugins55件を含む）とE2E58シナリオ／239toolは
[旧候補の履歴](acceptance-summary-v1.2.0-candidate-5ee-5c4-20261025.json)へ分離し、新sourceへ継承しません。

新候補で13環境の限定native試験を新規実行し、16環境は未試験です。旧成功継承は0です。
公開版の部分確認と認証済み総合受入は0／29のままです。
[今回の限定試験記録](../candidate-native-load-v1.2.0-cfp-ems-security-license-held-20261025.json)は、source275a・実行時HEAD72e・release6cc85・14ソースへ束縛しています。
Macの8 CLI＋4 SDKで31操作と拒否probe1件、Linux Codexのinstall2操作・metadata RPC3件を確認しました。

| 限定試験の範囲 | 環境数 |
| --- | --- |
| CLIでのmanifest・プラグイン・metadata読込（CodexはLinux CLIのみ） | 4 |
| CLIでのMCP設定のみ（Cursor／VS Code） | 2 |
| 設定とスキル読込（Goose／Cline） | 2 |
| スキルmetadataのみ（Roo） | 1 |
| SDKの合成オフラインfixture | 4 |

新OAuth・remote MCP・実モデル呼出・顧客業務操作はすべて0です。
この13試験はremote CFP／EMS取得、実ファイル保存、認証済みcatalogや新security runtimeの受入を含みません。
275aのLinux影響試験は初回1,401成功／11失敗でした。11操作の新しい引数delivery_modeが
既存parity期待値に含まれていなかったため、72eで試験9行のみを厳密に補正しました。
そのmoduleはMac・Linux各170件、Linuxの文書検査42件が成功（skip0）しました。
固定30監査116件・plugins55件（再現性3件を含む）は初回成功群に含まれます。
全1,412件を再実行して成功したとは記録せず、失敗した初回と補正後の再検証を分離しています。
CI条件lint・actionlint・27workflowのYAML・diff検査も成功しました。
275aのtool-only E2Eは239tool（237成功・対象不在の想定拒否2・失敗0）で、ローカルの
PostgreSQL／Redisと合成AS/APIのみです。実grant・remote MCPは使わず、認証58シナリオは再実行していません。
旧5eeの全suite・E2E58・本番image smokeを275aへ継承せず、275aの全suite／本番image成功は主張しません。
新規MCP OAuth、ChatGPT受入、LICENSE適用は利用者指示で保留しています。
ライセンスはHELDでLICENSE0件、旧MIT候補の配布・許諾申告は行いません。

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
| Claude | LICENSE適用保留により掲載条件を満たさず未申請。旧5ee候補はmanifestエラー・警告0、directoryはLICENSE_MISSINGのblocking1。今回のEMS修正候補でもmanifestエラー・警告0、directoryはLICENSE_MISSINGのblocking1。限定読込成功を掲載準備完了とは扱わない |

Registryの[認証仕様](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/authentication.mdx)と
[Terms](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/terms-of-service.mdx)を確認します。
GitHub配布、Registry登録、各社の掲載承認は別の結果です。DEV URLを本番URLとして申告せず、審査用認証情報は公開しません。
