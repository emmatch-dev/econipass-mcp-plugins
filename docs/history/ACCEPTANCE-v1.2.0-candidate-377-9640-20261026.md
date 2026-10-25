# DEV 1.2.0統合候補の受入・公式掲載状況

確認日: 2026-10-26 JST。実装ソース`6d3fc5d6ac4719618621302a51a81d75e157c5c8`、metadata`3775093d517eac5ef183afc148d56016058fea63`、
基点develop`06ee31fbe3c2a5a5700c08d72054240242c476e3`の新しい統合候補です。
**未配備・未公開、認証済み総合受入0／29、公開版の部分確認0／29です。**

Mac3.4.10の実登録は通常241／共有法定帳票254／最大256／固定PRD参照30です。
これはオフラインのprofile登録数であり、実環境catalogの公開数ではありません。
対応表SHAは`64e885efed0ed8df878efe53721fcd302e5754fdff0768aeb4ab84d9aacce345`、release.json SHAは`9640f2d6c3dbeb683d3031596ee3a62101686096e8c9bf80d43f5bc48854a27d`。
37 ZIP・999エントリ・common30ファイル・14ソース束縛・LICENSE0件を確認します。
[配布候補のhash](../candidate-package-v1.2.0-merged-ems-license-held-20261026.json)、[機械可読記録](acceptance-summary-v1.2.0-candidate-377-9640-20261026.json)、
[今回の限定試験](../candidate-native-load-v1.2.0-merged-ems-license-held-20261026.json)を正本とします。

## 実装と未完了の配備

上流のCSV受付集計`list_ems_import_summaries`、原本出力`export_ems_import_transactions`を保持しました。
EMS固定契約167操作（参照76・更新91、download12）、EMS担当172toolです。
CFP取得とEMS12download照会は既定metadata／明示embeddedを使い分け、同じbounded JSONを
text／structuredの両方へ返します。サーバー取得・本体同梱・クライアント受領を分離し、
metadataには本体や取得可能URLを含めず、受領確認はfalseです。対応クライアントで実保存を別に確認します。

旧監査0a691の承認・10f599適用と旧CI成功は旧source275aの履歴です。
新統合sourceの監査案は未承認・未反映で、protected3ファイルは06ee基点のbyteを維持しています。
新候補は未pushのためCI未実施、DEV未配備、未公開です。新しいLinux全体結果・image・CI・DEV結果は
最終ソースへ束縛して別途追記します。旧sourceの成功を新候補へ継承しません。
別の既存DEV predecessorとして06eeのbackend／Kong workflow成功を観測しましたが、
統合候補377の配備成功ではありません。frontend側の更新は別の進行中の作業です。

## 現在の29環境

Macの8 CLI＋4 SDKを逐次実行し、**12試行＝11限定成功＋Roo 1未合格**でした。
31クライアント操作、拒否境界probe1件、Node version probe1件の全33プロセスはexit0で、
OOM・timeoutは観測しませんでした。Rooはexit0でも候補7スキルを列挙できず、成功に数えていません。
初期化raceが疑われますが因果は未確定です。初回結果を保存し、再試行していません。
network denyによる接続試行の拒否を観測しましたが、remote MCP接続の成功は0です。
Linux Codexでは新候補をローカル導入2操作・metadata RPC3件で確認し、6項目のcheckが成功しました。
UID21125・network none・host mount0で、7スキルの有効状態を確認しました。
ローカル13試行は12限定成功・Roo1未合格で、全13成功ではありません。
native試験専用containerと新task image8件の不在、公式base保持を確認しました。別の全体試験用環境とは分離します。

Claude WebではEMS v3を新規importし、候補3ソースとダウンロード後の内容が一致しました。
他6スキルは今回ZIPが旧版とbyte同一であることと、現在のv2有効状態を再確認しました。
他6スキルの再importではありません。この1環境はスキル導入限定の追加観測です。

| 現候補の状態 | 環境数 |
| --- | --- |
| Macローカル試験の限定成功 | 11 |
| Linux Codex CLIのローカル導入・metadata確認の限定成功 | 1 |
| Claude Webスキル導入・有効状態確認の限定成功 | 1 |
| Rooスキルmetadata列挙の未合格 | 1 |
| 現候補では未実施（保留中ChatGPTを含む） | 15 |
| 認証済み総合受入 | 0 |

合計は限定成功13・未合格1・未実施15です。公開版の部分確認と認証済み総合受入は0／29です。
旧native13の成功継承は0です。
Cursor／VS Codeは設定のみ、SDKはローカル合成fixture、Claude hostedはWebのみです。
CLI／SDKのpackage entrypointは旧版と一致し、Nodeだけ22.23.2→22.23.4のHomebrew bottle更新を記録しました。
19のharness／policyと11の公開entrypointを前後照合しましたが、全依存ファイルの封印ではありません。
新OAuth、実モデル呼出、顧客業務操作は0で、認証済みcatalog・CFP／EMS取得・実保存・投入／置換の成功は含みません。

## 検証と履歴

新candidateのMac3.4.10 plugins55件が成功し、再現性3ケースを含みます。
7skill validator、builder check、14source／37ZIPのhash・CRC・JSON・参照検査を確認しました。
公開原本と候補の全37 ZIP再ビルドbyte照合は候補JSONで別に記録します。
Linux全suite・E2E・production imageの旧5ee／275a結果は新sourceへ継承しません。
[旧275a・6cc85候補の履歴](ACCEPTANCE-v1.2.0-candidate-275a-6cc85-20261026.md)と、その
[機械可読記録](acceptance-summary-v1.2.0-candidate-275a-6cc85-20261026.json)に旧監査承認・適用、CI時点、native13、試験結果を保存しました。
以前のCFP HTTP500修正、既存DEVのCFP／EMS XLSX非対応観測、本人UIのファイル保存は
それぞれ観測時点の証跡であり、新候補の配備・MCP本体受領の成功ではありません。

## 公式掲載と保留

| 公開先 | 状況 |
| --- | --- |
| GitHub | DEV1.1.0公開済み。1.2.0は未公開。新候補38assetのローカル照合・公開前draft境界検査を準備済み、uploadなし |
| MCP Registry | namespace未登録。remote-onlyでsoftware LICENSE不要でも、metadata CC0を含む規約同意・組織認証は未実施 |
| OpenAI | 公開者本人・法人確認が必要。未アップロード・未申請 |
| Claude | LICENSE適用保留。今回CLIもmanifestエラー／警告0、directoryはLICENSE_MISSINGのblocking1で未申請 |

新OAuth、ChatGPT受入、LICENSE適用は利用者指示で保留しています。MIT候補は配布せず、権利付与を推定しません。
Registryの[認証仕様](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/authentication.mdx)と
[Terms](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/terms-of-service.mdx)への同意は別の手続です。
DEV URLを本番として申告せず、審査用認証情報やローカル・利用者情報を公開しません。
