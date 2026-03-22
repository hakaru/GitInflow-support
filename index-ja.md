---
layout: default
title: サポート
lang: ja
---

# GitInflow サポート

GitInflow は、GitHub Issue をカンバン方式で管理する iOS クライアントアプリです。複数リポジトリのタスクを横断的に管理できます。

## 主な機能

- **カンバンボード** — Backlog / Ready / In Progress / Done のステータスタブ
- **マルチリポジトリ** — 最大5個のリポジトリを選択して横断表示
- **クイックトリアージ** — スワイプでステータス変更、ラベル・マイルストーン・コメント追加
- **スマート共有シート** — 他のアプリから Share Extension で Issue 作成
- **Pull Requests** — PR 専用タブ
- **ウィジェット** — ホーム画面に Issue 数を表示
- **ローカル通知** — 新しい Issue の通知

---

## ユーザーマニュアル

はじめ方・カンバン操作・スワイプアクション・Share Extension・ウィジェット設定など、全機能を詳しく解説しています。

**[ユーザーマニュアルを読む →](manual/ja/)**

---

## よくある質問（FAQ）

**Q: リポジトリは何個まで選択できますか？**
一度に最大 5 つまで選択できます。設定タブでリポジトリをタップして選択してください。

**Q: Issue を Done に移動すると GitHub ではどうなりますか？**
GitInflow が `status:done` ラベルを付与して GitHub 上の Issue をクローズします。他のステータスに戻すと Issue は再オープンされます。

**Q: プライベートリポジトリでも使えますか？**
はい。ログイン時に認可したリポジトリであれば、プライベートリポジトリも設定画面に表示されます。

**Q: Share Extension が共有シートに表示されません。どうすればいいですか？**
共有シートで **その他** をタップし、「GitInflow Share」を見つけて有効にしてください。

**Q: ウィジェットが更新されないのはなぜですか？**
ウィジェットの更新スケジュールは iOS が管理しています。GitInflow を一度起動するとデータが更新され、まもなくウィジェットに反映されます。

**Q: 誤って Done にしてしまいました。元に戻せますか？**
Done タブで Issue カードを右にスワイプして **戻す（Retreat）** をタップするか、カードを長押ししてコンテキストメニューからステータスを選択してください。GitHub 上の Issue が再オープンされます。

---

## バグ報告・機能要望

- [バグを報告する](https://github.com/hakaru/GitInflow-support/issues/new?template=bug_report.yml)
- [機能を要望する](https://github.com/hakaru/GitInflow-support/issues/new?template=feature_request.yml)

## お問い合わせ

ご質問、フィードバック、サポートが必要な場合:

- **メール:** [gitinflow@hakaru.net](mailto:gitinflow@hakaru.net)
- **GitHub Issues:** [GitInflow-support](https://github.com/hakaru/GitInflow-support/issues)

## 動作要件

- iOS 17.0 以降
- GitHub アカウント
