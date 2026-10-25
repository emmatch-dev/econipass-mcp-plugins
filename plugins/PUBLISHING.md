# EcoNiPass DEV 1.2.0 の配布・公開

この文書は **Draft作成前の準備時点（2026-10-25T18:32:22.688302+00:00）の記録** です。未作成・未upload・未配備・未公開・未受入の記載は、その時点の状態を示します。後続の現行状況は[PR #5](https://github.com/emmatch-dev/econipass-mcp-plugins/pull/5)と[GitHub Release](https://github.com/emmatch-dev/econipass-mcp-plugins/releases/tag/econipass-mcp-plugin-v1.2.0)で確認し、この準備記録を後続の実施結果として扱わないでください。

接続先は `https://api.dev.app.econipass.com/mcp`。37 ZIP＋release.jsonの38資産を使います。
配布設定source `355e24babeac05182d97001e3004177ff666bb9a`、MCP実装6d3、metadata377、基点06eeです。
release.json SHAは `f8317e75b008d3a09cb058d32236b6c882bde245e536fb5ba3840346f5efc287`、
map SHAは `64e885efed0ed8df878efe53721fcd302e5754fdff0768aeb4ab84d9aacce345`。
現在は未配備・未公開、新監査95c案は未承認・未適用、最終CI未実施です。
[受入記録](../docs/ACCEPTANCE.md)と[候補hash](../docs/candidate-package-v1.2.0-current-clients-license-held-20261026.json)を正本にします。

## GitHub配布の順序

以下は非公開backendのrelease担当向けの記録です。本公開repoにサーバー・builder・tests・CIを追加しません。
公開先は [emmatch-dev/econipass-mcp-plugins](https://github.com/emmatch-dev/econipass-mcp-plugins) です。

1. 新監査案の必要な承認・最終差分・独立レビューを確認する。旧0a承認を新95cへ流用しない。
2. 最終sourceの必須CI、merge後SHA、image buildを確認する。ローカルLinux377の成功はCIではない。
3. 通常DEVでbackend/MCPとKongの配備を別々に確認する。既存06eeの稼働結果は候補配備の証拠ではない。
4. 同じ原本からの37 ZIP・全1,016entry・共通30・source14を照合し、固定したrelease.jsonと合わせた38資産を準備する。
   新stageはローカル準備だけで、公開前draft=true／published_at=nullを要求するmetadata14対照と固定manifest照合が成功した。
   旧9640の999entry stage/helperは変更せず、新しい値へ束縛したGET専用検証helperを別に用意する。
5. 公開repoの差分・受入範囲を独立レビューし、最終公開元SHAとrelease targetを固定する。
   `econipass-mcp-plugin-v1.2.0` はDEV prereleaseとして、正確な新38資産だけを添付する。
   公開前draft metadata、公開後の匿名GET・hash/size/CRC/実測entry数・tag先commit照合は別gateで記録する。
6. 実際のCI・DEV・公開結果だけを追記する。未実施の実機受入や入力一致を新規実行成功へ置換しない。

新候補はWindsurf・Junie・Q/Kiro・Gemini Enterprise・n8nの5 ZIPが変わり、他32 ZIPは旧9640と同一です。
旧native13とClaude7は該当ZIP/sourceのbyte一致で明示再紐付けし、新試験／importは0です。
ローカル12限定成功＋Roo1失敗、Webスキル限定1を保持し、全29は限定成功13・失敗1・未実施15・総合受入0です。
設定補完したクライアントの新たな実機成功は主張しません。[配置と制約](PLATFORMS.md)を確認してください。

旧tag/assets・旧候補・旧native記録は変えず、MITレビュー候補を使用しません。
秘密・個人/顧客情報・ローカル絶対pathを公開せず、backend本体や設定をコピーしません。

## LICENSEと公式ディレクトリ

LICENSE適用はHELDで、現37 ZIPのLICENSE0を確認しています。新しい利用許諾を推定しません。
GitHub公開の指示は、公式規約・metadata CC0・ソフトウェアLICENSEへの同意ではありません。

- Claude: 同一common ZIPへ旧manifestエラー／警告0を再紐付けても、directory LICENSE_MISSING blocking1は継続。新validator実行・申請・MIT候補uploadなし。
- OpenAI: 公開者本人・法人確認が必要。未upload・未申請。
- MCP Registry: remote-onlyでsoftware LICENSEが不要でも、metadata CC0を含む規約同意と組織namespace認証は別。未登録・未同意。

新OAuthとChatGPT受入も保留中です。DEVを本番として申告せず、審査専用情報を公開しません。
認証済みcatalog、tenant/scope拒否、refresh/revoke、ファイル受領保存、投入/置換の受入は別に確認します。
