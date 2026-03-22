---
layout: default
title: User Manual
lang: en
---

# GitInflow User Manual

GitInflow is a GitHub Issue kanban client for iOS. This manual covers all features in detail.

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Kanban Tabs](#kanban-tabs)
3. [Changing Status](#changing-status)
4. [Search](#search)
5. [Repository Filter](#repository-filter)
6. [Creating Issues](#creating-issues)
7. [Issue Detail](#issue-detail)
8. [Labels & Milestones](#labels--milestones)
9. [Comments](#comments)
10. [Share Extension](#share-extension)
11. [Pull Requests Tab](#pull-requests-tab)
12. [Widget](#widget)
13. [Notifications](#notifications)
14. [Settings](#settings)
15. [Error Handling](#error-handling)
16. [FAQ](#faq)

---

## Getting Started

### Login

1. Launch GitInflow.
2. Tap **"Sign in with GitHub"** on the login screen.
3. Authenticate in the browser or via GitHub's app. GitInflow uses OAuth and never stores your password.

### Select Repositories

1. After login, go to the **Settings** tab (gear icon).
2. Tap repositories to select them. Selected repos are checked.
3. You can select **up to 5 repositories** at once.

### Set a Default Repository

In the Settings tab, tap the **star icon** next to a repository to mark it as the default. The default repository is used when:
- Creating a new issue via the **+** button
- Using the **Share Extension** when no repo is manually chosen

---

## Kanban Tabs

GitInflow organizes issues into four status columns, each represented by a tab:

| Tab | Description | GitHub Label |
|-----|-------------|--------------|
| **Backlog** | Issues with no status label — the inbox for new work | *(no label)* |
| **Ready** | Issues that are triaged and ready to start | `status:ready` |
| **In Progress** | Issues actively being worked on | `status:inProgress` |
| **Done** | Completed issues — automatically closed on GitHub | `status:done` |

Tap any tab to switch to it. Each tab shows only the issues matching that status from your selected repositories.

---

## Changing Status

There are four ways to change an issue's status:

### Swipe Left — Add / Advance

Swipe an issue card **to the left** to reveal quick actions:

- **Label** — Open the label picker sheet
- **Milestone** — Open the milestone picker sheet
- **Advance** — Move the issue to the next status (e.g., Backlog → Ready → In Progress → Done)

### Swipe Right — Retreat / Comment

Swipe an issue card **to the right** to reveal:

- **Retreat** — Move the issue back to the previous status (e.g., In Progress → Ready)
- **Comment** — Open a comment sheet to add a comment to the issue

### Context Menu (Long Press)

Long-press any issue card to open a context menu with all available status options. This lets you jump directly to any status without swiping multiple times.

### Issue Detail Buttons

Tap an issue to open the **Issue Detail** screen. Status change buttons are displayed at the bottom of the screen — tap **Advance** or **Retreat** to move the issue.

---

## Search

Each kanban tab has a **search bar** at the top. Tap it to filter issues in the current tab by keyword.

- Search matches issue **titles**.
- The search is local (no extra network request) and updates in real time as you type.
- Clearing the search bar restores the full list.

---

## Repository Filter

When you have **two or more repositories** selected in Settings, a row of **filter chips** appears below the tab bar on the kanban screen.

- Tap a chip to show issues from that repository only.
- Tap **All** (the leftmost chip) to show issues from all selected repositories.
- The filter applies to the current tab only; switching tabs keeps your filter selection.

---

## Creating Issues

1. Navigate to any kanban tab (the **+** button is always visible in the top-right corner).
2. Tap **+**.
3. If you have multiple repositories selected, a **repository picker** appears — choose the target repo. If you have a default repo set, it is pre-selected.
4. Enter a **title** (required) and an optional **body**.
5. Tap **Submit** to create the issue on GitHub. The new issue appears in the **Backlog** tab.

---

## Issue Detail

Tap any issue card to open its detail screen. The detail screen shows:

- **Title** — Issue title and number
- **Status badge** — Current kanban status (Backlog / Ready / In Progress / Done)
- **Labels** — All labels assigned to the issue
- **Milestone** — Assigned milestone, if any
- **Body** — Issue description (rendered as plain text)
- **Comments** — All existing comments in chronological order
- **Status change buttons** — Advance and Retreat buttons at the bottom

From the detail screen you can:
- Read the full issue description and all comments
- Change status using the Advance / Retreat buttons
- Add a comment (see [Comments](#comments))

---

## Labels & Milestones

### Adding a Label via Swipe

1. Swipe an issue card **to the left**.
2. Tap the **Label** action.
3. A picker sheet appears with all labels in the issue's repository.
4. Tap a label to toggle it on or off.
5. Tap **Done** to apply.

### Adding a Milestone via Swipe

1. Swipe an issue card **to the left**.
2. Tap the **Milestone** action.
3. A picker sheet appears with all open milestones in the repository.
4. Tap a milestone to assign it, or tap **None** to remove the current milestone.
5. Tap **Done** to apply.

> **Note:** Labels and milestones are fetched from GitHub and reflect what exists in that repository. Create labels and milestones on GitHub.com or the GitHub app first.

---

## Comments

### Adding a Comment via Swipe

1. Swipe an issue card **to the right**.
2. Tap the **Comment** action.
3. A comment sheet appears. Type your comment.
4. Tap **Post** to submit.

### Adding a Comment from Issue Detail

1. Tap an issue to open the detail screen.
2. Scroll to the bottom of the comments list.
3. Tap the **Add Comment** field.
4. Type your comment and tap **Post**.

---

## Share Extension

The Share Extension lets you create or update GitHub Issues directly from any app — browser, Notes, Safari, etc.

### Activating the Share Extension

1. In any app, tap the **Share** button (box with arrow).
2. Scroll the share sheet and tap **GitInflow Share**. If it does not appear, tap **More** and enable it.

### New Issue Mode

1. In the Share Extension, select **New Issue** from the mode picker.
2. Choose a repository (your default repo is pre-selected).
3. The shared content (URL, selected text, image) is pre-filled in the body.
4. Edit the title and body as needed.
5. Tap **Create** to post the issue.

### Append to Existing Mode

1. Select **Append to Existing** from the mode picker.
2. Choose a repository.
3. A list of open issues in that repository appears — tap the issue you want to append to.
4. The shared content is pre-filled as a comment.
5. Tap **Post** to add the comment.

### Show All Repos Toggle

By default, the Share Extension shows only your **default repository**. Enable the **"Show All Repos"** toggle in the Share Extension to see all selected repositories and pick any of them.

### Default Repository in Share Extension

The default repository set in Settings is pre-selected in the Share Extension, making one-tap issue creation possible.

---

## Pull Requests Tab

Tap the **PRs** tab (at the bottom navigation bar) to see all open pull requests from your selected repositories.

- Each row shows the PR title, repository, and author.
- Tap a PR to open it in Safari (GitHub web).
- When multiple repositories are selected, use the **repository filter chips** (same as the kanban screen) to filter by repo.

> Pull requests are read-only in GitInflow. Use GitHub.com or the GitHub app to review and merge PRs.

---

## Widget

GitInflow provides a home screen widget that shows your issue counts at a glance.

### Widget Sizes

| Size | Content |
|------|---------|
| **Small** | Count of **In Progress** issues |
| **Medium** | Counts for all four statuses: Backlog / Ready / In Progress / Done |

### Adding the Widget

1. Long-press an empty area on your home screen.
2. Tap **+** (top-left corner) to open the widget gallery.
3. Search for **GitInflow**.
4. Select **Small** or **Medium**.
5. Tap **Add Widget** and position it.

### Widget Behavior

- The widget refreshes periodically in the background (iOS controls the exact interval).
- Tapping the widget opens GitInflow on the kanban screen.

---

## Notifications

GitInflow can send **local notifications** when new issues appear in your selected repositories.

- Notifications are generated when GitInflow refreshes issue data (either in the foreground or background).
- New issues that were not present on the previous refresh trigger a notification.
- Tap a notification to open GitInflow directly to the relevant issue.

### Enabling Notifications

iOS will prompt you to allow notifications on first launch. If you declined, go to **iOS Settings → GitInflow → Notifications** and enable them.

---

## Settings

Open the **Settings** tab (gear icon) to manage:

### Repository Selection

- Tap any repository in the list to **select or deselect** it.
- A checkmark indicates a selected repository.
- You can select up to **5 repositories**.

### Default Repository

- Tap the **star icon** next to a repository to set it as the default.
- The star turns filled/yellow on the selected default.
- Only one default can be set at a time.

### Privacy Policy

- A link to the GitInflow Privacy Policy is available in Settings.

### Logout

- Tap **Logout** (at the bottom of Settings) to sign out of your GitHub account.
- All locally cached data is cleared on logout.

---

## Error Handling

### Failed Repository Banner

If GitInflow cannot load issues from a repository (e.g., network error, revoked access), a **red error banner** appears at the top of the kanban screen showing which repository failed.

### Retry Button

Tap the **Retry** button in the error banner to immediately re-fetch issues from the failed repository. If the problem persists, check your internet connection or verify that the GitHub token still has access to that repository (re-login if needed).

---

## FAQ

**Q: How many repositories can I select?**
Up to 5 repositories can be selected at a time in Settings.

**Q: What does "Done" status do on GitHub?**
When you move an issue to Done, GitInflow adds the `status:done` label and **closes** the issue on GitHub. Moving it back to any other status reopens the issue.

**Q: Can I use GitInflow with private repositories?**
Yes. GitInflow uses your GitHub OAuth token which has access to all repositories you authorized during login. Private repos appear alongside public repos in Settings.

**Q: The Share Extension is not showing up. What do I do?**
In the share sheet, tap **More** (or scroll right to find Edit), find GitInflow Share in the list, and enable it.

**Q: Why are my labels or milestones not showing?**
Labels and milestones are fetched from GitHub. If none appear, make sure the repository has labels and milestones created on GitHub, and that you have network access.

**Q: Why isn't the widget updating?**
Widgets on iOS refresh on a schedule managed by the system. Open GitInflow at least once to trigger a data refresh, and the widget will update shortly after.

**Q: How do I change which repositories appear in the widget?**
The widget reflects the repositories selected in Settings. Add or remove repos in Settings, and the widget will update on its next refresh.

**Q: I accidentally moved an issue to Done. How do I undo it?**
Swipe the issue card to the right in the Done tab and tap **Retreat**, or long-press the card and select a status from the context menu. This removes the `status:done` label and reopens the issue on GitHub.
