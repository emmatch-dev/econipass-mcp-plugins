> v1.2.0の現行候補はff0bのクライアントDEV previewです。37 ZIP＋release.json、EMS17操作追加と最大273のソース登録を含みます。65テスト・7スキル検査・CLI7環境25 metadata・SDK4合成fixtureが成功しました。総合受入0/29、Kong候補TLSとサーバー説明修正の配備は未完了です。LICENSE・新OAuth・ChatGPTは保留です。現行状態は[受入記録](../docs/ACCEPTANCE.md)、公開状態は[Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)を参照してください。
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
