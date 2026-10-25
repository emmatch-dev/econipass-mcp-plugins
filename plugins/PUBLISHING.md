# EcoNiPass DEV 1.2.0 の配布・公開

接続先は`https://api.dev.app.econipass.com/mcp`。共通プラグイン1・個別スキル7・29環境キットの37 ZIPとrelease.jsonを使います。
形式は[対応一覧](PLATFORMS.md)に従い、全製品が同じnative plugin形式とは扱いません。

現候補は実装`6d3fc5d6ac4719618621302a51a81d75e157c5c8`、metadata`3775093d517eac5ef183afc148d56016058fea63`、基点`06ee31fbe3c2a5a5700c08d72054240242c476e3`です。
通常241／共有法定帳票254／最大256／固定PRD参照30、EMS12downloadを含みます。
map SHAは`64e885efed0ed8df878efe53721fcd302e5754fdff0768aeb4ab84d9aacce345`、release.json SHAは`9640f2d6c3dbeb683d3031596ee3a62101686096e8c9bf80d43f5bc48854a27d`。
旧275a・6cc85監査承認・適用・CIは履歴で、新source監査は未承認・未反映、CI未push、DEV未配備、未公開です。
Mac12試行は11限定成功／Roo1未合格、Linux Codexは導入・metadata確認が成功しました。
ローカル13試行は12限定成功・1未合格です。Claude Webスキル確認を加えると13限定成功／1未合格／15未実施で、総合受入は0／29です。
[受入記録](../docs/ACCEPTANCE.md)と[候補hash](../docs/candidate-package-v1.2.0-merged-ems-license-held-20261026.json)を公開判断の正本とします。

## GitHub配布の順序

以下は非公開backendのrelease担当向けです。本公開repoにサーバー・builder・tests・CIを追加しません。
公開repoは[`emmatch-dev/econipass-mcp-plugins`](https://github.com/emmatch-dev/econipass-mcp-plugins)です。

1. 新統合ソースの差分・監査案を検証し、独立レビューと必要な明示承認を確認する。旧承認を新sourceへ流用しない。
2. 最終sourceの必須CIを通し、developへのmerge後SHA・image buildを確認する。
3. 通常DEV手順でbackend/MCPとKongの配備結果を別々に確認する。ZIP更新だけではサーバーへ反映されない。
4. 同じ原本から生成した37 ZIP＋release.jsonの38assetを照合し、公開原本common30・14ソース・全999entryのbyte一致を確認する。
   現9640候補はローカル38asset照合と、draft=true／published_at=nullを要求する公開前metadata境界検査を準備しただけでuploadはしていない。
5. 公開repoの差分と受入・未実施を独立レビューし、最終公開元SHAとrelease targetを固定する。
   `econipass-mcp-plugin-v1.2.0`をDEV prereleaseとして作成し、正確な38assetだけを添付する。
   公開前draft metadata検査と、公開後の匿名取得・hash／size／CRC／entry照合は別gateで記録する。
6. 公開後にREADME・受入記録へ実際のCI／DEV／公開結果を追記する。未実施の実機受入を成功へ置換しない。

v1.1.0のtag・assetsや旧候補を変更せず、MITレビュー候補を使いません。
公開ファイルに秘密・顧客情報・ローカル絶対pathを含めず、backend本体・履歴・設定をコピーしません。
利用者は公開済みの正しい版のZIPを取得し、同梱手順に従います。スキル導入自体でOAuth grantや業務権限は付与されません。

## ライセンスと公式ディレクトリ

LICENSE適用はHELDです。現37 ZIPのLICENSE0件を確認し、MIT等の許諾や新たな権利付与を推定しません。
GitHubでの既存公開指示は、公式規約・CC0・ソフトウェアLICENSEの同意ではありません。

- Claude: manifestエラー／警告0でもdirectoryはLICENSE_MISSING blocking1。LICENSE適用保留中は掲載申請・MIT候補upload・許諾申告をしない。
- OpenAI: 公開者の本人・法人確認前にZIP upload不可。未申請。
- MCP Registry: remote-only serverでsoftware LICENSEが不要でも、metadata CC0を含むTerms同意と組織namespace認証は別途必要。未登録・未同意。

新OAuthとChatGPT受入も保留中です。審査専用情報は公開せず、DEV endpointを本番として申告しません。

## 実機受入の範囲

今回のローカルCLI・SDK・Web skill導入は限定確認で、認証済み総合受入は0／29です。
Rooの初期化raceは疑いに留まり、最初のmetadata失敗を保存しています。
remote catalog/read、tenant・scope拒否、refresh/revoke、実ファイル受領保存、投入・置換・確認tokenを伴う業務フローは
認可済みの対象と実クライアントで別に確認します。結果不明の更新は自動再試行しません。
