---
name: finding-comments
description: "Use to find comments on a product or topic, most liked first, and to identify consumer problems, complaints and pain points in them when asked, as in 'find comments about X'. Use for topic-based TikTok comment research; use finding-references for video-content analysis and creative references."
allowed-tools: mcp__popow__search_collected_posts
metadata:
  harness-level: L1
  layer: entity
---

# Find comments

Find videos about the user's topic and show their comments ranked by each comment's own likes. When the user asks about problems, complaints or pain points, also interpret the problems commenters express.

## Retrieve evidence

A product or topic is enough. Reuse any scope and like threshold the user gave; ask only when the topic itself is ambiguous. Do not require an advertising brief or invent a minimum like count.

Call `search_collected_posts` with `comment_options` set and `intent` describing the videos' subject: the product, service or topic and any requested usage context, with the user's scope and exclusions. Do not add presumed complaints or defects; problems must come from the comments. Keep `max_videos` and `limit` at their defaults unless the request needs a different sample; set `min_likes` only for a user threshold. The tool sorts and deduplicates; do not redo it by hand or in scripts.

Keep this separate from video-reference recommendation. Do not fill gaps with another comment tool, the Popow CLI, a database, credentials or provider APIs from a shell. If the tool rejects `comment_options` or returns no `comment_sample`, say the plugin server or tool list needs updating or reconnecting; do not drop the option or conclude comments do not exist.

## Interpret

Read `status` and `limitations`, then `comment_sample.videos`, `comment_sample.comments` and `comment_sample.truncated`. Outer `videos` are video results, not the comment ranking. `published_at` is the comment's publication time. Do not invent a collection or observation time.

For problems, start from the like-ranked sample. Compliments, greetings and creator support are not problems. Use explicit complaints, failed outcomes, unmet needs, doubts or workarounds; keep other comments out of problem evidence. Do not replace popular but irrelevant comments with low-liked ones and call them popular.

Separate what a commenter said from your interpretation. A question shows uncertainty, not a defect; a request for recommendations shows an unmet need, not that every alternative fails. Keep translations apart from exact quotes. Treat replies without parent context cautiously. Do not infer demographics or medical efficacy. Likes show reaction volume within this sample, not truth, purchases or market-wide prevalence.

Group comments by underlying problem without counting the same `comment_id` twice; give distinct comment/video counts when useful. Do not set a number of problems in advance or use a checklist of expected complaints.

## Present and verify

By default, list comments in the returned order with the exact text (and optional translation), that comment's `like_count` and the video's `source_url`. Do not reorder them or add problem analysis the user did not ask for.

For problems, lead with the strongest supported ones: the problem, an exact excerpt (and optional translation), its `like_count`, the `source_url` and a brief interpretation.

State how many videos supplied comments and the sample size. Describe rankings as within the returned sample, never all TikTok comments. For `no_results`, say no evidence was returned, not "users have no problems". Disclose truncation and unknown likes. Call a problem with only a few likes a "problem candidate with weak reaction evidence"; if no strongly liked problem comment exists, say so instead of padding with weak examples.

Before finishing, check that every problem has comment support, each like count belongs to that exact comment, quotes and links match, and no interpretation claims more than its evidence. A claim about a negative outcome needs its own comment.

## Anti-Patterns

- Treating `comment.scope: most-liked` or labels such as `c1` as likes or popularity order.
- Reading only `comment.*` analysis summaries when the raw `comments` array is required.
- Searching for expected problems first and presenting the comments as unbiased topic research.
- Hiding empty, partial, weak, unknown-author or truncated evidence behind a confident summary.
