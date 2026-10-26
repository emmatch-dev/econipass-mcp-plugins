# DEV 1.2.0日付検証修正候補の受入状況

この文書は **日付検証修正候補の配備・公開前の観測時点（2026-10-26T00:38:56.122704+00:00）の記録** です。旧f831のDraftと新83f9候補を区別します。後続の現行状況は[PR #5](https://github.com/emmatch-dev/econipass-mcp-plugins/pull/5)と[Releases](https://github.com/emmatch-dev/econipass-mcp-plugins/releases)で確認してください。

確認対象commit`6f09904ba5eedc0805b3895341b032f0770f807b`（日付実装e79417e3）、release SHA`83f900b69c53acea93f5dbdee7ddc1d7611acd324f23bae77790b40576e952bc`、対応表SHA`224f3ae9b21e1f3ea594b85d2d0e7cc161d593d36dd75ed6679e5aa6f7381065`。
37 ZIP・1,016エントリ・LICENSE/PDF0。新候補は未配備・未公開です。
[候補hash](candidate-package-v1.2.0-canonical-date-license-held-20261026.json)と[入力一致の範囲](candidate-native-equivalence-v1.2.0-canonical-date-license-held-20261026.json)、[機械記録](acceptance-summary.json)を正本にします。

## 実装・ローカル検証・監査

日付helperはnative DTOに合わせ`YYYY-MM-DD`だけを受け付け、compact／ISO週日付を確認発行前に拒否します。
既存日付・確認境界471件、plugins65件は各1まとめ起動・skip0で成功し、CI同版lintも成功しました。
旧95c監査3ファイルは承認を受け`1169e186`に反映済みです。その後の日付修正sourceには
新94378監査（patch SHA`94378fa474fe0644fbb13b9234df5e661e75a8387d87092aa8af7bf5aec95a4e`）も明示承認を受け`6f09904b`へ反映済みです。
新案の別checkout overlayで既存formal116件・skip0、actionlint27・YAML27・lintが成功しました。
固定30操作・8タグ・PRD STOPは維持し、CI・image・通常DEV・一般公開の成功へ読み替えません。

通常241／共有法定帳票254／最大256／固定PRD参照30はsource登録数で、実環境catalogの件数ではありません。
旧Linux377のMCP5,308成功・smoke6skip、synthetic E2E239成功＋想定拒否2、root210成功＋skip1、
実synthetic PG35成功は履歴です。今はsource14のうち日付helperとmapが変わっており、
新e794全体のLinux・CI・配備検証として継承しません。

## 配布候補と入力一致

旧f831比10 ZIPの各1entryが変わり、27 ZIPは完全同一です。差分は共通対応表9コピーと
Windsurf preset indexのmap SHAだけです。業務指示・7個別skill ZIP・native認証設定は同一です。
現在の公開原本から全37 ZIP・1,016entryを再生成し、全hash・CRC・entry bytesの一致を確認しました。公開HEADのcommit／pushを示す検証ではありません。

| 状態 | 環境数・範囲 |
| --- | --- |
| 限定確認 | 12。入力一致native8＋Claude Webスキル1、新規native metadata確認3 |
| 旧失敗保持 | Roo1。原因未確定、再試行なし |
| package load前blocked | 2。Linux Codexは試験環境準備timeout、QueryPie/Aruはimport前UI blocked。原因はどちらも未確定 |
| 他未実施 | 14。ChatGPT保留を含む |
| 総合受入・公開版業務受入 | 0／29 |

Cursor／VS Codeはharnessがnativeへ渡した設定JSONだけが一致し、whole ZIPは異なります。
他7nativeキットはwhole ZIPが一致（6限定成功とRoo失敗）します。
元の4whole-input不一致は保持し、そのうち3環境だけは新候補の実metadata検証で確認し直しました。
CodexもSKILL・manifest・MCP設定29/30entryは一致しますが、変更mapをnativeが読まなかったとは推定しません。
Claude Webは7個別ZIP・保存済みprovider wrapper7件の20ソースが一致し、新たなhostedスキルimport・UI観測は0です。
全source14やcommon30の同一性はfalseであり、旧全ZIP一致の記録を新候補へ差し替えません。

Linux Codexは試験環境の準備が180秒でtimeoutしました。package、runtime、image、container、native metadata試験は未実行です。
原因は未確定・再試行なしで、パッケージ不正やCodex不具合とは扱いません。cleanup-only回復は別review中で、完了を主張しません。

QueryPie系Aruの専用試験projectでは、ZIP・フォルダ選択後のnative controlsが無効のままで、import前に中止しました。
完了import0・原因未確定で、パッケージ不正やvendor不具合とは断定しません。新MCP接続・OAuth・モデル送信は0です。
組織catalog名・個人情報・私有画面は公開しません。

## 既存Codex接続の前駆環境baseline

既存接続だけで組織情報とEMS取込の読み取りが成功しました。CFPはmaster・base_unit・activity_amount・
pcf_certification_period・aist_ideaの5種類で原本を受領・保存し、応答のsize／SHAと一致、CRC・XMLを確認しました。
この接続には更新scopeがなく、投入previewはscope境界で拒否されました。確認token発行、投入・置換、native業務検証はありません。
EMSテンプレートもSIMPLE_KWHのCSV（6列）とXLSX（6シート）を実受領・保存し、応答SHAと一致、XLSXのCRC/XMLを確認しました。
新OAuthは0。顧客値・事業所ID・ファイル本体・ファイル名・顧客ファイルdigestは公開しません。
未配備の83f9候補や29環境の総合受入には加算しません。


新83f9の38資産stageとGET専用helperは用意済みで、386項目の独立レビューは指摘0です。
これはローカル準備と合成metadata14対照の確認で、新候補のDraft upload・live metadata・公開後匿名取得は未実施です。

## 公開・保留・履歴

GitHubで一般公開済みの版は1.1.0です。既存1.2.0 Draft ID423591210は旧f831の38資産を持ち、
対象public SHAはbda0b2ffです。新83f9はこのDraftへuploadしていません。旧候補・stage・assetsを変更していません。
LICENSE適用、新OAuth、ChatGPT受入を保留し、公式申請は未実施です。
ClaudeのLICENSE条件、OpenAIの公開者確認、Registryの組織認証・規約／CC0同意が未完了です。
旧common ZIPのmanifestエラー0は履歴です。今回のClaude Codeのfresh metadata検証もエラー／警告0ですが、
公式ディレクトリのLICENSE_MISSING blocking1は継続し、掲載申請の成功を意味しません。

旧f831の[pre-Draft時点記録](ACCEPTANCE-v1.2.0-candidate-355-f831-20261026.md)と
[同時点の機械記録](acceptance-summary-v1.2.0-candidate-355-f831-20261026.json)、
旧9640の[時点記録](history/ACCEPTANCE-v1.2.0-candidate-377-9640-20261026.md)を保持します。
旧candidate/native/equivalence JSONも変更しません。
