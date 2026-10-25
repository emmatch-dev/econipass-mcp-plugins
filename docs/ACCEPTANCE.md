# DEV 1.2.0候補の受入・公式掲載状況

確認日: 2026-10-25 JST。接続先は `https://api.dev.app.econipass.com/mcp`。
**1.2.0はソース・オフライン配布物の検証を終えた候補で、未配備・未公開です。**
最終source commitのCI、通常DEV配備、公開後の照合、認証済み実機受入をそれぞれ確認してから状態を更新します。

## 1.2.0のソースと配布物

| 対象 | 確認結果 |
| --- | --- |
| 4profileのソース登録 | 通常239、共有法定帳票有効252、レビュー有効を含む最大254、PRD参照タグ30 |
| tool→skill対応 | 全254ツールを7スキルへ明示割当。新ツール・廃止ツールを検出すると再生成を停止 |
| ソース束縛 | 対応表の14ソースhashを実ファイルと照合。欠落・追加・重複・escape・symlink・byte不一致を拒否 |
| 既存plugins suite | 55 passed。実登録、source binding、再現可能ZIP、29kit、4API sampleのオフライン起動を確認 |
| skills／lint | 7スキルの検証、black／isort／flake8、diff check成功 |
| 最終生成物 | 共通1＋スキル7＋製品キット29＝37 ZIPを予定。ローカルのMITレビュー候補37件はhash／CRC照合済み。正式配布物はライセンス判断後に確定。旧1.1.0のassetは変更なし |

基点は`8c578bac1ac91bdd2ddf0561e200fb87b64c41c7`、実装ソースcommitは
`9286735044fd4635e11c5022e677d7cc2b7f9691`です。監査メタデータを含む最終リリースcommit、CI、配備SHAは別に確定します。
対応表と`release.json`の`source_binding`は確定したソースbyteを識別しますが、配備やtenant受入は証明しません。
29の製品設定形式、OAuth設定、SDKサンプルのread-only制限を一括変更していません。

追加した8ツールは`update_task`、`get_activity`、`create_activity`、`update_activity`、
`create_activity_comment`、`get_measure_custom_fields`、`get_task_custom_fields`、`get_activity_custom_fields`です。
独自項目の値更新と、定義そのものの作成・変更・削除を区別し、後者は本人ブラウザーに残します。
活動のnullable項目clear、現在状態／ETagと確認tokenの束縛、競合時の再取得をスキルにも記載しました。

## 現在のDEV配備とツール公開数の観測

| 観測 | 結果と限界 |
| --- | --- |
| 既存`8c578bac`のbackend配備 | [run 40171982330](https://github.com/emmatch-dev/econipass-backend/actions/runs/40171982330)成功。2026-10-25 07:53:41 UTCに完了 |
| 同じソースに対応するKong配備 | [run 40174506917](https://github.com/emmatch-dev/econipass-backend/actions/runs/40174506917)成功。07:57:42 UTCに完了。上流manual runの対応、公開検証・finalizeを確認 |
| Claude Webの既存接続UI | 07:53:26 UTCに244ツール＝interactive 15＋参照119＋更新110。CSV transaction・報告再生成・site validityの3表示名を確認 |
| 1.2.0候補の新操作・修正 | 上記の既存配備には含まれない。候補の配備と認証済み操作試験は未実施 |

backend／Kongは既存の通常DEV暫定repository-runner経路です。protected brokerへの切替やPRD／STG配備は主張しません。
Claude UIの観測は既存ログインの画面確認だけで、新規OAuth認可・権限変更・業務呼出しはありません。
UIで稼働SHAを読み戻しておらず、244件を特定sourceのraw `tools/list`結果とみなしません。
認証済みcatalogの全ページと、各clientの表示・実行結果を配備ソースへ照合する作業が残っています。

## 29環境の受入範囲

公開版としての1.2.0は**部分確認0／29、総合受入完了0／29**です。
別に、未公開のレビュー候補では13製品の限定確認を行いました。6製品は最終候補で再実行し、
7製品はZIPの全byte一致を条件に独立レビュー済みの試験を参照しています。
[候補の記録](candidate-native-load-v1.2.0-20261025.json)にはnative package、metadata、設定、SDKの段階を区別しています。
Codexの導入確認はLinux CLIだけで、Mac Desktop／IDEの受入へ転記していません。
この候補のMIT案は承認前であり、認証済みremote MCP・業務書込みの受入も未実施です。
全29製品の生成・構造検証はパッケージ検証であり、その製品によるnative読み込みや実接続ではありません。
各製品・surfaceの結果は[機械可読記録](acceptance-summary.json)へ個別に記録します。

10月21日の1.1.0には部分確認14／29、総合完了0／29の記録があります。
[詳細履歴](history/ACCEPTANCE-v1.1.0-20261021.md)と[旧JSON](history/acceptance-summary-v1.1.0-20261021.json)を保存し、
新版に読み込み済み・接続済みとして転記していません。Desktop／CLI／IDE／Web／mobile／cloudの結果も相互に流用しません。

総合受入では、各製品の配布・認証profileに従い、7スキル、指示カード、またはSDK contextと設定の実際の取り込みを確認します。
認証済みcatalogと参照、scope／事業所拒否、OAuth更新またはPAT rotation・専用grantの失効も対象です。
更新を公開する構成ではpreview／確認／1回実行／readback／token再利用拒否、CFPを公開する構成では
5ファイルの受領、投入・置換、サイズ制限、既存データ保持を専用fixtureで確認します。
参照専用profileでは更新を実行せず、非公開操作の除外と更新要求の拒否を確認します。
既存利用者のgrantを失効させたり、顧客データを置換したりして試験を成立させません。

新規MCP OAuth接続とChatGPTの受入は利用者の指示で保留中です。
既存接続の確認と、新しい継続アクセスの認可を区別して進めます。

## CFPの500修正と取得・投入の境界

旧稼働版`37284f6`と診断版`94ae94f`で発生した500は、一時領域の権限修正後の
`fde1cffb`で2026-10-21 01:25–01:26 UTCに再試験し、5種類のExcel取得に成功しました。
修正版の[backend配備](https://github.com/emmatch-dev/econipass-backend/actions/runs/39525015891)と
[Kong配備](https://github.com/emmatch-dev/econipass-backend/actions/runs/39526711825)も成功しています。

受領したのはmaster／base_unit／activity_amount／pcf_certification_period／aist_ideaです。
MIME、サイズ一致、ZIPヘッダーと必須OPCパーツを確認しました。CRC実体・XML・セル内容は当時のlive試験では未検証です。
raw HTTP transport statusは観測せず、実ファイルを受領した成功応答を根拠にしています。
顧客ID・名前・ファイル本文・内容hashは公開記録に保存していません。

この過去結果は1.2.0の再試験でも、投入・置換・既存データ保持の受入でもありません。
同じユーザーの業務データを再投入して成功扱いにせず、専用fixtureで残る操作を確認します。

## 公式ディレクトリ

| 公開先 | 状況 |
| --- | --- |
| GitHub公開リポジトリ・Release | DEV 1.1.0公開済み。1.2.0は候補の更新・公開準備中 |
| MCP公式Registry | DEV専用`io.github.emmatch-dev/econipass-dev`の`1.2.0-dev.1` manifest案を公式mcp-publisher 1.8.1で検証し、valid応答を確認。登録・公開は未実施 |
| OpenAI公式ディレクトリ | 2026-10-25に認証済みポータルで確認。公開者の本人・法人確認が必要なため、ZIP下書きの作成前で停止。審査・掲載は未完了 |
| Claudeディレクトリ | 2026-10-25に既存ログインのポータルで申請0件を確認。公開mainの1.1.0事前検査は7項目中6成功、LICENSE不足1件で停止。icon・privacy URLの警告は1.2.0候補へ対応し、CLI strict検証は警告0。ライセンス確定・公開後のポータル再検査・申請は未完了 |

GitHub配布、MCP Registry登録、各社の審査承認は別の結果として記録します。
DEV URLを本番URLとして申告せず、審査用秘密情報や認証情報を公開リポジトリへ保存しません。
申請手順は[公開手順](../plugins/PUBLISHING.md)に記録しています。
