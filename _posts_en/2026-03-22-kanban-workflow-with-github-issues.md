---
layout: default
title: "How to Run a Kanban Workflow with GitHub Issues"
date: 2026-03-22
lang: en
---

# How to Run a Kanban Workflow with GitHub Issues

*March 22, 2026*

You don't need Jira, Trello, or Linear to run a kanban workflow. If your code is already on GitHub, your task management can live there too. Here's how to set it up with GitInflow.

## The 4-Column Approach

A simple kanban board has four columns:

| Column | Meaning | When to use |
|--------|---------|-------------|
| **Backlog** | New ideas, bug reports, feature requests | When an issue is created but not yet prioritized |
| **Ready** | Triaged and ready to start | After you've decided this is worth doing soon |
| **In Progress** | Currently being worked on | When you start working on it |
| **Done** | Completed | When the work is finished |

## How GitInflow Maps This to GitHub

GitInflow uses **labels** to represent status:

- No label → **Backlog**
- `status:ready` → **Ready**
- `status:inProgress` → **In Progress**
- `status:done` → **Done** (issue is also closed)

This is the key insight: GitHub doesn't have built-in kanban columns, but labels are flexible enough to serve the same purpose. And since labels are part of the GitHub API, any tool can read and write them.

## A Typical Daily Workflow

### Morning: Triage Your Backlog

1. Open GitInflow → Backlog tab
2. Scan new issues that came in overnight
3. Swipe right on important ones to move them to **Ready**
4. Add labels and milestones as you go

### During the Day: Track Progress

1. Pick an issue from **Ready**, swipe to **In Progress**
2. Work on it
3. Leave comments via swipe actions for quick notes
4. When done, swipe to **Done** — the issue auto-closes on GitHub

### End of Day: Review

1. Check the **Done** tab — what did you accomplish?
2. Check **In Progress** — anything stuck?
3. Glance at the widget on your home screen for a quick count

## Tips for Multi-Repository Users

If you work across multiple repos (personal, work, side projects):

- **Select up to 5 repos** in Settings
- Use **filter chips** to focus on one repo at a time
- Set a **default repo** for quick issue creation
- The Share Extension respects your default repo too

## Why Labels Over GitHub Projects?

GitHub Projects is great for teams, but it's heavyweight for personal use:

- Labels are **universal** — they work with any GitHub tool
- Labels are **simple** — no board configuration needed
- Labels are **portable** — switch apps anytime, your data stays
- GitInflow creates the status labels automatically on first use

## Getting Started

1. Install GitInflow
2. Select your repos
3. Start triaging your Backlog
4. Build the habit: Backlog → Ready → In Progress → Done

It takes about 30 seconds to set up, and you'll never go back to unorganized issues.

---

*Questions about the kanban workflow? [Let us know](https://github.com/hakaru/GitInflow-support/issues).*
