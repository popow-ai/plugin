---
name: finding-references
description: "Use for every video reference request, whatever platform it names, and before every Popow search_collected_posts call: search the library with live social videos unless the user limits it to one side, clarify requirements, write intent and conditions, judge results, follow-up and more-like-this searches, too few matches, a developed brief. For topic comments and comment-based consumer problems use finding-comments."
allowed-tools: mcp__popow__search_collected_posts, mcp__popow__search_live_posts
metadata:
  harness-level: L2
  layer: entity
---

## Where to search

If the user limits the search with "only" wording ("릴스만", "틱톡만", "라이브러리에서만", "Reels only", "library only"), call only the tool that covers it. Otherwise search the Popow library (`search_collected_posts`) and live social videos (`search_live_posts`, following searching-live-videos) in one message. Naming a platform without "only" does not narrow the search: "릴스 찾아줘" still searches both.

- Without `search_live_posts`, use the library alone and do not mention it. For a platform neither search covers, follow researching-on-the-web.
- Settle the questions below, write `intent` and the live checklist (searching-live-videos step 1; write it even without live search), then make both calls.
- Use the checklist on library results only to place them, never to drop them: a video that meets it joins the axis groups, every other one goes to "Also worth a look" (showing-videos).
- A follow-up searches the same sides as the search it continues unless the user changes them. Each tool's `exclude_post_ids` takes its own ids.

## Before searching

Read the request and the relevant conversation. Identify what the user wants to learn or make, which requirements are mandatory, which are preferences, and which Popow can verify. Reuse decisions already made.

Before the first search in a conversation, check saved preferences once with read_memory search on the request; apply them as preferences, never as mandatory filters, and let the current request win. Never ask the user to set up memory. When the request depends on saved products or previous saves, follow managing-memory. A request to show saved videos is memory browsing, not a library search.

Ask only when the search target is ambiguous or requirements conflict. Broad exploration is enough to start. For everyday judgments such as "good references" or "good reactions", use fit to the user's purpose and the recorded engagement, and explain your choice; do not require the user to define a scoring system or invent a numeric filter. State the scope in one sentence and search.

Use the available fields to resolve required conditions. If a detail remains unknown, distinguish candidates from confirmed matches and continue the useful parts of the search. Ask before changing a requirement, not merely because one field is missing. Viewer reactions need comments, not video content.

## Write the search

- **intent**: one self-contained English paragraph describing videos that help the user's stated purpose. Separate what they are making from what they want to learn from other videos. Use their product and situation as context; require them in matches only when the request asks for that match. Keep the user's explicit requirements and relationships; never generalize them away to get more results. Describe the content and structure to find; keep production method or creator type when the user explicitly requires it, using available labels and disclosures to assess it. Before calling, check the scope for assumptions the user did not state and fix them, even after announcing it. The search scores every video against each sentence, so do not add "must", "essential" or exclusion sentences: they leave only a few videos. Keep language, ranking and output instructions out.
- **conditions**: mandatory publish-date, view-count and follower-count filters, and the user's required content fields in `conditions.video` / `conditions.comments` (also described in `intent`). Check content conditions against each video's `metadata` as the tool description says. An empty list proves absence only when the block's limitations do not mark the field unconfirmed. Never turn preferences into filters or change requirements without the user's agreement.

## Explain the results

- Judge with the user's requirements, not details you added. A requested count does not relax those requirements: keep useful alternatives separate from matches and outside the qualifying count. For creative references, separate close matches to the whole execution from variants with one transferable element; say what transfers and what differs.
- A platform AI label or creator disclosure can establish AI-made visuals with attribution. Video analysis describes scenes, not the production method. AI editing alone does not establish generated visuals. A brand-provided trial link can establish collaboration without cash payment.
- For a campaign, check `published_at` for timeliness. `metrics.observed_at` is only when counts were checked; do not infer when views happened.
- Lead with the requested answer: what fits, why, and what to borrow. Mention only gaps that affect that choice. Do not replace requested references with offers to write copy or plans.
- Collect a candidate only to resolve a gap that would change the recommendation or establish a required condition. Never bulk-collect to fill fields.
- Popow returns videos, not accounts: group by `creator`; who runs an account needs a web check or stays unverified.

## Too few matches

Never change a mandatory requirement, filter, problem or topic without the user's agreement. When library videos fall short of `target_count` (and the filters did not just change), retry once in the same turn in plainer terms without details you added, excluding post ids you have, and show both results. Still short: consider comparable products for the same buyer within the agreed scope and label the widening. If library plus live picks are still below `target_count`, fill the rest with web search in the same turn (researching-on-the-web) without asking. Report the shortfall only when web search is unavailable or still short.

## Follow up

Answer questions about dates, counts and languages from the results you have. For a question about what shown videos say or show that those results do not settle, follow starting-from-a-video instead of searching again. For a new search, copy your previous arguments and change only what the user changed. If a filter-only change returns `no_results`, report it; do not rewrite `intent`. For more like a pick, if the one they name was not shown but only one shown pick could be meant, say so and use it. For "popular" without a number, do not ask: state the recent range you use and order picks by recorded views.

For questions about a chosen video's opening, scenes, speech or editing, follow starting-from-a-video. Match the meaning of the request. A clear paraphrase can qualify without repeating the user's exact keyword.

## Carry a developed brief into the search

When the user developed a concept from comments, research or discussion, carry that idea forward instead of restarting from the product category.

- Keep the source observation separate from your interpretation. If selection depends on highly liked comments, check that comment's own reaction count and source; post reactions, repeated mentions and views do not show comment popularity. Do not present a derived concept as an actual comment or its popularity as proof an ad will work.
- Keep in `intent` the purpose, required hook or conflict, narrative relationships and any need for one complete video. Put the result count in `target_count` (20 when the user names none), not in `intent`. Keep the human conflict and why the audience relates; generalize incidental settings, and do not require the source comment's exact scene or wording unless asked.
- For an ad reference built on a relatable hook, describe what the opening must show, how that situation creates a product need, and how product use follows. A quick demo alone does not meet a required hook. If the user wants one complete reference, do not substitute several partial videos.
- Send the search a description of the content and relationships to match, not a transcript, reaction thresholds or instructions on how to judge and report.

Check required elements against each video's own evidence. For a required opening hook, identify the opening scene, line or on-screen text and its link to the product use that follows; a title, rank, category or benefit caption does not establish it. Verify an unsupported required hook or sequence through an available host analysis route before counting it. If no result verifies a requirement, say which one, and retry within the limit above without weakening the brief.

## Anti-Patterns

- Imposing a fixed shortlist size when the user gave none, or adding weak live picks to fill a number.
- Labeling unreviewed candidates unsuitable.
