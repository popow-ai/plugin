---
name: writing-content-briefs
description: "Use when the user wants to turn a reference video into their own video plan: a content brief, script, hook, scene breakdown or shooting plan for what they are making or promoting. Finding the reference itself uses finding-references or starting-from-a-video; proposals and approval documents use writing-reference-reports."
metadata:
  harness-level: L2
  layer: entity
---

# Write a content brief

A content brief turns one reference video into a script the user can shoot: the reference's hook carried into the user's field, a body that follows from that hook, and the call to action the user chose. It works for any length of video: the hook and call to action stay short, and the body grows with the length.

## Settle the inputs

Ask for everything that is missing in one message, usually the point of the video and the call to action together, and wait for the answer. Do not write the brief before you have the point: without it the script only lists features.

- **Reference**: the video the user picked. One reference supplies the hook and the flow; a second can supply a single named element only when the user asks for that.
- **What they are making**: the product, service or topic, the one point the video should get across, and who it is for. When personal memory is connected and the user names a saved product, read its facts with read_memory search instead of asking again.
- **Call to action**: what the viewer should do at the end. This is the user's choice: ask which one they want, or whether they want none. Do not pick, recommend or copy the reference's one unless they ask which you would choose. For a detail they did not give, such as the comment keyword, do not spend another question: use the plainest choice (the product name), say so in Setup and let them change it. Skip the question only when they already said it.

When the user named no length or platform, follow the reference's and say so in the brief.

### When the user asks which calls to action exist

Explain the kinds that fit their goal and platform in plain words, then let them choose:

- **Reach**: save the video, send it to someone, stitch or duet it.
- **Following**: follow, often tied to a next part; answer a question in the comments.
- **Leads**: comment a keyword to get a link or resource by direct message; send a direct message.
- **Purchase**: profile link, the platform's shop or cart, a discount code, a link in a pinned comment.

Say what each one needs before it works: a keyword-to-message reply needs an automation tool or manual replies, a shop call needs a tagged product, a code or resource has to exist. Say where it can sit: spoken, overlay text, the post caption or a pinned comment. One main call to action per video is the common practice; an early "save this" can support it. Do not quote conversion rates for a kind of call to action.

## Read the reference before writing

For a link or saved video without Popow evidence (search results or the analysis from starting-from-a-video), follow starting-from-a-video first. A saved note alone does not establish the scenes.

Work out three things:

- **Hook**: the opening line, overlay text and what is on screen, and what kind of opening it is (a result, a question, a relatable problem, a surprising claim).
- **How the body follows from the hook**: the beats in order and what each one does for the promise the hook made, such as naming the problem, showing the steps, proving the result or answering a doubt.
- **How it is shot**: talking to camera, screen recording, text only with a sound, props, cuts.

Timed `transcription` utterances establish spoken lines and their order. A key-moment list does not establish order, and analysis text is not verbatim speech. Mark any beat you could not establish as unconfirmed rather than filling it in.

When nothing establishes how the reference opens, do not write a brief from its title or summary as if it followed the reference. Tell the user the opening could not be read and let them choose: describe the opening themselves, pick another video, or get a looser script based only on the summary.

## Carry the hook into the user's field

When the user has already said how they want the video to open or flow, follow that; the reference's structure below is the default when they have not.

The hook decides the rest. Keep the reference hook's shape and replace its subject with the user's. Name that shape to yourself first, such as "[tool] can now [surprising result]" or "I [result] with only [small means]", and write the new hook in the same shape. Do not move an idea from a later beat into the hook.

- **Same field**: keep the hook's wording pattern and change only what belongs to the other product or creator.
- **Different field**: move the hook over. Keep what makes it work (the kind of opening, its rhythm, the tension it sets up) and state it in the user's field, product and audience.

Then write the body so it delivers what that hook promised, in the reference's beat order. The body changes only as far as the new field requires: each reference beat becomes the matching moment for the user's product. Do not pick a body format from a list or add beats the reference does not have. If a reference beat has no honest equivalent for the user's product (for example proof of earnings they do not have), say so and ask what they can show instead of inventing it.

Check the result before answering: the body must make sense as the continuation of the new hook, and the call to action must follow from what the body showed. If the user's call to action does not fit the flow, say why and offer the closest fit, but keep their choice.

## Write the brief

Keep the brief short: one screen the user can shoot from, not a planning document. Use the content structure below.

```markdown
## <working title>

<length> · <platform> · [@creator](reference link)

**Hooks**

- **Hook A:** <spoken line, or overlay text for a video with no voice>

**Setup**

- <how to shoot it, taken from the reference; what changed from the reference>

| # | Time | Screen | Dialogue | Overlay text |
|---|---|---|---|---|
| 1 | 0–3s | <what is on screen> | <line said> | <text laid over the video> |

**Caption:** <post caption>
```

- **Hooks**: one hook. Add Hook B only when the user asks for a variant.
- **Setup**: one or two bullets. Add one more only for something the user must prepare before shooting, such as their own real numbers or screenshots, a discount code or message automation.
- **Dialogue and Overlay text**: keep what is said apart from what is written. Dialogue is the line said in the beat, on camera or as voice-over. Overlay text is laid over the video; write it on every beat where it shows, whether it appears once at the start or changes scene by scene. Leave a cell empty when the beat has none.
- **Table**: one row per beat in order: the hook rows first, then the body, then the call to action. Do not add section headings or a column for them. Times are approximate. Leave out the call-to-action rows when the user chose none.
- **Caption**: the description posted with the video, in one line with its mentions and hashtags, and the call to action when it lives there. It is not text inside the video.
- When a reference beat could not be established, end with one line naming it. Otherwise add nothing after the caption.

Rules for the content:

- Take product facts, benefits, audience, offers and usage only from the user or their saved product facts, never from the reference or your own knowledge. Do not add medical, guarantee or result promises the user did not state.
- Do not carry over the reference's brand, product details, hashtags, handles, numbers or claims. Numbers and results shown on screen must be the user's own and real; mark them as a slot to fill, never as a made-up figure.

## Show the brief

Present the brief with the host's document, artifact or visualization capability when it fits the request; otherwise answer in Markdown. In every format keep the reference link and any supplied source links as links, and the unconfirmed beats. `show_web_videos` displays videos, not the brief.

After the brief, the user can change the reference, hook, message, call to action or any beat; revise the affected parts and keep the rest. Do not search for more references unless asked.

## Anti-Patterns

- Asking for a video length before writing, or declining to write a brief for a short video.
- Padding the brief with a concept summary, reference analysis or shooting advice beyond Setup.
- Inventing a selling point, audience, reward, claim or number to make the brief feel complete.
