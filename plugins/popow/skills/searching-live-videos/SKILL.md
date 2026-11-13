---
name: searching-live-videos
description: "Use with finding-references for every video reference request, whatever platform it names, when search_live_posts is connected; alone only when the user limits the search to live, Reels or live TikTok: short search phrases, a written checklist to judge each result, one gap-filling search, what viewers said on the picks, and grouping them for show_web_videos."
allowed-tools: mcp__popow__search_live_posts, mcp__popow__read_live_comments, mcp__popow__show_web_videos
metadata:
  harness-level: L2
  layer: entity
---

finding-references "Where to search" owns when to search one side only, and its "Before searching" owns when to ask first.

## 1. Write the checklist first

Before searching, write the checklist from the user's request, in their language, and keep it for the whole task:

- **Topic branches**: each alternative the user accepts, judged separately. "Using an astrology app or talking about their own sign" is two branches.
- **Required**: what every pick must have, such as language, creator-made UGC style or a named format.
- **Excluded**: topics or sources the user ruled out.

Keep this brief and use only requirements the user stated.

## 2. Search

Search once, covering every angle in that single call: each extra call costs a full judging round. Include app or product names only when the user's topic is that product. Keep one page per phrase; a response holds at most 80 videos, so search again with `exclude_post_ids` instead of asking for more pages. Use `conditions` only for date or view limits the user asked for. Pass `platforms` only when the user limits the search to one platform.

## 3. Judge every result

Judge the checklist from the returned fields. `is_ad` and `paid_partnership` describe promotion, not the creator-made format. Then decide:

- **Include**: at least one branch ○, every required item ○, no excluded item ○.
- **Wider**: at least one branch ○ and nothing × or excluded, but a required item unknown. Put it in "Also worth a look" (showing-videos) with what is unconfirmed.
- **Drop**: no branch ○, a required item ×, or an excluded item ○. Never drop for a reason not on the checklist.

Keep which branches matched; you will show them.

## 4. Fill gaps once

Search again, at most once, only if fewer videos passed than you will show (about 30).

## 5. Read what viewers said

When `read_live_comments` is connected, choose your picks as in step 6, then call it once; with more than 25 picks, send the 25 with the most comments. From each video note the situations, exact words and objections viewers bring up; treat `repeated_phrases` as part of the format. Comments explain why a pick is worth borrowing; the result is still the videos. Comments never decide whether a video passes, and a video without usable comments stays. If the call fails, say so and continue.

## 6. Show grouped picks

Pick about 30 included videos, more when more pass and the display has room (showing-videos), higher views first within a group. Group by content format (app review/demo, POV skit, sign-by-sign list, meme/text card…) unless the user asked for another axis, such as branch. Then make one `show_web_videos` call (showing-videos) with, for each pick:

- `title`: a short one-line summary of what the video shows, in the user's language.
- `reason`: the matched branches and what the user can borrow, in the user's language. When a comment supports it, quote it exactly in its original language with its likes. Under 300 characters; cut a long comment with "…".
- `group`: the group label.

After the call, explain the useful patterns and what the user can borrow. When comments help, include a few exact excerpts with their own likes and video links.

## Anti-Patterns

- Answering with a comment report instead of videos, or quoting a popular off-topic comment.
- Paraphrasing inside quotation marks, or naming who wrote a comment.
- Merging "A or B" into one topic, or including a video that shows an excluded topic because another branch matched.
- Repeating empty phrases unchanged.
- Showing videos you dropped, or mixing wider videos into the axis groups.
- Treating absence of an ad label as proof that a post is organic.
