---
name: analyzing-saved-videos
description: "Use when the user asks to analyze, compare, categorize, visualize, or draft a creator brief from their saved videos and notes."
allowed-tools: mcp__popow__read_memory, mcp__popow__show_web_videos
metadata:
  harness-level: L2
  layer: entity
---

Read saved references with `read_memory` list and follow every cursor; use search only for an explicitly narrower request and say it can miss results. Use saved titles, original URLs and notes, plus any analysis of those videos already available in the conversation. Keep all notes for a video and separate the user's words, observed content and new proposals. Do not infer scenes, hooks, metrics or similarities the supplied evidence does not support. Do not newly analyze or search videos.

For a creator brief, turn the selected videos' observed opening and sequence into concrete shot directions.

Shape the tables to the user's question, not a fixed template. Tie each claim to its source video or note and separate observations from recommendations. When useful, add a table of original notes and a separate comparison or common-patterns table. Pass source videos through the common `videos` input, with original URLs and `saved_note` ids and notes. Put every supporting canonical video id in each row's `video_ids`, including rows comparing several videos. Use video ids, not saved memory item ids. Name a title column `제목` / `Title`, not `영상` / `Video` (the thumbnail column already uses that). Write supporting links in cells as Markdown links with short video names, not raw URLs.

Never silently omit videos. If a page is partial or unavailable, or the display contract limits the result, split the result into sheets within the contract or name the limit, and do not claim full coverage. Use `sheet.limitations` only for such retrieval failures, incomplete coverage or display limits. Mark missing evidence next to a claim only when needed to avoid a misleading conclusion. Do not add routine notes that the analysis used titles and notes or did not reanalyze videos.

Pass only supported original TikTok, YouTube Shorts and Instagram links to the view. For any other URL in a note, keep its meaning, leave the address out and tell the user it is not displayed. Never pass stored media or thumbnail URLs.

Call `show_web_videos` with `layout: sheet`, the common `videos` input, current language and a title. Put the requested column labels in `sheet.columns` and evidence video ids and matching cells in `sheet.rows`; each row must have one cell per column. Use the same sheet contract for a saved list or comparison; the display tool does not infer a mode from the data. When the user asks to compare two or three specific videos against each other, give each video its own row and set `sheet.side_by_side: true`: the view then shows one column per video so they read side by side. Leave it out for everything else, including a comparison of more than three videos and rows that group several videos. Respect the 50-video / 200-row limit and state incomplete coverage. For a refined request, reread memory when needed and produce a new result. Do not generate a separate HTML file or upload saved data. If personal memory is unavailable, say so instead of running a fresh search.

## Anti-Patterns

- Presenting an inferred video scene as a fact, or omitting a failed page from the stated scope.
