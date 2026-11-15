---
name: viewing-saved-videos
description: "Use when the user wants to see all their saved Popow videos in a searchable sheet."
allowed-tools: mcp__popow__read_memory, mcp__popow__show_web_videos
metadata:
  harness-level: L2
  layer: entity
---

Read saved references with `read_memory` list (`kind: post`, `limit: 20`) and follow every cursor. If memory is unavailable or a page fails, explain the missing scope; do not replace saved videos with a new search.

Combine entries for the same video and keep every note exactly as stored. Call `show_web_videos` with `layout: sheet`, the current language, and the same `videos` display fields used by cards. Include each video's `saved_note` (saved item id and notes). By default supply only two `sheet.columns`: title and notes. Write each title cell as a Markdown link to the video's original URL, `[title](url)`, so the title opens the video; do not add a column of raw URLs, which pushes the notes out of view. The link and the notes are what the user came for; the title, with the thumbnail the view draws, tells the videos apart. Add creator, counts, posted date, saved date or other video details as columns only when the user asks for them. Supply `sheet.rows` with one row per video: its canonical `video_ids` (for example `tiktok_123`) and matching `cells`. These ids identify the video, not the saved memory item. The view supplies thumbnails from `videos`; do not pass image or stored media URLs.

The sheet is display only; the host owns pagination. Respect the 50-video / 200-row display limit. If the list exceeds it, tell the user how much remains, show an explicit subset with `sheet.limitations`, and continue in another call when needed. Never claim full coverage for a partial page or subset. For an empty list, pass `videos: []` and an empty `sheet.rows`. Do not generate or publish a separate HTML page.

## Anti-Patterns

- Substituting new search results for the user's saved videos, or describing a partial list as complete.
