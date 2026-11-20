---
name: shortlisting-creators-from-videos-for-outreach
description: "Use when the user wants a shortlist of creators to contact about promoting a product, whether for seeding, sponsored posts, ad content or an ambassador-style collaboration. Read the requirements and the existing roster, find videos that match what the user is looking for, remove people already on the roster, check each remaining author's account, then deliver a shortlist with evidence. Combines finding-references, searching-live-videos, starting-from-a-video, looking-up-creators and showing-videos."
metadata:
  harness-level: L3
  layer: use-case
---

# Shortlist creators from videos

The user needs creators to promote their product. Popow finds candidates from videos that match what the user is looking for, removes people already on the user's roster, checks each remaining candidate's account against the user's requirements, and delivers a shortlist with the evidence for each candidate. The user reviews the shortlist and decides whom to contact.

Five terms are used below. A **candidate** is one person, who may have several accounts. A **requirement** must be met, and an exclusion is a requirement; a **preference** only ranks candidates who meet every requirement. The **roster** is the user's existing list of people. The **shortlist** is the result of this request.

## Pre-Execution Checks

Read four things from the request and the conversation before searching.

| What to read | Example from one request |
|---|---|
| Product, number of candidates and how their content will be used | "20 more candidates to promote Popow Plugin on their own accounts" |
| Platform, requirements, preferences and exclusions | "Instagram, at most 100K followers, median views of the latest 20 Reels above 1,000, at least one related video above 100K views, not Higgsfield" |
| Roster | "Leave out anyone already on this sheet" |
| Where to save the shortlist | "Add them to the same sheet", or nothing |

The numbers and platforms in the examples belong to that request. Use what this user says; this skill has no default numbers. Its only fixed number is the limit of 20 latest posts per account below. If the user did not say whether candidates will post on their own accounts or make ads for the product, do not ask. State in the result that this was not given.

When the request answers these, start searching without further questions. Ask one question and wait for the answer before any search, including web search, only in these cases:

- The user wants "new" or "more" candidates, or wants roster people left out, and you cannot read the roster. Ask where it is. If you can read only part of it, say which part and ask whether to continue with that limit. A candidate compared with part of the roster is not confirmed as new.
- The user wants the shortlist saved, and it is unclear whether to add to the roster or to create a new list.
- Two requirements contradict each other.
- A requirement asks for more than the latest 20 posts of an account. Say that this skill reads at most the latest 20 posts per account, and ask whether to use 20.
- No connected tool can supply what a requirement needs. Name the requirement and offer a choice: change it, or receive candidates with that requirement marked unconfirmed. Do not change a requirement without telling the user, and do not report this as a search that found no one.

If the user named no roster, do not ask for one. State in the result that no roster was compared and that you can compare if they share one. If the user named no place to save, return the shortlist in the conversation.

Read the whole roster before searching, including its notes and the accounts it links to one person. Never put the roster or contact details into a repository or a public page.

## Find videos and their authors

Use finding-references to choose where to search and searching-live-videos for live search. For this workflow, replace its one-follow-up limit with up to three live searches per round: one initial search and up to two follow-ups. Keep its other search rules.

Count only verified new creators toward the requested total across rounds. If a round ends below target, start another only when it can reasonably find new candidates, such as when a response was cut off or a relevant search angle has not been tried. Carry forward the same requirements, the roster including creators already saved, and all previously seen candidates. Pass previously returned post IDs within the tool's exclusion limit and still check returned results against everything already seen.

Here a video is a lead to a candidate. The requested number counts candidates, not videos, and an author who appears in several videos is one candidate.

For each video keep its link, the author's account ID and handle, the publication date, the view count, when that count was observed, and the search that found it. For a video with co-authors, confirm which account posted it before counting it for a candidate. When a requirement depends on what the video shows, such as demonstrating the product, use starting-from-a-video. A caption or a stored analysis is not a scene you confirmed. Repeated partner tags show promotional experience, not that the creator has a contract with that brand now. When the user wants creators who promote one product repeatedly, count the found videos by that author for the same product, and say that only found videos were counted.

A search term match or a content category alone does not show that a candidate fits. Fit comes from what a video shows the creator doing. For each candidate pick one relevant video as the representative video: the one that most clearly shows why they fit.

A search error, an empty result and a cut-off response are different outcomes. Report which one happened.

**Proceed when:** every candidate has at least one relevant video and an identified author account.

## Remove people already on the roster

Do this before any account lookup, so that no billed lookup is spent on someone already on the roster.

Compare every candidate with the whole readable roster and with the other candidates: by platform and account ID, by handle (ignoring case, "@" and link form), and by profile link. Where the roster says two accounts belong to one person, treat them as one. Two candidates that match each other are one candidate.

- A candidate who matches a roster row on any of these is already on the roster. Leave them out whatever their contact status, and name the roster row they matched.
- Popow tools return no profile text or public email, so Popow cannot find a person's second account from those. A referral code is visible only when a video caption shows it. When the roster, the user or a caption shows a shared email or code, treat it as a possible match: do not merge the two accounts on that alone, mark the candidate unconfirmed, and say why in the result.
- Popow tools do not return which product an account promotes now. Name only the products seen in the videos you found.

**Proceed when:** every remaining candidate is not on the roster. A possible match is unconfirmed and is not looked up.

## Check each candidate's account

Use looking-up-creators to read each remaining candidate's account live. It owns how to call the lookup and how to report what was read. The request for candidates who meet account requirements is the user's choice of these accounts. Skip candidates who already fail a requirement that the video alone decides. Look up one account first. If that lookup is not connected or fails, make no further lookups, mark every requirement that needs the lookup unconfirmed, and continue. Otherwise look up the rest, one call each.

Decide each requirement from what the lookup returned.

- A requirement on the latest N posts, such as median views of the latest 20, is met only with `recent_posts.complete: true`, N different posts, and a publication date and view count on every one. With anything less it is unconfirmed. A post the lookup lists under another author is a co-authored post on this account's profile: count it, and report how many of the N are co-authored. An account with fewer than N posts in total fails it. `status: completed` alone does not show this, and neither does a stored summary.
- A follower requirement is unconfirmed when no follower count was returned.
- A candidate is unconfirmed when the looked-up account ID differs from the video author's account ID.

Calculate statistics with the host's calculation capability, not by estimate. The median of an even number of posts is the mean of the two middle values. When evidence the user supplied shows rounded counts such as "1.2K", work with the range each count could stand for, and pass the requirement only if it holds across the whole range. Never lower N or a threshold to reach the requested number of candidates.

Keep the account's values and the representative video's values apart, each with its observation time. One high-view video does not show how the account's recent posts perform.

**Proceed when:** each candidate is in one of three groups: meets every requirement and is new, fails a requirement, or unconfirmed. Apply preferences only to the first group. Report the other two with reasons.

## Deliver the shortlist

For each candidate give the profile link, the representative video link, each requirement with the value found and the number of posts it was based on, why the candidate fits, the roster comparison result, and when each value was observed. Use showing-videos to show the candidates' videos. The user is choosing between candidates, not videos: showing-videos can group cards by creator or give each candidate a sheet row, and the posts you read for a candidate's account belong under that candidate. Its sheet layout only displays; it writes nothing to a spreadsheet.

Save only when the user asked for it and the host has a way to write to that place.

- Follow the roster's existing columns and examples, and use the file path exactly as the user gave it.
- When the columns have no room for the evidence above, return the rows and the evidence together. Rows alone are not enough.
- A status or contact-status column describes the user's outreach, not whether requirements passed. Leave it empty in new rows unless the user gave a value.
- Before adding, compare with the roster again. Do not change existing rows, notes or contact statuses.
- If you cannot write there, return the shortlist in the conversation and say what prevented saving.

## Post-Execution Verification

**Before the final response, check the search.** Finish searching when the verified total reaches the requested count, the remaining search and verification options are exhausted, or a blocker prevents further progress. If you are below target and can follow up on a cut-off response, check a promising candidate, or try a relevant search angle, continue. If another live search is needed after the current round reaches its limit, start a new round.

Verify each saved batch by reading back its location and count. If a write outcome is unclear, check before retrying. Once the search ends, deliver the shortlist in the conversation or confirm the saved rows. Report the verified new total against the requested count, the reason for any shortfall, the failed and unconfirmed candidate counts, and any failed saves.

## Anti-Patterns

- Treating two accounts as one person because of a shared email, referral code, name or similar appearance, when the roster does not link them.
