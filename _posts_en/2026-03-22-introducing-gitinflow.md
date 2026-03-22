---
layout: default
title: "Introducing GitInflow: GitHub Issues as Your Kanban Board"
date: 2026-03-22
lang: en
---

# Introducing GitInflow: GitHub Issues as Your Kanban Board

*March 22, 2026*

We're excited to announce **GitInflow**, a new iOS app that turns GitHub Issues into a full kanban workflow — no extra tools required.

## Why GitInflow?

If you're a developer who uses GitHub Issues to track tasks, you've probably wished for a more visual way to manage them on your phone. GitHub's mobile app is great for code review, but for task management? Not so much.

GitInflow fills that gap. It gives you a **kanban board** directly on your iPhone, powered entirely by GitHub Issues and labels. No extra backend, no proprietary data store — just GitHub.

## How It Works

GitInflow uses GitHub labels to represent status:

- **Backlog** — Issues with no status label (your inbox)
- **Ready** — `status:ready` — triaged and ready to work on
- **In Progress** — `status:inProgress` — actively working
- **Done** — `status:done` — completed (auto-closes the issue)

Swipe an issue to the right to advance it. Swipe left to move it back. That's it.

## Key Features

### Multi-Repository Support
Select up to 5 repositories and see all their issues in one unified kanban view. Filter by repo using chips at the top of each tab.

### Quick Triage
Swipe actions let you change status, add labels, set milestones, and leave comments — all without leaving the list view.

### Smart Share Sheet
See an interesting article? A bug report in Slack? Share it directly to GitInflow to create a GitHub Issue in seconds.

### Widget
Add a home screen widget to see your In Progress count at a glance. The medium widget shows counts for all four statuses.

### Privacy-First
Your data stays between your device and GitHub. No analytics, no tracking, no third-party servers. OAuth tokens are stored in the iOS Keychain, and token exchange happens through a secure Cloudflare Worker.

## Getting Started

1. Download GitInflow from the App Store
2. Log in with your GitHub account
3. Select your repositories in Settings
4. Start swiping!

We built GitInflow because we needed it ourselves. We hope you find it useful too.

---

*Have feedback? [Open an issue](https://github.com/hakaru/GitInflow-support/issues) or email us at [gitinflow@hakaru.net](mailto:gitinflow@hakaru.net).*
