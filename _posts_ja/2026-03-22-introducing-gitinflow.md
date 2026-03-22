---
layout: default
title: "GitInflow リリース：GitHub Issue をカンバンボードに"
date: 2026-03-22
lang: ja
---

# GitInflow リリース：GitHub Issue をカンバンボードに

*2026年3月22日*

**GitInflow** をリリースしました。GitHub Issue をカンバン方式で管理する iOS アプリです。追加ツール不要で、GitHub だけでタスク管理が完結します。

## なぜ GitInflow を作ったのか

GitHub Issue でタスクを管理している開発者は多いと思います。しかし GitHub のモバイルアプリはコードレビュー向けで、タスク管理には物足りない。

GitInflow はその隙間を埋めます。iPhone 上で**カンバンボード**を使い、GitHub Issue とラベルだけでワークフローを回せます。独自バックエンドもデータベースも不要です。

## 仕組み

GitInflow は GitHub ラベルでステータスを表現します：

- **Backlog** — ステータスラベルなし（受信トレイ）
- **Ready** — `status:ready` — トリアージ済み、着手可能
- **In Progress** — `status:inProgress` — 作業中
- **Done** — `status:done` — 完了（Issue は自動クローズ）

Issue を右スワイプで次のステータスに進め、左スワイプで戻す。それだけです。

## 主な機能

### マルチリポジトリ
最大5つのリポジトリを選択し、カンバンビューで一元管理。タブ上部のフィルタチップでリポジトリごとに絞り込めます。

### クイックトリアージ
スワイプアクションでステータス変更、ラベル追加、マイルストーン設定、コメント追加。リストビューから離れずにすべて完了。

### スマート共有シート
ブラウザで見つけた記事やSlackのバグ報告を、共有シート経由で直接 GitHub Issue に。

### ウィジェット
ホーム画面ウィジェットで In Progress の件数を一目で確認。Medium サイズなら全ステータスの件数が見えます。

### プライバシー重視
データはデバイスと GitHub の間だけ。アナリティクスもトラッキングもなし。OAuth トークンは iOS Keychain に保存、トークン交換は Cloudflare Worker 経由。

## はじめよう

1. App Store から GitInflow をダウンロード
2. GitHub アカウントでログイン
3. 設定でリポジトリを選択
4. スワイプ開始！

自分たちが欲しかったアプリを作りました。ぜひお試しください。

---

*フィードバックは [GitHub Issues](https://github.com/hakaru/GitInflow-support/issues) または [gitinflow@hakaru.net](mailto:gitinflow@hakaru.net) まで。*
