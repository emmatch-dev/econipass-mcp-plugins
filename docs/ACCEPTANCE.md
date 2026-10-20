# DEV 1.1.0 の実機受入・公式掲載状況

確認日: 2026-10-21 JST。接続先は `https://api.dev.app.econipass.com/mcp`。
配布版のbackendソースは `37284f6c8f17175984ded533bea471693443aada`。
このページに記載したクライアント・操作以外の実機成功を意味しません。

## 確認できたこと

| 対象 | 実施内容 | 結果 |
| --- | --- | --- |
| Codex desktopの既存EcoNiPass接続 | 認証済み組織一覧・EMSサイト一覧の取得 | 成功。業務データは本リポジトリに保存しない |
| 同じ接続の更新scope不足 | EMSサイト作成の`dry_run=true`を要求 | 更新権限不足として拒否。確認tokenの発行・更新実行なし |
| Codex CLI 0.163.0-alpha.10.2 | 専用設定ディレクトリでmarketplace登録、plugin導入、native一覧・詳細の照会 | 1.1.0、7スキル有効、MCP設定1件を確認。通信を遮断した読み込み検証 |
| Claude Code 2.1.299 | 専用設定・`--plugin-dir`でnative検証と詳細照会 | エラー0、警告0、1.1.0、7スキル、MCP設定1件。通信を遮断した読み込み検証 |
| Codex desktopのCFP入力Excel取得 | master / base_unit / activity_amount / pcf_certification_period / aist_idea | 5種類ともbackend HTTP 500。ファイルの受領なし |
| DEV Web画面のCFPマスタ取得 | 既存ログインで標準ダウンロード操作 | HTTP 500 / E000003。同じ問題を再現 |

CLIの読み込み検証は公開配布ソースとファイルハッシュを照合して実施しました。
既存ユーザー設定・認証情報を変更していません。MCP接続済みのCodex desktopでの
参照成功と、配布プラグインのCLI読み込みは別の証跡です。

CFPのMCP応答には`INVALID_ARGUMENT`と表示されますが、上流HTTP 500であり、
利用者の入力ミスと断定していません。原因と修正は調査中です。

## 29環境の受入範囲

29件は[配布キットの製品別エントリ](../plugins/platform-support.json)です。
desktop / CLI / IDE / web / mobile / cloudで設定や実行経路が異なる場合、
それぞれの証跡が必要です。1つのsurfaceの成功を製品全体へ転記しません。

完了条件は、導入・7スキル読込、認証済みの実際のtool catalog、参照結果、
OAuth更新またはPAT rotation、専用grantの失効、scopeと事業所境界の拒否です。
更新を提供する構成では、専用fixtureでdry-run、対象と置換範囲の確認、
1回の実行・読み戻し・確認token再利用拒否まで確認します。
CFPは5種のファイル、添付受領、サイズ上限、既存データ保持も対象です。

全29環境の総合受入は未完了です。既存ユーザーの認証を失効させたり、
既存の業務データを置換したりして受入を成立させることはありません。
専用fixture・各サービスの利用可能なアカウント・必要な実機が準備できた範囲で続行します。

[環境ごとの確認状況](acceptance-summary.json)は、ローカルクライアントの所在と
実施済みの検査を分けて記録します。「未検出」は今回調べた端末の範囲であり、
製品がMCPに非対応であるという意味ではありません。

## 公式ディレクトリ

| 公開先 | 状況 |
| --- | --- |
| GitHub公開リポジトリ・Release | DEV 1.1.0を公開済み |
| MCP公式Registry | DEV専用の`io.github.emmatch-dev/econipass-dev`、`1.1.0-dev.1`を準備。公式CLIの検証成功。公開操作は未完了 |
| OpenAIのChatGPT / Codex公式ディレクトリ | 公開者確認が未完了のためZIP下書き作成前で停止。本番HTTPS URL、審査専用アカウント、動画等も必要 |
| Claudeディレクトリ | 申請ポータルへのログイン、専用審査環境、plugin内README・配布ライセンス等の準備が必要。申請未完了 |

MCP Registryの登録はOpenAIやClaudeの審査承認を意味しません。
現在のDEV URLを、本番URLや全29環境での受入完了として申告しません。
公開用アカウント・認証情報・審査用秘密情報は本リポジトリへ保存しません。

公式の申請要件:
[OpenAI](https://developers.openai.com/plugins/deploy/submission-errors)、
[Claude](https://code.claude.com/docs/en/plugins/publish)、
[MCP Registry](https://github.com/modelcontextprotocol/registry/tree/main/docs).
