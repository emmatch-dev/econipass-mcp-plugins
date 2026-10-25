# プラグイン配布物の検証記録

この文書のcommand・source bindingは非公開backendで実行した検証の記録です。
本公開リポジトリ単独の再実行手順ではありません。builder・tests・サーバー本体は含みません。
生成済みZIPとrelease.json、公開原本とのbyte一致、実機受入はそれぞれ別に確認します。

追加EMSソース275aのローカル影響2suiteは旧FastMCP3.4.7で496件成功しました。
Linux3.4.10の影響検証は初回1,401成功／11失敗を保存し、72eの試験9行のみの厳密補正後、
parity170件・文書42件が成功（skip0）しました。固定30監査116件・plugins55件（再現性3件）は
初回成功群です。全1,412件の一括再成功とは扱いません。CI条件lint・actionlint・27workflow YAMLも成功しました。
新sourceのtool-only E2E239件は237成功／想定対象不在拒否2／失敗0で、ローカル合成AS/APIと
PostgreSQL／Redisのみです。認証58シナリオや本番imageは5eeの履歴へ分離します。
これらは実SDKファイル保存・実接続受入・CI・DEV配備を証明しません。
新候補の[限定native13試験](../docs/candidate-native-load-v1.2.0-cfp-ems-security-license-held-20261025.json)はsource275a／実行時HEAD72e／release6cc85へ束縛し、
旧成功継承0・残り16環境未試験です。設定・スキル・SDK合成fixtureの確認はremote CFP／EMS取得や
実ファイル保存・新runtime・認証済み業務受入を証明しません。

## 1.2.0 更新時の確認

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
  新3.4.10 source5eeの全suiteにも同じ55件が含まれる。追加EMS source275aの55件も上記Linux影響試験の初回成功群で再確認した。
  source byte bindingと境界拒否、実登録profile、allowlistのread-only属性、37 ZIP再現性、
  隠しmanifest、29kitと4API sampleのオフライン起動を既存suiteで確認した。
  ディレクトリ用PNGの構造・CRC・サイズ境界と、任意LICENSEの全37配布物への
  byte保持・再現性も検証した。LICENSEの選択・適用は別途確認する。
- 7skillsの`quick_validate.py`、black 26.3.1 / isort 5.13.2 / flake8 7.3.0、
  `git diff --check`が成功。生成物は新規directoryへ作成し、既存ZIPを上書きしない。

最終のbuild hashは確定ソースのrelease証跡へ記録する。
以下の各版の結果を1.2.0の再試験結果として扱わない。

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
