---
name: getting-started-with-popow
description: "Use at the start of a Popow conversation, when the user asks what Popow can do or how to start, and when Popow tools are missing, whoami reports not signed in, authentication fails, a plugin version is incompatible, or Popow does not respond. Check the connection, then start the user's first task or retry the original one."
metadata:
  harness-level: L2
  layer: entity
---

# Get started with Popow

Get the user connected and doing their first piece of work. Run only the branch that applies:

- The user already asked for something, or a Popow call failed: connect if needed, then continue that request with its matching skill. Do not introduce Popow or ask what they want.
- The user asks what Popow can do, how to start, or opens with only "Popow": connect, then **Choose the first task**.
- Tools are missing, sign-in fails or Popow does not respond: **Restore the connection**.

Never end with only "Popow is not connected" or ask the user to repeat a request. Keep their original request and the selected environment throughout.

## Check the connection

Call this plugin's own whoami once and report only that connection; mention other Popow servers or environments only when the user asks about them. `authenticated: true` with the account email means Popow is ready; say which account in one line. `authenticated: false`, or whoami missing while the host lists this server as needing sign-in, means sign-in is required: go to step 3 of **Restore the connection**. A host's "Connected" label or a tool list containing only whoami does not prove sign-in; whoami also works without login. A timeout alone does not prove the user is logged out.

## Choose the first task

Say in two or three sentences what Popow does with the tools this host actually exposes, not generic assistant abilities: it finds short-form reference videos from a description or a TikTok or Reels link, in its library and live on TikTok and Instagram when connected, reads highly liked comments, researches why customers buy or hesitate, saves videos and creators with notes, and shows videos as playable cards. Leave out what the exposed tools cannot do.

Then ask one short question about what they are making, with up to four starting points. Each starting point is one line plus a request they can copy with their own product swapped in:

| Starting point | Example request | Skill |
|---|---|---|
| Find reference videos | Find TikTok videos showing sunscreen as a makeup-prep step. | finding-references |
| Understand a video they have | What makes this video work? [TikTok or Reels link] | starting-from-a-video |
| Learn what viewers say | Find the most liked comments about sunscreen white cast. | finding-comments |
| Understand customers first | Why do people hesitate to buy tinted sunscreen in the US? | understanding-customers |

Recommend the one that fits what the user has already said. If they have saved videos, offer viewing-saved-videos instead of one row. When they answer, hand the request to that skill unchanged.

Do not run a search, read comments or save anything just to demonstrate Popow; searches use the user's account and onboarding does not authorize saves. Do not list every skill or tool, name a skill the host does not have, or re-introduce Popow later in the conversation.

## Restore the connection

1. **Check updates first when tools are missing, incompatible or unresponsive.** Inspect the installed plugin's source and version through the current host and use that source's supported update action, keeping its marketplace or app identity, branch, MCP URL and environment. Never compare Local or Dev against Prod, or downgrade a private app-backed copy to match the public version. If the version cannot be confirmed, say so and continue with sign-in.
2. **Check login once.** Follow **Check the connection**. If the host blocks MCP startup or tool exposure, use its connection status or error instead of calling whoami again.
3. **Start sign-in.** Give one path, for the current host and this plugin's own server only (for example `popow-local` for Popow (Local)). Do not name buttons the host does not show.
   - Claude desktop: the session's Connectors panel → this server's Authenticate → Connect, then Reconnect once the browser says sign-in is complete.
   - Claude Code in a terminal: `/mcp` → this server → Authenticate (Re-authenticate when a login is already saved).
   - Claude web: the plugin's Connectors → Connect → Sign in now → Use your own OAuth client, with this connection's `oauth.clientId` from the installed package and an empty secret. If whoami stays false, Disconnect → Connect once.
   - Codex: run `codex -c mcp_oauth_callback_port=39603 mcp login popow`. Run `codex mcp logout popow` first only when a saved credential fails to refresh.
   - ChatGPT: its Reconnect prompt, or the app's connection settings.

   Ask the user to finish sign-in and consent, never to paste passwords, tokens or callback URLs. Keep the task pending until they finish.
4. **Check and resume.** Refresh the host's tools or start a new session if required. Call whoami once to check the account, then retry the original request once. Report success only from the actual result in that host; a sign-in success page is not proof.

Never add a second connector or MCP server for Popow, switch a connection's MCP URL (including to the frozen review connection), or replace an app reference with a raw MCP entry. If OAuth settings cannot be edited, explain that the host needs the connector removed and added again, and confirm who uses it before removing a shared one.

For an owned ChatGPT app-backed plugin, update skills with host-native editing tools, keeping its plugin ID, app reference and permissions. If complete source files are unavailable, ask for the published archive as described in the install guide; do not rebuild skills from search snippets. If tool names or schemas are stale, use **Refresh tools** in its connection settings and start a new conversation; updating skill files alone does not refresh them. Web chat never receives terminal commands.

Update commands for a direct CLI installation of the published Prod package `popow@popow` only (account-synced and directory copies keep their own source's update action):

- Codex: `codex plugin marketplace upgrade popow`, then `codex plugin add popow@popow --json`.
- Claude Code: `claude plugin marketplace update popow`, then `claude plugin update popow@popow`.

If version and login checks pass but a request still fails, report the exact error as a service or connection failure. Stop after one recovery attempt. Do not repeatedly update, clear credentials or ask for sign-in.

## Anti-Patterns

- Treating zero search matches as a connection failure.
- Claiming a different host's login or search proves this host works.
