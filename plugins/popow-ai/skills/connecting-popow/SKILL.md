---
name: connecting-popow
description: "Use when Popow tools are missing, whoami reports not signed in, authentication fails, a plugin version is incompatible, or Popow does not respond. Check updates, guide sign-in and retry the original task."
allowed-tools: mcp__popow__whoami
metadata:
  harness-level: L2
  layer: entity
---

# Restore the Popow connection

Do not end with only "Popow is not connected" or ask the user to repeat a failed search. Keep their original request and the selected environment throughout recovery.

1. **Check updates first when tools are missing, incompatible or unresponsive.** Use the installed plugin's source and the current host's update tools. Read `https://raw.githubusercontent.com/popow-ai/plugin/main/install.md` for that host's installation and recovery path. As a fallback for the public Prod package, read `https://raw.githubusercontent.com/popow-ai/plugin/main/plugins/popow/.codex-plugin/plugin.json`. Never compare Local or Dev against Prod, or downgrade a private app-backed copy just to match the public package version. Apply an available update when the host supports it. Otherwise give the shortest exact user action. If the lookup fails, say the version is unconfirmed. Do not invent an update requirement or hold back a known sign-in fix.
2. **Check login once.** Call whoami once if available. `authenticated: false` means sign-in is required. If the host blocks MCP startup or tool exposure, use its connection status or error instead of calling whoami again. A timeout alone does not prove the user is logged out.
3. **Start sign-in.** Use the current host's Connect, Authenticate or Reconnect action. Web Chat uses the installed plugin's app or connector settings. Desktop Code/Work may show Settings → MCP servers → From plugins → popow → Authenticate while signed out. Claude Code uses `/mcp` as described below. Do not name buttons the host does not show. Ask the user to finish sign-in and consent, never to paste passwords, tokens or callback URLs. Keep the task pending until they finish.
4. **Check and resume.** Refresh the host's tools or start a new session if required. Call whoami once to check the account, then retry the original request once. Report success only from the actual result in that host.

For an owned ChatGPT app-backed plugin, use host-native editing tools when available and preserve its plugin ID, app reference and permissions. Do not replace it with raw MCP setup or create a duplicate. If complete source files are unavailable, ask for the published archive as described in the install guide. Do not rebuild skills from search snippets. Web chat must not receive terminal commands as its recovery action.

If a ChatGPT app still has old tool names or schemas, use **Refresh tools** in its connection settings when available, then start a new conversation. Updating skill files alone does not refresh saved tool metadata.

With a terminal on the user's computer, the published Prod package supports these commands. Check in the installed host, not a substitute:

- Codex CLI or desktop Code/Work with a terminal: update with `codex plugin marketplace upgrade popow` then `codex plugin add popow@popow --json`. Sign in with `codex -c mcp_oauth_callback_port=39603 mcp login popow`. Only if an existing credential fails to refresh, run `codex mcp logout popow` first. It removes that connection's saved OAuth credentials.
- Claude Code: update with `claude plugin marketplace update popow` then `claude plugin update popow@popow`. Sign in with `/mcp` → the plugin's `popow` server → Authenticate (Re-authenticate when a login is already saved).

If the host cannot find the installed server, use its plugin connection UI. Do not register a duplicate MCP server. Never apply these Prod commands to Local or Dev.

If version and login checks pass but a request still fails, report the exact error as a service or connection failure. Stop after one recovery attempt. Do not repeatedly update, clear credentials or ask for sign-in.

## Anti-Patterns

- Treating zero search matches as a connection failure.
- Claiming a different host's login or search proves this host works.
