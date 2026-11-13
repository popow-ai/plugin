---
name: showing-videos
description: "Use when presenting TikTok videos, YouTube Shorts or Instagram Reels from Popow, live social search or the web. Use show_web_videos with cards for recommendations or sheets for lists and comparisons."
allowed-tools: mcp__popow__show_web_videos
metadata:
  harness-level: L2
  layer: entity
---

## Showing videos

End every turn that recommends or sorts supported videos with one successful `show_web_videos` call, from Popow and the web alike. Every video the answer names must be in it. Choose `layout: cards` (default) or `layout: sheet` explicitly. Use the same `videos` input for both. A sheet adds `sheet.columns` and `sheet.rows` with evidence `video_ids` and aligned `cells`; rows may compare several videos. Every displayed video must be referenced by at least one row. Read and analyze data before displaying; the view does not retrieve saved data or decide the layout. Pass fields as its description says. For live-search picks, also pass `live_cover_url` exactly as returned (including null); never replace it with a stored thumbnail. A current CDN cover is used directly; null or omission uses the signed resolver.

## Groups (cards)

Give each video a `group`. When only one kind of search ran, label where it came from: one short label per Popow search, in the user's language, and one for web finds. Omit `group` when every video comes from one search and none goes to Also worth a look. Live results use the axis searching-live-videos chose (content format by default).

When library and live results share a turn, group every video by that same axis and mix both sources, and web finds, inside each group. Do not group or label by source or platform unless the user asks; each card shows its platform.

## Also worth a look (cards)

The display holds 50 videos. Every library video goes in as returned, even one that looks off-topic: library videos that fail the checklist (finding-references) go to the "Also worth a look" section, as do live picks searching-live-videos sends wider. Live picks take the remaining slots; if they do not all fit, say how many were left out.

Declare the section once in `sections` as `{ "id": "adjacent", "title": "Also worth a look", "note": "Partly matches the request; may widen the idea" }` ("그 외 고려해볼 만한 영상" and "요청과 일부만 맞지만 아이디어를 넓혀 줄 수 있어요" in Korean; translate both for other languages). Give each such video `section: "adjacent"` and a `group` naming what differs from the request (a different situation, product type, or UGC not confirmed), not a content format. Merge similar differences into 2–4 groups; never make a group of one, put a stray video in the closest group. Each `reason` says what it shares with the request and what is missing.

## Save draft

When memory is connected, include `save_context`. Draft its `note` from the returned metadata and caption: why the video holds viewers, then the visible brand and the current task when useful. Never include the full chat or turn a recommendation into a user quote or lasting preference.

## Failures

Keep each rejected video's original link in your reply with the returned reason. Show what you have even when a search fails, times out or returns nothing, and state the failure in your reply. Fill optional fields only with evidence and name sources accurately, including mixed sources. If the tool is unavailable, use the host's output.

## Anti-Patterns

- Counting a rejected video as a displayed card.
