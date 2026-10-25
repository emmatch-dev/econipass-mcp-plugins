# EcoNiPass DEV 1.2.0 の配布・公開

接続先は `https://api.dev.app.econipass.com/mcp`。配布形式は共通プラグイン、
7個のスキル、29環境の導入キット（合計37 ZIP）。環境ごとのネイティブプラグイン、
設定ファイル、指示書、SDKサンプルの違いは [対応一覧](PLATFORMS.md) に従う。

## GitHubでの配布

以下は非公開backendのrelease担当向け手順です。本公開リポジトリにはサーバー本体・
builder・CIを含めません。利用者はGitHub Releasesの生成済みZIPと`release.json`を取得します。

2026-10-25の利用者指示でライセンスの適用は保留しています。現在の候補はLICENSEを
同梱せず、MIT等の利用許諾を追加しません。以前のMITレビュー候補37 ZIPは公開対象にせず、
LICENSEを除いて新規生成・検証した配布物を使います。GitHub配布の更新と、LICENSEを
必須とするClaude公式ディレクトリ掲載は分けて扱います。

backendリポジトリは非公開である。プラグインだけを配布する公開リポジトリ
[`emmatch-dev/econipass-mcp-plugins`](https://github.com/emmatch-dev/econipass-mcp-plugins)へ、
プラグイン原本、marketplace定義、導入手順、生成済みZIPを公開する。
backendリポジトリの可視性を変更したり、backend本体・履歴・設定をコピーしたりしない。

1. 機能変更と監査記録を独立レビューし、対象SHAの必須CIを通す。
   最終監査差分と通常DEV反映は承認済みですが、CI・配備成功を承認だけで代替しません。
2. `develop`へマージ後、そのSHAのCI・image buildを確認する。
3. 既存のDEV配備手順でbackend/MCPとKongの結果を確認する。
   一般task/activity追加とサーバー修正は、ZIPの更新だけでは接続先に反映されない。
4. そのソースから `python plugins/scripts/build_packages.py --output <新規の絶対パス>` を実行する。
5. 公開用リポジトリのGitHub Release `econipass-mcp-plugin-v1.2.0` に37 ZIPと`release.json`を添付する。
   リリースノートに対象SHA、DEV配備結果、未実施の実機受入を記載する。
   v1.1.0のtag・assetは変更せず、新しいreleaseへ公開する。`release.json`の
   `source_binding`・対応表hash・37 ZIPのhashを公開後の匿名取得で照合する。
6. 利用者は自分の環境のZIPを取得して同梱READMEに従い、OAuth認証する。
   認証情報はZIP・リリースノート・リポジトリに含めない。

Git marketplaceでは公開用リポジトリを登録する。公開ZIPとGit内のプラグインを
同じ原本から生成し、公開するファイルに秘密情報・利用者データ・ローカル絶対pathが
含まれないことを確認する。tool対応表のソースpathとhashは追跡用メタデータとして維持する。

## 公開ディレクトリへの申請準備

Claude公式ディレクトリはLICENSE不足で停止中です。ライセンス適用の保留中は
MIT候補のアップロード、許諾の申告、掲載申請を進めません。ローカルCLIのmanifest検証はエラー・警告0でも、directory検証はLICENSE_MISSINGでblocking error 1件となる。manifest検証の成功は
この掲載条件を満たしたことを意味しません。

正式な公開者情報、公開対象環境、審査専用テナントを申請前に確定する。
現在のDEV配布物を本番向けとして申請したり、既存利用者のアカウントを審査に流用したりしない。
manifestの`EcoNiPass`という表示名は、公開者の本人確認・組織確認が済んだことを意味しない。

OpenAIの申請では、確認済みの公開者と申請権限、公開情報、審査用接続手段、
操作説明を提出し、審査承認後に公開操作を行う。
[公式の申請手順](https://developers.openai.com/plugins/deploy/submission)を正本とする。
Claude Code / CodexのGitマーケットプレイス経由の配布や、
Geminiのローカル拡張登録とは別の手続きである。

| 申請項目 | 準備状況 |
| --- | --- |
| 名前・説明・カテゴリ・開始プロンプト | `econipass/plugin.json`に収録 |
| MCP接続・7スキル | 共通ZIPに収録。DEV接続 |
| 正式な公開者・確認済み開発者の選択 | 未提供 |
| 会社・プライバシー・サポート等の公開URL | 申請に使う正式URLを要確定 |
| 公開対象環境と公開範囲 | DEV配布のみ準備。本番公開は未確定 |
| 審査専用アカウントとサンプルテナント | 未提供。秘密情報は申請先の専用欄へ |
| 操作動画・審査用実行結果 | 専用テナント準備後に作成 |
| 適合性の申告・審査承認・公開操作 | 未実施 |

## 審査・利用環境で確認する操作

審査用データで、次の順序と拒否条件を確認する。通常利用者のデータを変更しない。

1. `setup`を開始し、認証、所属事業所、実際の`tools/list`とscopeを確認する。
2. EMSの計測値・管理設定・監視イベント・共有報告を参照する。
   許可外事業所と不足scopeでは拒否されることを確認する。
3. EMS更新は`dry_run=true`で内容を確認し、利用者の明示確認後、
   同一payloadと確認tokenで1回実行して結果を読み戻す。
   topology planのnative preview自体にも更新権限と確認が必要。
4. task/activityは実在する対象の現在状態と独自項目定義を取得し、previewからの
   競合拒否・更新・コメント・readbackを専用サンプルで確認する。
5. CFPは5種のうち対象のExcelを取得し、対象事業所・期間・置換範囲を確認する。
   専用サンプルの投入をプレビュー、確認、実行、履歴照会の順に検証する。
6. tokenなし・期限切れ・payload変更・他事業所で更新が拒否されることを確認する。
   結果不明の更新を自動再試行しない。
7. OAuth更新・失効・再認証と、生成した添付ファイルの保存を検証する。

各環境の実機結果は `platform-support.json` の受入状態と分けて記録する。
オフラインのZIP検証、CI成功、公開HTTP応答だけで上記の完了を判断しない。
