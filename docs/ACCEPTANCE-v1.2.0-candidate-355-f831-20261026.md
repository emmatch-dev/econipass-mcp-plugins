# DEV 1.2.0現行クライアント設定候補の受入・公式掲載状況

この文書は **Draft作成前の準備時点（2026-10-25T18:32:22.688302+00:00）の記録** です。未作成・未upload・未配備・未公開・未受入の記載は、その時点の状態を示します。後続の現行状況は[PR #5](https://github.com/emmatch-dev/econipass-mcp-plugins/pull/5)と[GitHub Release](https://github.com/emmatch-dev/econipass-mcp-plugins/releases/tag/econipass-mcp-plugin-v1.2.0)で確認し、この準備記録を後続の実施結果として扱わないでください。

確認日: 2026-10-26 JST。配布設定source `355e24babeac05182d97001e3004177ff666bb9a`、
MCP実装 `6d3fc5d6ac4719618621302a51a81d75e157c5c8`、metadata `3775093d517eac5ef183afc148d56016058fea63`、
基点 `06ee31fbe3c2a5a5700c08d72054240242c476e3` です。
**候補未配備・未公開、認証済み総合受入0／29、公開版の部分確認0／29です。**

release.json SHAは `f8317e75b008d3a09cb058d32236b6c882bde245e536fb5ba3840346f5efc287`、
対応表SHAは `64e885efed0ed8df878efe53721fcd302e5754fdff0768aeb4ab84d9aacce345`。
37 ZIP・1,016エントリ・共通30ファイル・14ソース束縛・LICENSE/PDF混入0を確認しました。
[候補hash](candidate-package-v1.2.0-current-clients-license-held-20261026.json)、[機械可読記録](acceptance-summary.json)、[入力一致による再紐付け](candidate-native-equivalence-v1.2.0-current-clients-license-held-20261026.json)が正本です。

## 設定補完と未完了の配備

旧Cascadeは他MCPを含む100有効ツール上限に合わせ、組織確認だけの既定と業務別13設定を用意しました。
各設定は1〜64ツール、全256ツールは横断して到達できます。設定は一つだけ選びます。
除外リストは未知ツールを自動で隠せないため、実catalog全ページの名前・件数・hashを記録profileと
照合し、差分時は利用を止めて再生成します。新Devin Localは別の専用設定です。
Junie自身のMCP設定、旧Qを保持したKiro alias `ep` と `oauthScopes: mcp:read`、
Gemini Enterpriseの初期Actions全OFF・Reload後最大100の選択、n8n v1.2以降のHTTP Streamableも補完しました。
[プラットフォーム別の手順](../plugins/PLATFORMS.md)を確認してください。5クライアントの新たな実機試験はしていません。

サーバー実装・共通30ファイル・map・14sourceは旧9640候補とbyte同一です。
通常241／共有法定帳票254／最大256／固定PRD参照30はオフライン登録数で、実環境の公開数ではありません。
EMS固定契約167操作・担当172tool・download12、CFP取得のbounded metadata既定／明示embeddedを維持します。
metadataでは本体・取得可能URLを返さず、クライアント受領／保存確認は別です。
新監査95c案は未承認・未適用で、実protected3ファイルは06ee基点のbyteを維持しています。
旧0a監査承認・10f反映・旧CI、既存DEV06eeのbackend/Kong成功は履歴です。
新候補のCI・image build・通常DEV配備・公開結果は未実施で、それらの成功へ流用しません。

## ソース別のローカル検証

| 検証 | 結果と範囲 |
| --- | --- |
| Linux source377 MCP | 5,308成功／6skip。skipは未指定の実接続smoke。内包pluginsは旧55件 |
| 同synthetic E2E | 241操作＝239成功＋想定対象不在2拒否、失敗0 |
| 同root限定suite | 210成功／既存と同じskip1。専用隔離container・network none・限定capability |
| 同backend影響 | 実synthetic PostgreSQLで35成功／skip0 |
| 同workflow/lint | CI同版lint・actionlint27・YAML27成功 |
| 新クライアント設定 | Mac65成功／skip0。builder/testはc55eb freezeと同一。最終58eeは文書変更だけで別validator・レビューを確認 |
| 新候補 | 公開原本＋source355固定builder/API7から37 ZIP・全1,016entryを再生成しbyte一致 |

Linuxはsource377の別試験checkoutで95c監査案の試験overlayを含みます。実worktreeへの適用や人間承認ではありません。
source14/mapの一致によってサーバー実装へ束縛しますが、新355の全ソースをLinuxで試験したとは主張しません。
旧root overlay失敗23件を保存し、そのうち11件の旧子例外原因は直接観測していません。
最終独立closureは376チェック・指摘0。専用VM停止、2設定の元hash復元、所有資源の不在とdefault contextを確認しました。
他VMの状態が不変だったとは主張しません。これらはCI・配備・実テナント受入の証拠ではありません。

## 29環境の入力一致による再紐付け

旧9640で実行したMac12試行は11限定成功・Roo1未合格、Linux Codexは導入／metadata確認1限定成功でした。
その13キットと共通ZIPが新候補と完全一致すること、元receipt・前後seal・source14/mapが維持されることを確認しました。
Claude Webの旧EMS v3／他6 v2についても7 ZIP・20ソース・保存済みprovider wrapper7件の内容を照合しました。
新候補についての新規native実行、import、現在UI観測は0で、履歴の実行日時とhashを保持した再紐付けです。

| 状態 | 環境数 |
| --- | --- |
| 元Mac試験の限定成功を入力一致で再紐付け | 11 |
| 元Linux Codex CLI試験の限定成功を再紐付け | 1 |
| 元Claude Webスキル導入の限定確認を再紐付け | 1 |
| Roo metadata列挙の失敗を維持 | 1 |
| 未実施（ChatGPT保留を含む） | 15 |
| 総合受入／公開版の部分確認 | 0 |

Rooの初期化raceは疑いで、因果は未確定・再試行なしです。exit0を成功へ読み替えていません。
Cursor／VS Codeは設定のみ、SDKは合成fixture、Claude hostedはWebのスキルのみです。
認証済みcatalog、tenant/scope拒否、refresh/revoke、CFP／EMS実ファイル受領・保存・投入／置換は未受入です。
旧9640の[時点記録](history/ACCEPTANCE-v1.2.0-candidate-377-9640-20261026.md)と
[同時点の機械記録](history/acceptance-summary-v1.2.0-candidate-377-9640-20261026.json)を保存しています。
旧native/package JSONも変更していません。

## 公開と保留

| 公開先 | 状況 |
| --- | --- |
| GitHub | DEV1.1.0公開済み。1.2.0は未公開。新38資産をローカル準備し、公開前draft=true／published_at=nullを含む14対照を確認。uploadなし |
| MCP Registry | namespace未登録。metadata CC0を含む規約同意・組織認証は未実施 |
| OpenAI | 公開者本人・法人確認が必要。未upload・未申請 |
| Claude | 共通ZIP同一性で旧manifestエラー／警告0とdirectory LICENSE_MISSING blocking1を再紐付け。新validator実行なし・未申請 |

LICENSE適用、新OAuth、ChatGPT受入は利用者指示で保留しています。MIT候補は配布せず、権利付与を推定しません。
Registryの[認証仕様](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/authentication.mdx)と
[Terms](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/terms-of-service.mdx)への同意は別の手続です。
DEV URLを本番として申告せず、審査情報・個人情報・ローカル絶対pathを公開しません。
