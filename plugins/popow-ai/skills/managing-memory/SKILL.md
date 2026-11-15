---
name: managing-memory
description: "Use when the user asks to save or revisit videos or creators, recall prior product facts or personal preferences, browse saved items, or correct/delete a memory. Also use when reference work depends on previously saved context. New library searches use finding-references; video display uses showing-videos."
allowed-tools: mcp__popow__whoami, mcp__popow__read_memory, mcp__popow__write_memory, mcp__popow__show_web_videos
metadata:
  harness-level: L2
  layer: entity
---

## Personal memory

Memory belongs to the signed-in individual. Use whoami only when account identity needs resolving. Do not ask for an organization or collection. Without the memory tools, say personal memory is not connected and never claim a save.

## Recall and browse

- Recall with read_memory search when prior facts, preferences or saves matter; not on every message just to reformat an answer. The user's current instructions win.
- For a complete list, page with list and follow next_cursor; never request more than 20 per page.
- Resolve ambiguous product names from personal product items and use the returned product ID. Saved videos are not linked to products: find a product's saved videos by searching the notes. Apply general preferences only where they fit.
- Show saved references through showing-videos with `saved_note` (every note as stored, newest first) and a short format `group` in the user's language, the same name for every video of that format. Do not run a library search just to show saved references.
- When the user wants saved references for new work, first show the matching items with their notes and ask which to build on when several fit. For a brand, product or hook, search the notes and say search may miss items; use list for a complete set.
- Saved creators (kind creator): search finds them by handle, name or note; list with `creator: {platform, platform_account_id}` is the only exact match for one account. Give the creator's notes in your reply; a saved creator has no card and no saved videos.
- Report partial results, missing items and failures. Do not invent product properties or reasons for saving.

## Save

- Save a video (kind post) only on an explicit request, with its original link (TikTok video, YouTube Shorts or Instagram Reel) and verified fields. Do not require a product.
- A bare "save this" / "저장해줘" is permission, not the note. Unless the user's message already holds the note (their reason, hook points or keywords), reply with a drafted note and ask once, briefly: save with this note, change it, or save without a note. Call write_memory only after they answer. End the reply with that question; do not explain why you ask or that nothing is saved yet.
- The note replaces the reference sheet users keep by hand and is found later by semantic search. The user sees it word for word as their memo, so write plain sentences with no headings, format-name line or numbering: why the video is worth keeping (what holds viewers, the reaction it triggers such as curiosity or relatability; not a scene summary), plus what else the user keeps: their reason, product, brand and how it appears, similar links or remarks. Draft it from returned metadata (opening, key point, central appeal, comment reactions), the caption and the current task.
- Pass the video's verified title, caption and creator handle when known; they keep a note-less save findable. When none is known (only a link), do not collect or analyze the video to draft a note: in the same question ask for their reason and a few words to find it by, and say that without them it will be hard to find. If the user declines or gives nothing, save without a note and do not ask again; when no note or verified text exists, say it can be found only by browsing the full list.
- Read existing items first to avoid saving an identical context twice. Reuse existing products.
- Save a creator only on an explicit request, from a Popow video result of that account. Copy `platform` from the video's `platform` and `platform_account_id` from its `creator.platform_account_id`, exactly as returned. If the result has no `platform_account_id`, do not retry with a handle: say that account's id is missing and offer to save from one of that account's video results. Add the handle, display name and `sec_uid` (TikTok, when the result has one) as returned. A creator save holds the account and the note only: do not pass videos.
- A creator save asks the same note question as a video. The note is all that is kept about why, so draft it in detail: the product or brand fit, how their videos work, and which videos led to the choice (each one's title or what it shows, and its link).
- For a creator, read existing notes with read_memory list and the creator filter. Follow the user's intent: update an existing note for a correction, reuse it for the same context, or save a separate entry for a new context. Ask only when that intent is unclear.
- Store product facts and lasting preferences only when the user asks or clearly supplies reusable context. A one-off search constraint or a guessed USP is not a lasting fact. Product usp, characteristics and constraints are arrays, even for one value.
- On MEMORY_TOO_LARGE, propose a shorter note that keeps the user's wording, and save after they accept, or ask them to shorten it. Do not recite storage limits.

## Correct and remove

- Resolve the item with list/search/get and update by the returned ID. Product updates replace the data: carry forward facts the user did not change.
- To correct a note, keep what the user did not change; null clears the note. Never save a copy and delete the original to edit a note.
- Remove only a resolved target the user asked to delete. Removing a post removes that saved context; other contexts of the same video remain. To unsave the video entirely, remove all its matching items. Removing a product does not remove saved videos.
- For an unknown write result, inspect the item or retry identical input with the same operation_id. Never present a fresh save as a safe retry.

## Anti-Patterns

- Automatically saving search results or treating one selected video as a universal preference.
- Replacing saved-item browsing with new library results, or silently weakening a failed recall.
- Saving a creator by handle or name, with an id from another account or a made-up id.
