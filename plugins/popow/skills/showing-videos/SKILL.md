---
name: showing-videos
description: "Use when presenting TikTok videos, YouTube Shorts or Instagram Reels from Popow, live social search or the web. Use show_web_videos with cards for recommendations, cards grouped by creator when the user is choosing creators, or sheets for lists and comparisons."
metadata:
  harness-level: L2
  layer: entity
---

## Showing videos

End every turn that recommends or sorts supported videos with one successful `show_web_videos` call, from Popow and the web alike. Every video the answer names must be in it. Choose cards for recommendations, a sheet for comparisons, or the brand layout for one brand’s UGC overview. A sheet adds `sheet.columns` and `sheet.rows` with evidence `video_ids` and aligned `cells`; rows may compare several videos. Every displayed video must be referenced by at least one row. Read and analyze data before displaying; the view does not retrieve saved data or decide the layout. Pass fields as its description says. For live-search picks, also pass `live_cover_url` exactly as returned (including null); never replace it with a stored thumbnail. A current CDN cover is used directly; null or omission uses the signed resolver.

## By creator (cards)

Cards normally answer "which video": each card is a video and `group` sorts them. When the user is comparing or choosing creators instead, set `group_by: "creator"`. Each creator then gets a heading with their handle and follower count, and their videos run under it on one strip, so the user can scan an account's style and recent activity before moving to the next. Pass every video you have for that creator, with `creator.handle` on each and `creator.follower_count` when you read it. Posts read through looking-up-creators fit here: give each one the handle and follower count of the account it was read from, with its link, date and view count. The strip shows only the videos you pass; say in your reply whether they are the account's newest or just the ones a search found.

A user choosing creators wants to see each account's feed, and a strip holding only the one video that led you to a creator shows little of it. When that is all you have, show it and tell the user they can ask for those accounts' recent posts; looking-up-creators reads them for the accounts and the number the user chooses.

## Sheets

A sheet scrolls sideways: the user sees the first two or three columns and reaches the rest only by scrolling. So before building one, work out from the request what the user is comparing or choosing between: videos, creators, topics, products or something else. One row stands for one of those, and its name is your first column.

- When a row is one video, the cover already leads the row; start with the title or what the video shows.
- When a row is something else, put its name first and set `sheet.columns_before_videos: 1`, so the name leads and the covers follow as that row's evidence. A user asking to analyze or choose creators is comparing creators: one row per creator, the handle first, and every video you found by that creator in the row's `video_ids`.

Order the other columns by how much each helps this user decide, the most helpful first. That depends on the request. For choosing a creator to promote a product it is usually why the creator fits and how the account performs, with one video's view count or date further right; for a user asking which videos are newest, the date belongs near the front. Judge it for each request: no column has a fixed place, and a column the user asked for by name keeps the place they gave it.

## Groups (cards)

Give each video a `group`. When only one kind of search ran, label where it came from: one short label per Popow search, in the user's language, and one for web finds. Omit `group` when every video comes from one search and none goes to Also worth a look. Live results use the axis searching-live-videos chose (content format by default).

When library and live results share a turn, group every video by that same axis and mix both sources, and web finds, inside each group. Do not group or label by source or platform unless the user asks; each card shows its platform.

## Also worth a look (cards)

Cards hold 50 videos. Every library video goes in as returned, even one that looks off-topic: library videos that fail the checklist (finding-references) go to the "Also worth a look" section, as do live picks searching-live-videos sends wider. Live picks take the remaining slots; if they do not all fit, say how many were left out.

Declare the section once in `sections` as `{ "id": "adjacent", "title": "Also worth a look", "note": "Partly matches the request; may widen the idea" }` ("그 외 고려해볼 만한 영상" and "요청과 일부만 맞지만 아이디어를 넓혀 줄 수 있어요" in Korean; translate both for other languages). Give each such video `section: "adjacent"` and a `group` naming what differs from the request (a different situation, product type, or UGC not confirmed), not a content format. Merge similar differences into 2–4 groups; never make a group of one, put a stray video in the closest group. Each `reason` says what it shares with the request and what is missing.

## Save draft

When memory is connected, include `save_context`. Draft its `note` from the returned metadata and caption: why the video holds viewers, then the visible brand and the current task when useful. Never include the full chat or turn a recommendation into a user quote or lasting preference.

## Failures

Keep each rejected video's original link in your reply with the returned reason. Show what you have even when a search fails, times out or returns nothing, and state the failure in your reply. Fill optional fields only with evidence and name sources accurately, including mixed sources. If the tool is unavailable, use the host's output.

## Anti-Patterns

- Counting a rejected video as a displayed card.
