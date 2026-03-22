---
layout: default
title: "Building GitInflow: Technical Decisions Behind the App"
date: 2026-03-22
lang: en
---

# Building GitInflow: Technical Decisions Behind the App

*March 22, 2026*

GitInflow went from idea to App Store in a single sprint. Here's a look at the key technical decisions we made along the way.

## Architecture: SwiftUI + MVVM + No Backend

The entire app runs on two things: **SwiftUI** and the **GitHub REST API**. No custom backend, no database, no sync engine.

```
SwiftUI Views
  → ViewModels (@MainActor, ObservableObject)
    → Services (GitHubAPIClient, StatusService, CacheService)
      → GitHub REST API v3
```

This simplicity is intentional. Every piece of data lives on GitHub. The app is just a view layer with local caching.

## Kanban via Labels

The kanban system uses GitHub labels (`status:ready`, `status:inProgress`, `status:done`) instead of GitHub Projects. Why?

1. **No API complexity** — Labels are a single field on the Issue object
2. **Universal** — Works with any GitHub client, CLI tool, or automation
3. **Auto-creation** — GitInflow creates missing labels on first use via `POST /repos/{owner}/{repo}/labels`

When you move an issue to "Done", the app does two things in sequence: updates the labels, then closes the issue. Moving back reopens it.

## Multi-Repository: TaskGroup for Parallel Fetching

One of the most impactful features is viewing issues across up to 5 repositories at once. This is implemented with Swift's `withTaskGroup`:

```swift
await withTaskGroup(of: (Repository, Result<[Issue], Error>).self) { group in
    for repo in repos {
        group.addTask {
            do {
                var fetched = try await self.apiClient.fetchIssues(...)
                // Filter PRs, assign repoFullName
                return (repo, .success(fetched))
            } catch {
                return (repo, .failure(error))
            }
        }
    }
    // Merge results, track failures
}
```

Partial failures are tracked separately — if one repo fails, the others still display. An error banner shows which repo failed with a retry button.

## OAuth Security: Server-Side Token Exchange

The initial implementation had the OAuth client secret embedded in the app binary. This is a common pattern but fundamentally insecure — anyone can extract it with `strings`.

We moved token exchange to a **Cloudflare Worker**:

```
App → sends auth code → Cloudflare Worker → exchanges for token → returns token to app
```

The worker holds the client secret via `wrangler secret`. The app never sees it. Total cost: $0 (Cloudflare free tier).

## Share Extension: App Group + Keychain Sharing

The Share Extension runs as a separate process. It needs two things from the main app:

1. **OAuth token** — Shared via Keychain Access Group
2. **Selected repositories** — Shared via App Group UserDefaults

This required careful entitlement configuration:
- Both targets need `keychain-access-groups` with `$(AppIdentifierPrefix)com.gitinflow.GitInflow`
- Both targets need `com.apple.security.application-groups` with `group.com.gitinflow.shared`

## Localization: String Catalogs

Rather than maintaining `.strings` files, we use Xcode's **String Catalog** format (`.xcstrings`). SwiftUI's `Text("日本語")` automatically looks up translations in the catalog — no code changes needed for most strings.

For non-SwiftUI contexts (error messages, notifications), we use `String(localized:)`.

## Widget: WidgetKit + App Group

The widget reads issue counts from App Group UserDefaults. The main app writes these counts after each fetch:

```swift
private func updateWidgetData() {
    let defaults = UserDefaults(suiteName: AppConfig.appGroupID)
    defaults?.set(backlogCount, forKey: "widget_backlog_count")
    // ...
    WidgetCenter.shared.reloadAllTimelines()
}
```

Simple, reliable, no background networking required.

## What We'd Do Differently

- **Pagination from day one** — We added it later, but the 100-item limit bit us early in testing
- **Protocol-first services** — We retrofitted `StatusServiceProtocol` and `AuthServiceProtocol`; should have started with them
- **Offline support** — Not yet implemented, but the caching infrastructure is there

## Stack Summary

| Component | Technology |
|-----------|-----------|
| UI | SwiftUI (iOS 17+) |
| Architecture | MVVM + @MainActor |
| Networking | URLSession + async/await |
| Concurrency | TaskGroup (parallel fetch) |
| Auth | OAuth + Cloudflare Workers |
| Storage | Keychain (tokens), UserDefaults (preferences) |
| Extensions | Share Extension, WidgetKit |
| Localization | String Catalogs (.xcstrings) |
| Build | xcodegen (project.yml) |

---

*Interested in the code? GitInflow is built in the open. Questions and feedback welcome at [gitinflow@hakaru.net](mailto:gitinflow@hakaru.net).*
