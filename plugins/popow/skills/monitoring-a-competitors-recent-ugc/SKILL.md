---
name: monitoring-a-competitors-recent-ugc
description: "Use when the user asks how much recent TikTok or Instagram Reels UGC a named brand gets, who creates it, or which videos account for its views."
metadata:
  harness-level: L2
  layer: use-case
---

## Search the requested period

Use the last 90 days ending today unless the user specifies a period. The brand name is required. Apply any requested platform, market and language. Follow “Before searching” in finding-references.

For this overview, use the following search depth in place of the single search in searching-live-videos:

- Call `search_live_posts` with the period, `pages: 3`, and 8–12 phrases spanning the brand name, product, brand and partner hashtags, and relevant category terms. Search every available platform within scope.
- Keep in-period videos whose caption, hashtags, on-screen text or speech names the brand. A search hit or platform-generated summary alone is insufficient. Identify the brand's own handles and retain their videos.
- Repeat with the same phrases and all previously returned post IDs in `exclude_post_ids`. A failed phrase can be retried once. Stop when a round adds fewer than five new qualifying videos, after four rounds, or when the next call would exceed the exclusion limit.

## Check the top creators

Rank non-official creator accounts by combined views across the kept videos. For the top five, use looking-up-creators with `recent_posts: 30` and the brand's name and spellings in `mention_words`. Add previously unseen, in-period posts returned with `mentions: true`. For a spotlight reason, use the returned `recent_posts.mentioning` out of `recent_posts.posts.length` as a caption-match count. Describe these as the latest posts only when `recent_posts.complete` is true.

## Deliver the overview

If no videos qualify, report zero confirmed matches, the period and any search limits. Otherwise use `show_web_videos` once with `layout: brand`, the period, official handles and the collected video IDs. If the combined set exceeds the tool's capacity, keep the most-viewed videos and disclose the cutoff.

Choose spotlight videos for what they reveal about this brand. Give a reason grounded in a result, such as a video's recorded views or its creator's caption-match count. In `brand.limitations`, record the phrases and platforms searched, candidates read, matches found, failed searches or account reads, and the stopping reason.

The overview supplies the totals. In three to five lines, explain what stands out and what the search could have missed. On request, use searching-live-videos for comments, starting-from-a-video for a closer look, or managing-memory and writing-content-briefs to turn saved evidence into a brief. Look up business figures only when asked.

## Anti-Patterns

- Inferring sponsorship from views or crediting a format for a video's performance without evidence.
