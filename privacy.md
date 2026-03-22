---
layout: default
title: Privacy Policy
lang: en
---

# Privacy Policy

**Last updated:** March 22, 2026

GitInflow ("the App") is developed by hakaru. This privacy policy explains how we handle your data.

## Data We Access

### GitHub Account Data
- The App accesses your GitHub account via OAuth authentication with the `repo` scope
- This provides read/write access to your repositories, issues, labels, milestones, and comments
- Authentication tokens are stored securely in the iOS Keychain
- Token exchange is performed via a secure server-side proxy (Cloudflare Workers) — your OAuth credentials never pass through third-party services

### Data Stored on Your Device
- **OAuth Token:** Stored in iOS Keychain (encrypted, hardware-protected)
- **Repository Preferences:** Selected repositories and default repository stored in UserDefaults
- **Issue Cache:** Temporary cache of issue data for display purposes

## Data We Do NOT Collect

- We do **not** collect, store, or transmit your personal data to any server
- We do **not** use analytics or tracking services
- We do **not** use advertising or ad tracking (no IDFA)
- We do **not** access your GitHub data for any purpose other than displaying it in the App

## Third-Party Services

- **GitHub API:** The App communicates directly with GitHub's REST API to fetch and manage your issues. GitHub's privacy policy applies to data stored on GitHub.
- **Cloudflare Workers:** Used solely for OAuth token exchange. No user data is stored or logged.

## Data Sharing

We do not share your data with any third parties.

## Data Deletion

- You can revoke the App's access to your GitHub account at any time from [GitHub Settings > Applications](https://github.com/settings/applications)
- Uninstalling the App removes all locally stored data including the OAuth token
- You can log out from the App's Settings tab to delete the stored token

## Children's Privacy

The App is not directed at children under 13.

## Contact

If you have questions about this privacy policy:

- **Email:** [gitinflow@hakaru.net](mailto:gitinflow@hakaru.net)

## Changes

We may update this privacy policy from time to time. Changes will be posted on this page with an updated date.
