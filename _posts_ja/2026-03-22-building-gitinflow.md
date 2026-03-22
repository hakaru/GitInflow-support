---
layout: default
title: "GitInflow の技術的な裏側"
date: 2026-03-22
lang: ja
---

# GitInflow の技術的な裏側

*2026年3月22日*

GitInflow はアイデアから App Store まで一気に作り上げました。その過程で下した技術的な判断を紹介します。

## アーキテクチャ：SwiftUI + MVVM + バックエンドなし

アプリ全体が **SwiftUI** と **GitHub REST API** の2つだけで動きます。カスタムバックエンドもデータベースも同期エンジンもなし。

```
SwiftUI Views
  → ViewModels (@MainActor, ObservableObject)
    → Services (GitHubAPIClient, StatusService, CacheService)
      → GitHub REST API v3
```

このシンプルさは意図的です。すべてのデータは GitHub に存在し、アプリはローカルキャッシュ付きのビューレイヤーに過ぎません。

## ラベルによるカンバン

カンバンシステムは GitHub ラベル（`status:ready`、`status:inProgress`、`status:done`）を使います。GitHub Projects ではなくラベルを選んだ理由：

1. **API がシンプル** — ラベルは Issue オブジェクトの1フィールド
2. **汎用的** — GitHub CLI や他のツール、自動化とも連携可能
3. **自動作成** — 初回使用時に `POST /repos/{owner}/{repo}/labels` でラベルを自動生成

Issue を「Done」に移動すると、アプリは2つの操作を順番に実行：ラベル更新 → Issue クローズ。戻すと再オープン。

## マルチリポジトリ：TaskGroup による並列フェッチ

最大5リポジトリの Issue を一画面で見る機能は、Swift の `withTaskGroup` で実装しています：

```swift
await withTaskGroup(of: (Repository, Result<[Issue], Error>).self) { group in
    for repo in repos {
        group.addTask {
            do {
                var fetched = try await self.apiClient.fetchIssues(...)
                // PR除外、repoFullName付与
                return (repo, .success(fetched))
            } catch {
                return (repo, .failure(error))
            }
        }
    }
    // 結果をマージ、失敗を記録
}
```

部分的な失敗は個別に追跡。1つのリポジトリが失敗しても他は正常に表示され、エラーバナーに再試行ボタンが出ます。

## OAuth セキュリティ：サーバーサイドでのトークン交換

当初は OAuth クライアントシークレットをアプリバイナリに埋め込んでいました。よくあるパターンですが根本的に安全ではなく、`strings` コマンドで抽出できてしまいます。

トークン交換を **Cloudflare Worker** に移しました：

```
アプリ → 認証コードを送信 → Cloudflare Worker → トークンに交換 → アプリに返す
```

Worker が `wrangler secret` でシークレットを保持。アプリはシークレットを一切見ません。コスト：$0（Cloudflare 無料枠）。

## Share Extension：App Group + Keychain 共有

Share Extension は別プロセスとして動きます。メインアプリから2つのものが必要：

1. **OAuth トークン** — Keychain Access Group で共有
2. **選択中リポジトリ** — App Group UserDefaults で共有

エンタイトルメントの設定が肝心：
- 両ターゲットに `keychain-access-groups`（`$(AppIdentifierPrefix)com.gitinflow.GitInflow`）
- 両ターゲットに `com.apple.security.application-groups`（`group.com.gitinflow.shared`）

## ローカライゼーション：String Catalogs

`.strings` ファイルの管理ではなく、Xcode の **String Catalog** 形式（`.xcstrings`）を採用。SwiftUI の `Text("日本語")` がカタログの翻訳を自動で参照するため、ほとんどのコード変更が不要。

非 SwiftUI コンテキスト（エラーメッセージ、通知）では `String(localized:)` を使用。

## ウィジェット：WidgetKit + App Group

ウィジェットは App Group UserDefaults から Issue 件数を読み取ります。メインアプリがフェッチ後に書き込み：

```swift
private func updateWidgetData() {
    let defaults = UserDefaults(suiteName: AppConfig.appGroupID)
    defaults?.set(backlogCount, forKey: "widget_backlog_count")
    // ...
    WidgetCenter.shared.reloadAllTimelines()
}
```

シンプルで確実。バックグラウンドネットワークは不要。

## やり直すなら

- **ページネーションは最初から** — 後付けしたが、テスト中に100件制限に引っかかった
- **プロトコルファースト** — `StatusServiceProtocol` を後から追加した。最初から作るべきだった
- **オフラインサポート** — 未実装だがキャッシュ基盤は整っている

## 技術スタック一覧

| コンポーネント | 技術 |
|-------------|------|
| UI | SwiftUI (iOS 17+) |
| アーキテクチャ | MVVM + @MainActor |
| ネットワーク | URLSession + async/await |
| 並行処理 | TaskGroup（並列フェッチ） |
| 認証 | OAuth + Cloudflare Workers |
| ストレージ | Keychain（トークン）、UserDefaults（設定） |
| 拡張 | Share Extension, WidgetKit |
| ローカライゼーション | String Catalogs (.xcstrings) |
| ビルド | xcodegen (project.yml) |

---

*質問やフィードバックは [gitinflow@hakaru.net](mailto:gitinflow@hakaru.net) まで。*
