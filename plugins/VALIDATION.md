> [v1.2.0のクライアントDEV preview](https://github.com/emmatch-dev/econipass-mcp-plugins/releases/tag/econipass-mcp-plugin-v1.2.0)をprereleaseとして公開しました。公開日時は2026-10-27 07:18:52 JST（2026-10-26T22:18:52Z）です。Authorization headerなしの匿名GETで38資産のSHA・sizeと37 ZIP・1,016エントリのCRC、LICENSE混入0を確認しました。旧v1.1.0のtag・資産は保持しています。
>
> 公開tagは公開時の原本`df81a01051bb662cef1c4af87b181b087f05e9ed`に固定します。この追加観測を反映するmainの更新対象は文書5件だけで、梱包入力33ファイルと38公開資産を変更しません。配布物の生成source dd389と、この公開tag・後続の文書更新を区別します。
>
> 公開済み配布物はff0bのクライアントDEV previewです。生成source dd389、37 ZIP＋release.json、EMS17操作追加と最大273のソース登録を保持します。65テスト・7スキル検査・CLI7環境25 metadata・SDK4合成fixtureが成功しています。
>
> Claude Webでは7スキルの実ダウンロードで元source全20エントリが候補と一致し、EMS v4の保存後再読込・有効状態と他6スキルのv2・有効状態を確認しました。限定確認12（CLI7＋SDK合成4＋Claude hosted1）・環境条件未解消2・未実施15・総合受入0/29です。このスキル保存・読戻しだけでは、ZIP全体のbyte一致やremote MCP・業務実行の受入を主張しません。
>
> 先の既存DEVコネクタ画面確認は271件とEMS17操作タイトルの可視性に限る観測です。後続のClaude Web接続では`delivery_mode`が露出し、EMS XLSXとCFP masterを明示`metadata`で各1回取得しました。metadataは会話に届き、server取得true・本体同梱false・clientファイル受領false・resource URI nullを確認しました。通常MCP呼出し計2・model prompt計3、新OAuth・業務更新・embedded・業務ファイル保存は0です。source38adでの結果に限定し、20fのDEV受入・全hostのschemaや総合受入へ拡張しません。限定12・総合0/29は不変です。
>
> 説明修正に必要な監査3ファイルは利用者承認後に適用し、PR #1806のhead88cc・7 CI成功後、2026-10-26T23:41:57Zにsource20fへmergeしました。app／MCP sourceは生成source dd389と同じで、ff0b・梱包入力33ファイル・公開38資産は不変です。[統合CI40421511292](https://github.com/emmatch-dev/econipass-backend/actions/runs/40421511292)の全7 jobと[image build40421511490](https://github.com/emmatch-dev/econipass-backend/actions/runs/40421511490)の非skip 9 jobは成功しました。[通常DEV40425777373](https://github.com/emmatch-dev/econipass-backend/actions/runs/40425777373)もattempt1・14 job成功で配備・外部検証・finalizeを完了し、2026-10-27T00:34:31Zにfinalizeしました。サーバー説明修正を含む20fと公開候補の14ファイルはGit source bytesが一致しています。配備後の認証済みUATはブラウザー制御無効・EcoNiPassツール利用不可のため未実施で、38adのmetadata受領を継承しません。
>
> 新しい[連動Kong40427278443](https://github.com/emmatch-dev/econipass-backend/actions/runs/40427278443)はsource20f・attempt1で失敗しました。step12の候補TLS証明書の残存7日検査で停止し、新resource作成・Kong切替へ未到達です。後続snapshot・切替・capsuleはskipし、tail cleanupの成功をrollout成功へ読み替えません。旧38adのKong失敗とpush起点40425667397のskipは別の履歴です。候補ペアの更新metadataは2026-08-16のままで、隔離した共有旧更新経路は再開していません。既存DEV 2台へのSSHは各1回timeoutとなり、接続経路の確認が残っています。TLS metadata読取案v2はprotected 2ファイルの人間承認待ち・共有source未適用です。LICENSE・新OAuth・ChatGPT・STG/PRD停止は維持します。現行状態は[受入記録](../docs/ACCEPTANCE.md)、公開状態は[Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)を参照してください。
>
> 以下は以前のsource・候補・準備時点の履歴です。現行候補や現在の配備完了を示すものとして継承しません。

# プラグイン配布物の検証記録

現在の配布先と検証・受入の範囲は[README](../README.md)と[受入記録](../docs/ACCEPTANCE.md)を確認してください。
以下は[a72時点の履歴](https://github.com/emmatch-dev/econipass-mcp-plugins/blob/a72fb24fa8ca97db94091e9452a07d5a69195cbf/plugins/VALIDATION.md)です。「未upload」「未配備」「候補」などは各観測時点の記録で、後続の現在値を示しません。

## a72以前の記録

この文書は **日付検証修正候補の配備・公開前の観測時点（2026-10-26T00:38:56.122704+00:00）の記録** です。旧f831のDraftと新83f9候補を区別します。後続の現行状況は[PR #5](https://github.com/emmatch-dev/econipass-mcp-plugins/pull/5)と[Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)で確認してください。

## 2026-10-26 日付検証修正候補

確認対象commit6f09904b（日付実装e79417e3）、release SHA`83f900b69c53acea93f5dbdee7ddc1d7611acd324f23bae77790b40576e952bc`、map224f3ae9です。
既存日付・確認境界471件とplugins65件はそれぞれ1起動で成功・skip0、CI同版lint成功です。
94378監査は別checkout overlayのformal116成功・skip0とworkflow27検査・独立レビューを経て、
利用者の明示承認後に実保護targetへ6f09904bで反映しました。旧95cの反映commitは1169e186です。

37 ZIP・1,016entryを新規生成し、全CRC・安全パス・LICENSE/PDF0を確認しました。
f831比10ZIPの10entryが変わり、うち9はmapのmeasures.py source SHA、1はWindsurfのmap SHA束縛です。
他27ZIP、7個別スキル、全業務指示と認証設定は同一です。source14の1件とmapが変わっているため、
旧source377のLinux全結果や旧native13全入力一致は継承しません。
現在の公開原本からの全37 ZIP・1,016entry再生成は成功し、全hash・CRC・entry bytesが83f9と一致しました。

現在は限定確認12（入力一致9＋fresh3）・Roo失敗1・package load前blocked2（Linux Codex＋QueryPie/Aru）・他未実施14・総合受入0です。
既存Codex接続のCFP5種類とEMSテンプレートCSV／XLSXの受領・保存・応答SHA一致・構造確認、EMS読み取りは前駆環境の別baselineであり、新候補の受入ではありません。
Claude Code／Gemini CLI／Copilot CLIでnative metadata15操作を新規実行し限定成功3を確認しました。
新たなhostedスキルimport・モデル・remote MCP呼び出しは0、CI・image・DEV・公開は未実施です。
[候補hash](../docs/candidate-package-v1.2.0-canonical-date-license-held-20261026.json)と[入力一致範囲](../docs/candidate-native-equivalence-v1.2.0-canonical-date-license-held-20261026.json)を参照してください。


新83f9の38資産stageとGET専用helperは用意済みで、386項目の独立レビューは指摘0です。
これはローカル準備と合成metadata14対照の確認で、新候補のDraft upload・live metadata・公開後匿名取得は未実施です。
## 以下は355/f831候補およびそれ以前の時点記録

以下のsource・「同一」「現候補」「新規」は各観測時点の記録で、新e794/83f9の成功を示しません。

この文書は **Draft作成前の準備時点（2026-10-25T18:32:22.688302+00:00）の記録** です。未作成・未upload・未配備・未公開・未受入の記載は、その時点の状態を示します。後続の現行状況は[PR #5](https://github.com/emmatch-dev/econipass-mcp-plugins/pull/5)と[GitHub Release](https://github.com/emmatch-dev/econipass-mcp-plugins/releases/tag/econipass-mcp-plugin-v1.2.0)で確認し、この準備記録を後続の実施結果として扱わないでください。

この文書のcommand・source bindingは非公開backendで実行した検証の記録です。
本公開リポジトリ単独の再実行手順ではありません。builder・tests・サーバー本体は含みません。
生成済みZIP、公開原本とのbyte一致、CI・配備、実機受入は別々に確認します。

## 2026-10-26 現行クライアント設定候補の検証

配布設定source `355e24babeac05182d97001e3004177ff666bb9a` の候補release SHAは
`f8317e75b008d3a09cb058d32236b6c882bde245e536fb5ba3840346f5efc287`。
37 ZIP・1,016entry・LICENSE/PDF0。旧9640から5 ZIP変更、他32はbyte同一で、共通30・map・source14も不変です。
公開原本と固定source355のbuilder/API7から全37 ZIP・各entryを再生成し一致しました。
Macの統合設定65テスト／skip0とCI同版lintは同一builder/test bytesへ束縛しています。
最後のGemini/n8n差分58eeは文書のみで、7skill/29kit validatorと独立レビューを別に確認しました。

Linux source377（MCP実装6d3、source14/map同一）の別checkoutでは、MCP5,308成功・実接続smoke6skip、
synthetic E2E241操作（239成功・想定対象不在2拒否）、root限定210成功・既存skip1、
実PG backend影響35成功・skip0、CI同版lint・actionlint27・YAML27が成功しました。
95c監査案の試験overlayを含む検証で、実保護ファイルへは未承認・未適用です。
内包pluginsは旧55件で、新設定65件のLinux実行ではありません。
root suiteは専用tmpfsと限定capabilityの隔離container・network noneで確認し、旧失敗証跡も保存しています。
最終独立closureは376項目・指摘0。専用VM停止・2設定hash復元・所有資源不在を確認し、他VM不変は主張しません。

既存native13とClaude7スキルは入力・保存済みroundtripのbyte一致による再紐付けで、新実行／import／UI観測は0です。
Roo1失敗は維持します。29環境は限定成功13／失敗1／未実施15／総合受入0です。
[現在の入力一致記録](../docs/candidate-native-equivalence-v1.2.0-current-clients-license-held-20261026.json)と[候補hash](../docs/candidate-package-v1.2.0-current-clients-license-held-20261026.json)を参照してください。
CI・image build・DEV配備・公開・認証済み業務受入は未実施で、LICENSE／新OAuth／ChatGPT保留を維持します。

## 以下は旧9640候補およびそれ以前の時点記録

以下の「現候補」「新規」「未実施」は各節の観測時点を指し、現在のfresh実行や未完了gateを上書きしません。

2026-10-26の現候補はMac12試行中11限定成功・Roo metadata列挙1未合格です。
Linux Codexの導入／metadata確認1件も成功し、ローカル13試行は12限定成功・1未合格です。
新規native資源のcleanupを確認しました。認証済み受入・全13成功は主張しません。
Claude WebのEMS v3新規import／3ソースroundtripと他6同一ZIPの有効状態再確認は別の限定観測です。
[今回の限定記録](../docs/candidate-native-load-v1.2.0-merged-ems-license-held-20261026.json)を参照してください。総合受入は0／29です。
以下の統合Mac検証節はmetadata377作成時点の記録で、当時の「新native13未実施」は候補生成時の状態です。
後続の275a／5ee／各旧版はソース別履歴であり、新sourceのLinux全suite・image・CI・DEV成功へ継承しません。

## 2026-10-26 develop追加2操作の統合ソースとMac検証

基点develop `06ee31fbe3c2a5a5700c08d72054240242c476e3`へ、旧候補の一般task/activity・
CFP受信互換・EMS metadata既定/明示embeddedを統合した。実装source commitは
`6d3fc5d6ac4719618621302a51a81d75e157c5c8`。
上流の`list_ems_import_summaries`と`export_ems_import_transactions`を維持し、
固定EMS契約は167操作（参照76・更新91、そのうちdownload12）、EMS担当は172toolとなる。
12download照会へ同じ返却方式を適用し、source decimal・原本ledgerと現在の登録状態を区別する。

- Mac専用hash lockのPython 3.11.16 / FastMCP3.4.10 / mcp1.30.0 / pytest9.1.1で、
  既存refresh helperから4profileの実登録241 / 254 / 256 / 固定PRD参照30を観測した。
  socket/DB接続を拒否し、lifespan・業務toolは呼んでいない。Linux実測は未実施。
- tool→skill割当は両側を統合し、256toolの明示割当と14source inventoryを保持した。
  source6d3の14ファイルへbyte hashを正式同期し、release branch基点は06eeと記録した。
  新map SHAは`64e885efed0ed8df878efe53721fcd302e5754fdff0768aeb4ab84d9aacce345`。
- 既存plugins suite55件が成功（skip0、37 ZIP再現性・任意LICENSEの保持を検査する3件を含む）。
  7skill validator、builder check、JSON・source binding・相対参照・diff検査も成功した。
  LICENSEを一時fixtureで検査することと、実配布物へ適用することは別である。
- 新しいMac検証候補は37 ZIP・999entry・common30ファイル・14source bindingで、
  全ZIPのSHA/CRCとcommon30のbyte一致を確認した。LICENSE/PDFは0件。
  release.json SHAは`9640f2d6c3dbeb683d3031596ee3a62101686096e8c9bf80d43f5bc48854a27d`。
  Linux/本番image/CI/DEV・認証済み業務受入は未完了で、新native13の再試験もまだ実施していない。
- develop側のダッシュボード・CSV受付集計/原本出力と、一般task/activity・CFPの追加を両方保持する。
- 以下の275a/5ee・develop単独の試験、旧6cc候補/native13/Claude Web観測は各ソースの履歴であり、
  新しい統合sourceのCI・配備・実機受入へ継承しない。Mac検証候補は新規生成したが、公開は行っていない。
- 旧0a691b監査承認・10f599適用と旧CI成功は統合後ソースの監査承認ではない。
  protectedファイルは06eeのまま保持し、新監査案の検証・独立レビュー・必要な承認を別に確認する。
- LICENSE適用、新OAuth、ChatGPT受入の保留は維持し、旧MIT候補を配布対象にしない。

## 1.2.0 旧275a候補の検証履歴

実施日: 2026-10-25。ブランチ基点は `8c578bac`、実装ソースcommitは
`275a21cda3b89ebadaf722b3eadff55e9e2e8775`。最終の登録入力は
`econipass/tool-skill-map.json` の `source_files_sha256`、生成物は新規出力先の
`release.json` の `source_binding` と `artifact_sha256` で識別する。
この記録とオフライン試験は、DEV配備・公開や29環境での総合受入の証明ではない。

既存Claude接続で実測したCFP・EMSのXLSX resource非対応に対し、CFP取得とEMS11 downloadで
既定metadataと明示embeddedを分離した。
同じfile metadataをJSON textとstructuredの両方へ返し、取得・本体同梱・受領保存を区別する。
CFP/Workbook113件、関連境界207件と独立60ケースは旧3.4.7で確認した履歴であり、
新3.4.10/slim・opentelemetry-api1.45.1でのsource5eeの全suiteは5,225 passed / 6 skipped、
認証E2E58件・239tool（ok237 / 想定対象不在refused2 / failed0）が成功した。
6skipはRUN_SMOKE_TESTS未指定の実接続smokeである。この結果は追加EMS修正275aの全体成功へ
継承せず、275aのEMS・境界・schema・plugins・formal・byte SDK試験を別に確認する。
4profileは新3.4.10のLinux実登録で239/252/254/固定30、map SHAは
`ec2295c64c3781032cb684b367dab521d8781c4d037aae34d6b3da347c8701ad`。
LICENSEはユーザー保留のまま適用せず、以前のMITレビュー候補を公開対象にしない。

- 4profileの登録数は239 / 252 / 254 / PRD参照30。全254toolを7skillsへ割り当てる。
  4profileの実登録読取をpackagerと既存coverage suiteで共用する。
  `scripts/refresh_tool_skill_map.py`は明示的なtool→skill割当を保持して件数とhashを再生成し、
  未割当toolや廃止toolを検出したら停止する。業務tool・lifespan・ネットワーク/DBは起動しない。
- ソースbyteの1文字改変、source inventoryの欠落・追加・重複、path escape、
  symlink、存在しないfile、不正hash、重複JSON keyを既存plugins suiteで検証する。
- versionは共通/Codex互換/Claude/Geminiの4manifestで1.2.0に同期する。
  対応29環境のnative config形式、OAuth設定、確認/自動承認方針を一括変更しない。
- 7skillsへtask/activity/独自項目、最新EMS3操作、法定本人ブラウザー引継ぎと、
  CFP download成功とupload受入の区別を反映する。

- 旧3.4.7での `python -m pytest -q plugins/tests`: **55 passed**。
  新3.4.10 source5eeの全suiteにも同じ55件が含まれる。追加EMS source275aでは別途再検証する。
  source byte bindingと境界拒否、実登録profile、allowlistのread-only属性、37 ZIP再現性、
  隠しmanifest、29kitと4API sampleのオフライン起動を既存suiteで確認した。
  ディレクトリ用PNGの構造・CRC・サイズ境界と、任意LICENSEの全37配布物への
  byte保持・再現性も検証した。LICENSEの選択・適用は別途確認する。
- 7skillsの`quick_validate.py`、black 26.3.1 / isort 5.13.2 / flake8 7.3.0、
  `git diff --check`が成功。生成物は新規directoryへ作成し、既存ZIPを上書きしない。

最終のbuild hashは確定ソースのrelease証跡へ記録する。
以下の各版の結果を1.2.0の再試験結果として扱わない。

## 2026-10-25 develop側EMS契約の検証履歴

CSVの受付集計・原本出力と、ダッシュボード監査Wave 1の事業所有効開始変更・
保存報告再生成を両方保持した。native router/DTOから再生成した固定契約は
167操作（参照76・更新91・出力12）で、管理用・業務用の公開範囲を省略していない。

- fastmcp/slim 3.4.10・OpenTelemetry API 1.45.1・Python 3.11.17のLinux環境で、
  既存`test_tool_coverage.py`のruntime catalog readerを再利用して実登録を観測した。
  Python socketとpsycopg2接続を拒否し、lifespan・業務toolは実行していない。
- 4profileの実登録数は233 / 246 / 248 / PRD参照30。
  全248ツールを既存7スキルへ割り当て、EMSは172ツールを担当する。
  tool名hash・skill件数・6登録ソースのhashを実測へ同期した。
- 追加された2更新は`ems-write` / `write`タグと`mcp:write`の確認付き操作であり、
  PRD参照profileの固定30件・8タグ・tool名hashを変更していない。
  version 1.1.0、cloud adapter、接続先ごとの許可範囲も変更していない。
- native contractの再生成一致、hard schema blockerなし、既存soft schema snapshotとの
  一致を確認した。全MCP suite・HTTP・配備・認証済み受入の完了は、最終統合ソースの
  証跡で別途確認する。この対応表同期は外部公開やtenant受入を表さない。

### 同日のダッシュボード監査Wave 2統合

既存のダッシュボード照会へ`site_ids`、品質課題照会へ5つの任意filterを追加した
上流変更と、CSV受付集計・原本出力を保持した。固定カタログの167操作、公開tool名と
固定PRD参照30件・8タグ、version・adapterは変更していない。対応表の登録ソースhashは
Wave 2のserver・固定契約へ同期した。

共有metadataの入力制約と出力schemaも更新されるため、上記の旧登録観測だけで新しい
ソース全体の検証完了とは扱わない。確定コミットでnative生成一致・実登録profile・
既存metadata/EMS/権限境界の影響suite・HTTPを確認し、監査・CI・配備・認証済み受入は
それぞれの最終ソース証跡で記録する。

## 2026-10-24 CSV照会の対応表同期

`list_ems_import_summaries`と`export_ems_import_transactions`を既存の
`ems-operations`スキルへ割り当てた。登録ソースは対応表の
`source_files_sha256`で識別する。EMS生成カタログのhashと、基点のdevelopで既に
変更済みだったserver・法定帳票2ファイルの古い記録を現sourceへ合わせた。
後者3ファイルのコードは今回変更していない。

- fastmcp/slim 3.4.10・OpenTelemetry API 1.45.1のLinux環境で、既存
  `test_tool_coverage.py`のruntime catalog readerを再利用して観測した。
  Python socketとpsycopg2接続を拒否し、lifespan・業務toolを実行していない。
- 4profileの実登録数は231 / 244 / 246 / PRD参照30。
  全246ツールを既存7スキルへ割り当て、EMSは170ツールを担当する。
  profileのtool名hash・skill件数は実測名から計算した。
- 新規2操作はreadOnlyHint=true、`ems-operations`タグ、`mcp:read`のみ。
  PRD参照profileの30件・tool名hash・条件、cloud adapterとversionは変更していない。
- 全MCP・配布物検査と実HTTP E2Eの最終結果は、最終ソース固定後の証跡で確認する。
  この対応表の同期は、プラグインの外部公開・インストール・認証済みtenant受入を表さない。

## 1.1.0 更新時の確認

実施日: 2026-10-20。ブランチの基点は
`b818582b07472cddda000e759858618af501797b`。更新後の登録ソースは
`econipass/tool-skill-map.json` の `source_files_sha256` で識別する。
これはソース登録・配布形式の検証であり、各接続先の公開・認証済み受入を表さない。

- 58件のEMS操作追加後、4公開profileの登録数は228 / 241 / 243 / PRD参照30。
  全243ツールを7スキルへ割り当て、EMSは167ツールを担当。
  profile名・条件・tool名ハッシュは対応表を正本とする。
- 既存MCP suiteへ`../../plugins/tests`を追加。サービス内の既存`pytest -q`で
  パッケージテストも収集されることを`--collect-only`で確認した。
  追加CI job・追加pytest起動はない。
- `python -m pytest -q ../../plugins/tests`（MCPサービス起点）: **24 passed**。
  引き続き登録確認はDB・ネットワーク接続を拒否し、業務ツールを呼ばない。
- 既存Backend lintの対象を`plugins/**/*.py`へ拡張。
  実Git checkoutの変更一覧に対し、CIのcollectorを実行して対象/除外を確認する
  契約テストを含む`test_backend_dev_privileged_governance.py`: **142 passed**。
- black 26.3.1 / isort 5.13.2 / flake8 7.3.0でpluginsと変更した契約テストが成功。
  全27 workflowのYAML parse、ローカルactionlint 1.7.12 `-oneline`、
  `git diff --check`が成功。
- 7スキルの`quick_validate.py`が成功。独立レビューで、料金試算が保存済みの
  有効設定を使うこと、定期実行は報告snapshotの作成であること、M&V判断が
  `expected_sequence`と証跡hashに従うことを確認し、説明を修正した。
- ネイティブ計画previewはsavepoint内で書込とrollbackを行うため、MCPではwrite扱い。
  MCP dry-run → 確認付きnative preview → 別途create/applyという区別を手順に明記。
- Codex / Claude / GeminiのmanifestとClaude marketplaceはversion 1.1.0に同期。
  共通`plugin.json`と`mcp.json`は保存済みのAgent Plugins 1.0.0公式Schema検証が成功。
  platform matrixの2026-10-08時点の製品仕様確認日は、再調査なしに更新しない。

CIのdigest固定actionlintコンテナは、Docker daemon不在のためローカルでは起動できず、
上記ローカルbinaryで検査した。最終リリース担当がexact SHAのCI・配備・公開・
認証済み受入の結果を別途記録する。
以下は1.0.0時点の証跡であり、1.1.0の外部公開や実機受入を示すものではない。

## 1.0.0 の確認記録

実施日: 2026-10-08。MCP参照ソース: `7ca723a1e877500f4df7f49a3c76a46a48dbb9bd`。
対象はプラグイン、業務スキル、各クライアント用の設定・指示書・APIサンプル。
サーバー処理、権限、公開タグ、認証設定、CI workflowは変更していない。

## 確認結果

- 7スキルのSkill Creator `quick_validate.py`が成功。
- `python -m pytest -q plugins/tests`: **24 passed**。
  4つの公開profileで実MCP登録を読み、最大185ツールの割当・件数・ハッシュを照合。
  この登録確認ではネットワーク・DB接続を拒否し、lifespanや業務toolは実行しない。
  Copilot cloudの全allowlist対象も、実登録のreadOnlyHint・タグ・scopeから参照専用と確認。
- ZIPの再現性、隠しmanifestの同梱、スキル参照の境界、既存出力保護、symlink拒否、
  カスタム接続先の反映、QueryPieに未確認のSSE接続先を作らないことを確認。
- 4つのAPIキットをSDK非読込のPythonで実行し、同梱手順の`--check-config`が成功。
  認証情報はテスト用文字列で、モデルAPI・MCPへの接続は行っていない。
- black 26.3.1、isort 5.13.2、flake8 7.3.0で全追加Pythonファイルが成功。
  flake8は最大行長88・複雑度10・既存CIのignore指定を使用。
- `plugin.json`と`mcp.json`をAgent Plugins 1.0.0の公式JSON Schemaで検証し成功。
- Codex CLIでローカルmarketplaceを登録し、`econipass@econipass-plugins`の
  version 1.0.0がavailableと表示された。インストール・有効化・OAuth認証は未実施。
- 独立レビューとEMS・CFP・参照専用接続のシナリオ確認を実施。
  API導入手順の相対パス不一致は修正し、生成キットの起動テストで確認。
- 最終ビルドは共通プラグイン1・個別スキル7・プラットフォームキット29の計37 ZIP。
  各配布物のSHA-256は生成先の`release.json`に収録。

## 再実行

MCPサービスの開発依存を入れたvenvをactivateして、リポジトリrootから実行する。

```bash
python -m black --check plugins
python -m isort --profile black --check-only plugins
python -m flake8 plugins --max-line-length=88 \
  --ignore=A003,E800,E203,W503,W504,B008,B006 --max-complexity=10
python -m pytest -q plugins/tests
python plugins/scripts/build_packages.py --check
python plugins/scripts/build_packages.py --output /absolute/path/new-release
```

## 未実施の項目

29環境でのインストール、認証済みの参照・更新、OAuth refresh/revoke、添付リソースの受入は
実施していない。Claude/Gemini等の実CLIでのロードも未実施。APIサンプルは実SDK・モデルAPI
との疎通試験前であり、Roo bridgeも未起動。公開ディレクトリ申請・組織への配布は未実施。
この記録はGAや全環境での動作保証を表さない。

1.0.0の配布形式だけの変更にはバックエンドのデプロイは不要だった。
1.1.0で追加した58操作にはbackend/MCPの配備と公開catalogの確認が必要。
機能が実際に使えるかは、接続先のcatalog・scope・機能フラグ・利用者の権限と、
各プラットフォームでの受入結果によって判断する。
