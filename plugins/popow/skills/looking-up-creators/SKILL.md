---
name: looking-up-creators
description: "Use when the user asks about one specific TikTok or Instagram account, picked from search results or named by handle or profile link: its current follower count, or its newest posts with their dates, views and links, read live. Finding new creators uses finding-references; saving one uses managing-memory."
metadata:
  harness-level: L2
  layer: entity
---

`read_live_creator` reads one account from the platform at request time. Without it, say live account lookup is not connected; a video search result's creator fields and Popow's stored creator values are not a substitute.

## 1. Settle the one account

- From a search result: pass that video's `platform` and `creator.handle` unchanged.
- Named by the user: pass the handle or profile link they gave. If they gave only a display name, or the platform is unclear, ask which account instead of guessing a handle.
- Several accounts: look up only the ones the user chose, one call each. Do not look up every creator in a search result.

## 2. Ask for what the user asked for

- Follower count or account facts only: omit `recent_posts`.
- Recent posts: pass the number the user asked for. There is no default; if they asked for "recent posts" without a number and the number changes the answer, ask.
- Posts that name a brand or product: also pass `mention_words` with its name and spellings.
- Request once. Do not call again to "check" a result; a repeat call is billed and reads the same profile.

## 3. Report what was read

Give, for the account: handle, profile link, follower count, and that it was read live at `observed_at`. For each post: original link, author, publication date and view count. State the coverage in the same answer: whether the posts are confirmed as the newest (`recent_posts.complete`), how many were read against how many were asked for, and every line of `limitations`. When the user asked about "posts" on Instagram, say the list is Reels.

Keep live values apart from stored ones: a follower count in a library search result is what Popow recorded earlier, and this one is what the platform returned now. Publication date and observation time are different facts; give both when the user compares numbers.

When this account came from a search result, compare `account.platform_account_id` with that result's `creator.platform_account_id`. If they differ, the handle now belongs to another account: say so and do not merge the two.

## Anti-Patterns

- Treating the videos a search returned for an account as its newest posts.
- Filling a missing follower count, date or view count from another platform, a stored value or an estimate.
- Judging whether the creator fits a brief, deduplicating a list, or drafting outreach here; hand those back to the request that needs them.
