# Install Popow

Popow adds TikTok creative-reference search to ChatGPT, Claude, Codex and
Claude Code. A Popow account is required.

Choose the instructions for the app you want to connect:

- [ChatGPT web](#chatgpt-web): connect the remote MCP tools.
- [Claude web](#claude-web): install the skill and MCP connection together.
- [Codex](#codex) and [Claude Code](#claude-code): install the plugin with the CLI.

Only the CLI sections require commands on the user's computer. If you cannot
run them there, give the user those steps. Web setup takes place in the app,
without running the CLI installation commands.

## ChatGPT web

This route connects Popow's MCP tools. It does not install this repository's
bundled skill. Custom MCP availability depends on your account and workspace
permissions; ask your administrator if the option is missing.

1. Open [ChatGPT Plugins](https://chatgpt.com/plugins).
2. Select **+**, then **Add custom MCP server**.
3. Name it **Popow** and enter `https://mcp.popow.ai/mcp` as the connection URL.
4. Choose OAuth authentication and complete the Popow sign-in when prompted.
   Review the permissions and risk warning before continuing.
5. Select **Create as a plugin**, review its tools, and install it if prompted.
6. Start a new chat. Type `@`, select Popow, and ask: **Which Popow account am I
   connected to? Call whoami to check.**

The current Plugins flow does not require enabling Developer Mode first.
See [OpenAI's custom MCP setup guide](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt)
for account requirements and the legacy Apps interface.

Do not assume that importing this GitHub marketplace makes the plugin usable
on the web. An imported MCP plugin can be marked **Desktop only**; see
[OpenAI's marketplace import guide](https://learn.chatgpt.com/docs/enterprise/plugin-management).
If you need the bundled skill, verify that your installed plugin includes it
and is web-compatible separately from the MCP connection.

## Claude web

Use [Claude](https://claude.ai) on an account with plugin access. Workspace
policies may restrict third-party marketplaces.

1. Open **Customize → Plugins**.
2. Choose **Add → Add marketplace → Add from a repository** and enter
   `https://github.com/popow-ai/plugin` (or `popow-ai/plugin`).
3. Find **popow** in the added marketplace and choose **Add**.
4. Complete the bundled Popow connector's sign-in when prompted. If needed,
   open **Customize → Connectors**, find Popow, and choose **Connect**.
5. Start a chat, type `/` or use the **+** menu, and select the Popow skill.
   Ask: **What can Popow do?** Then ask it to call `whoami` to check the account.

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
Type `$popow` and select the Popow reference-search skill. Autocomplete inserts
`$popow:popow`. Try:

```text
$popow:popow What can Popow do?
```

## Claude Code

Run in a terminal:

```bash
claude plugin marketplace add popow-ai/plugin
claude plugin install popow@popow --scope user
```

Start a new Claude Code session. Run `/mcp`, select the plugin's `popow` server,
choose **Authenticate**, and sign in with your Popow account.
Type `/popow` and select `/popow:popow` from autocomplete. Try:

```text
/popow:popow What can Popow do?
```

## Check the connection

1. Check that Popow is installed and enabled in the app. CLI installations
   should list `popow@popow`; a custom web MCP connection may use its display name.
2. If you installed the bundled skill, invoke it and check that its reply
   describes TikTok reference search. For an MCP-only setup, report the skill
   as not installed rather than treating tool access as skill installation.
3. Ask the host to call Popow's `whoami`. Check the returned account before
   asking for references.

Report installation, skill availability/invocation and account connection separately.
A capability reply alone does not establish a successful account connection.
If authentication fails, report the exact error and use the host's sign-in flow.
Never ask the user to paste passwords or tokens into chat.

If a `popow` marketplace already exists, check its source in the host's plugin
settings before replacing it. Removing a Claude Code marketplace can also
remove its plugins and saved data. Keep an existing connection until the new
plugin works, then remove duplicate MCP registrations through the host settings.

## Update

For web apps, manage updates through the same plugin or connector interface used
for setup. For ChatGPT custom MCP connections, use **Refresh** when available
after tool metadata changes, then start a new chat and check the connection
again. This does not install or update the repository's bundled skill.

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
