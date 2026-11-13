---
name: starting-from-a-video
description: "Use to understand a TikTok or Instagram Reels link or answer follow-up questions about a selected video's scenes, opening, speech or editing. For similar-video searches, use finding-references."
allowed-tools: mcp__popow__search_collected_posts
metadata:
  harness-level: L2
  layer: entity
---

## Searching from a reference video

For a bare reference link, first get enough information to understand the video. Ask about the production purpose only if it would change the search target or selection criteria; a broad exploration request needs no purpose.

Answer from the evidence already returned before requesting more. Distinguish speech from on-screen text and use the supplied timing. An utterance starting at 0:07 locates the quote. It does not establish each word's exact time.

First check which tools this connection exposes. If `get_post_context` is unavailable, Popow cannot prepare the link here: use the host analysis routes below. Continue with the search only when the reference has enough evidence.

When `get_post_context` is available:

1. Call `get_post_context` with the link and follow its `request_id` procedure. If a call errors but names a `request_id`, read once with it.
2. Use the returned `extractions`, `metadata` and `transcription`. For missing evidence, use the routes below.
3. If the user also asks for similar videos, write `intent` from the reference's `extractions` and `metadata` (or another route below). Match the aspects the user requested, such as topic, product category or structure. For structural references, generalize only details the user has not required. Put the user's own product or topic in `intent` when known. For a TikTok reference, pass its numeric post id in `exclude_post_ids` (never a Reels shortcode). Retain the agreed `conditions`, call `search_collected_posts` once and explain each result by how it resembles the reference.

## Questions about videos

This covers given links and videos you already showed ("the third one", "these"); the user does not need to give links again. Answer from what you already have when it settles the question, such as counts, dates, captions and languages. Otherwise call `get_post_context` with the videos the question is about (their `platform` and `post_id`, or the links) and follow its `request_id` procedure. Then answer the question yourself from `metadata`, `extractions` and `transcription`, naming the video behind each point.

- What is said: use `transcription` utterances and words with their times. It is machine speech recognition, not on-screen text or a verified quote. If a transcript you need is `pending` or `processing`, read once more with `request_id`; if it is still not ready, say the speech is not confirmed yet. A null, `failed` or utterance-less transcript is unconfirmed, never proof that nothing is said.
- Counts: use `metadata` with its `observed_at`.
- Keep the conditions the user set. When fewer videos meet them than asked, say how many do instead of adding videos that do not.
- Report every rejected or failed post and what stays unconfirmed.

Call `answer_post_questions` only when the user asks for it by name. Missing, preparing or failed context is not a reason to call it.


## Reference analysis outside Popow collection

Before asking the user, try the host's browser, download and video-analysis tools, and web-search the post id and handle (caption-level evidence). Captions or thumbnails are not a watched video, sampled frames are not a full transcription, and downloading alone is not analysis. Do not create or change resources in another service without the user's agreement. Name the actual source and keep unsupported features unconfirmed.

If every route fails, state the blocker and in the same message ask for the file or a short description, and what they are making or the problem it solves. If they cannot describe the reference, do not ask again: search from their product's concrete situations (the problem, the scene of use), not moods, and say similarity to the reference is unconfirmed.

## Anti-Patterns

- Resubmitting posts to `get_post_context` instead of reading the existing `request_id`.
- Searching again to answer a question about videos already shown.
- Claiming Instagram library search: Popow searches TikTok only.
