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

# EcoNiPass DEV 1.2.0の配布・公開

現在の配布先と検証・受入の範囲は[README](../README.md)と[受入記録](../docs/ACCEPTANCE.md)を確認してください。
以下は[a72時点の履歴](https://github.com/emmatch-dev/econipass-mcp-plugins/blob/a72fb24fa8ca97db94091e9452a07d5a69195cbf/plugins/PUBLISHING.md)です。「未upload」「未配備」「候補」などは各観測時点の記録で、後続の現在値を示しません。

## a72以前の記録

この文書は **日付検証修正候補の配備・公開前の観測時点（2026-10-26T00:38:56.122704+00:00）の記録** です。旧f831のDraftと新83f9候補を区別します。後続の現行状況は[PR #5](https://github.com/emmatch-dev/econipass-mcp-plugins/pull/5)と[Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)で確認してください。

新候補は確認対象commit`6f09904ba5eedc0805b3895341b032f0770f807b`（日付実装e79417e3）、release SHA`83f900b69c53acea93f5dbdee7ddc1d7611acd324f23bae77790b40576e952bc`、map SHA`224f3ae9b21e1f3ea594b85d2d0e7cc161d593d36dd75ed6679e5aa6f7381065`。
37ZIP＋release.jsonの38資産を扱い、接続先はDEVの`https://api.dev.app.econipass.com/mcp`です。
旧f831のDraft423591210と新83f9は別候補で、新候補のupload・配備・一般公開は未実施です。
[候補hash](../docs/candidate-package-v1.2.0-canonical-date-license-held-20261026.json)と[受入記録](../docs/ACCEPTANCE.md)を正本とします。

## 後続のgate

1. 95c監査1169反映と、日付修正後の94378監査の明示承認・6f099反映を確認済みです。別作業の実行中CI・配備の終端を確認してから新候補をpushします。
2. 最終sourceの必須CI、merge後SHA、image buildを確認し、backend/MCPとKongの通常DEV配備を別々に検証する。
3. 現在の公開原本と固定builderから全37 ZIP・1,016entryを再生成し、hash・CRC・全entry byte一致を確認済みです。最終public commit／pushとの束縛は別に行います。
4. fresh native metadata成功3とpackage load前blocked2（Linux Codex環境準備timeout／QueryPie/Aru import前UI blocked）を区別する。現在は限定12・Roo失敗1・blocked2・他未実施14・総合受入0です。
5. 新候補の38資産stageとGET検証helperは別に固定し、386項目の独立レビューは指摘0です。最終public SHAへの束縛は未完了で、旧f831や旧9640のstage/helperは保持します。
6. 既存Draftへの後続反映が必要なら、actualmetadata・資産ID・不一致一覧を読んでから具体的差分をreviewする。結果不明時にcreateやuploadを自動再試行せず、clobber・削除・tag付替えを推測で行わない。
7. 公開前metadata、認証済みasset実bytes、公開後匿名GET・size/SHA/CRC・tag先commitを別gateで記録する。Draftの存在は一般公開ではありません。

旧1.1.0のRelease/tag/assets、旧f831候補とDraft、全過去のnative/equivalence記録を保持します。
既存Codex接続の前駆環境読み取りは、未配備の新候補や29環境総合受入の証拠へ加算しません。
秘密・顧客値・workbook・ローカル絶対pathを公開せず、backendコードを本公開repoへコピーしません。

## LICENSEと公式ディレクトリ

LICENSE適用・新OAuth・ChatGPT受入は保留です。候補のLICENSE0を確認し、MIT等の権利付与を推定しません。
ClaudeのLICENSE条件、OpenAIの公開者確認、Registryの組織認証・規約／metadata CC0同意は未完了で、公式申請は行っていません。
DEVを本番として申告せず、scope不足によるCFP投入preview拒否を業務投入成功として扱いません。
