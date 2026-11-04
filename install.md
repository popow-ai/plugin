# Install Popow

Popow adds TikTok creative-reference search to ChatGPT, Claude, Codex and
Claude Code. A Popow account is required.

Popow is not yet listed in the ChatGPT or Claude plugin directories. Use the
manual setup below for the app the user wants to connect:

- [ChatGPT web](#chatgpt-web): connect the remote MCP tools.
- [Claude web](#claude-web): add this repository as a marketplace.
- [Codex](#codex) and [Claude Code](#claude-code): install the plugin with the CLI.

Only the CLI sections require commands on the user's computer. If you cannot
run them there, give the user those steps and wait. Web setup happens inside
the app and needs no commands.

When setup is complete, end with the single handoff in
[Try Popow](#try-popow). Do not describe connection checks or tool names to the
user; the Popow skill handles them.

## ChatGPT web

This route connects Popow's MCP tools. It does not install this repository's
bundled skill. The option can be hidden by workspace policy; if it is missing,
the user should ask their workspace administrator.

1. Open [ChatGPT Plugins](https://chatgpt.com/plugins).
2. Select **Add**, then **Add custom MCP server**.
3. Name it **Popow** and enter `https://mcp.popow.ai/mcp` as the server URL.
4. Keep **OAuth** as the authentication. Expand **Advanced OAuth settings**,
   leave the registration method as **User-Defined OAuth Client**, and enter
   `b459679b-695c-4f8c-bd33-c901f8156c41` as the OAuth client ID. Leave the
   client secret empty and the token endpoint auth method as **none**. Popow
   does not support dynamic client registration, so this step is required.
5. Check **I understand and want to continue**, then select
   **Create as a plugin**. Popow appears under **Installed**.
6. In the **Connect Popow** dialog, select **Connect Popow** and complete the
   Popow sign-in in the window that opens.

Do not import this GitHub repository as a ChatGPT marketplace. Imported plugins
that declare an MCP server are marked **Desktop only** and cannot run in ChatGPT
on the web; see [OpenAI's plugin management guide](https://learn.chatgpt.com/docs/enterprise/plugin-management).
See [OpenAI's custom MCP server guide](https://developers.openai.com/api/docs/guides/custom-mcp-server)
for the current dialog and account requirements.

## Claude web

Use [Claude](https://claude.ai) on a plan with plugin access (Pro, Max, Ultra,
Team or Enterprise). Workspace policies may restrict marketplace sources.

1. Open **Customize → Plugins**.
2. Select **+**, then **Add marketplace → Add from a repository**. Pick
   `popow-ai/plugin` from the list or enter it, then select **Sync**.
3. On the **Popow** card that appears, select **Add**. Confirm **Continue** on
   the notice that the plugin includes components that run code. Claude then
   shows "Popow is installed and ready to use".
4. Adding the plugin does not sign you in. Open the Popow plugin page, select
   the **Connectors** tab, and choose **Connect** next to `popow`. In the
   **Add custom connector** dialog (name and URL are prefilled) select
   **Continue**. On step 2 keep **Sign in now** and **Use your own OAuth
   client**, enter `b459679b-695c-4f8c-bd33-c901f8156c41` as the OAuth client
   ID, leave the secret empty, and select **Add**. Popow does not support
   dynamic client registration, so the client ID is required. Complete the
   Popow sign-in in the window that opens. The plugin's connector does not
   appear under **Customize → Connectors**.

See [Anthropic's plugin guide](https://support.claude.com/en/articles/13837440-use-plugins-in-claude)
and [connector guide](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).
The web app uses the hosted MCP endpoint; no local callback port is needed.

## Codex

Run in a terminal:

```bash
codex plugin marketplace add popow-ai/plugin
codex plugin add popow@popow --json
```

Start a new Codex session. For browser sign-in, keep the callback port:

```bash
codex -c mcp_oauth_callback_port=39603
```

Complete the Popow connection prompt and sign in with your Popow account.

## Claude Code

Run in a terminal:

```bash
claude plugin marketplace add popow-ai/plugin
claude plugin install popow@popow --scope user
```

Start a new Claude Code session. Run `/mcp`, select the plugin's `popow` server,
choose **Authenticate**, and sign in with your Popow account.

## Try Popow

Installed plugins load when a session starts, so the user must open a new chat
or session first. Then tell the user to send exactly one prompt:

| App | Prompt |
| --- | --- |
| ChatGPT web | `@Popow What can Popow do?` |
| Claude web | Type `/`, choose the Popow skill, then `What can Popow do?` |
| Codex | `$popow:popow What can Popow do?` |
| Claude Code | `/popow:popow What can Popow do?` |

Popow answers with what it can do and checks the connected account itself. If
the account is not connected, it guides the user through the host's sign-in
flow.

Your final message to the user is two parts only: one sentence saying
installation finished, then the prompt above. Do not list marketplace, plugin,
MCP or connection status, do not mention other Popow registrations, and do not
name Popow tools. Popow reports connection problems itself when the prompt is
sent.

If sign-in fails, report the exact error and use the host's sign-in flow.
Never ask the user to paste passwords or tokens into chat.

If a `popow` marketplace already exists, check its source in the host's plugin
settings before replacing it. Removing a Claude Code marketplace can also
remove its plugins and saved data. Keep an existing connection until the new
plugin works, then remove duplicate MCP registrations through the host settings.

## Update

For web apps, manage updates through the same plugin or connector interface used
for setup. For a ChatGPT custom MCP connection, use **Refresh** when available,
then start a new chat.

For Codex:

```bash
codex plugin marketplace upgrade popow
codex plugin add popow@popow --json
```

For Claude Code:

```bash
claude plugin marketplace update popow
claude plugin update popow@popow
```

Start a new session after updating.

For help, contact [Popow Support](https://popow.ai/support).
Read the [Privacy Policy](https://popow.ai/privacy) and
[Terms of Service](https://popow.ai/terms).
