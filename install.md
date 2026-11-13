# Install Popow

Install Popow's skills and connection together in the host you use.
A Popow account is required. Use that host's section below. Web chat does not
run the Codex or Claude Code terminal commands.

## Copy-and-paste setup prompt

Use the same prompt for setup or recovery:

```text
Follow https://raw.githubusercontent.com/popow-ai/plugin/main/install.md to set up or repair Popow in my current host.
Use its supported installation or update tools, preserve my existing Popow connection, and enable automatic updates where supported.
Check the installed skills and connected account with whoami, then resume my original request.
If a user action is required, give me the shortest exact step instead of commands for another host.
```

Use OAuth for web connections. If the host asks for client settings, choose a
provided client and use `b459679b-695c-4f8c-bd33-c901f8156c41` as the client ID.
This public client has no secret. Complete the host's sign-in and consent steps.

## Claude web, desktop Chat and Cowork

Open **Customize → Plugins → Add → Add marketplace → Add from repository**.
Enter `https://github.com/popow-ai/plugin` and keep **Sync automatically** on.
Add Popow, then open its **Connectors** tab and complete **Connect** and sign-in.
Installation and connection are separate steps. Check both.

Marketplace updates apply after the source syncs. Use **Check for updates** to
request a check, then start a new conversation or task if it still uses old skills.
See [Claude's plugin installation and update rules](https://claude.com/docs/plugins/overview).

Claude Code can load the plugins installed in the same Claude account at startup.
Keep the existing installation source when repairing it. A separate CLI install
can override the account-synced copy.
See [Claude Code's account sync rules](https://code.claude.com/docs/en/plugins/loading#synced-plugins).

If a connector reports an unapproved request header, report that exact error as a
Popow setup issue. Reinstalling or signing in repeatedly will not approve a header.

## Codex CLI and desktop Code/Work

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
Type `$popow` and select `connecting-popow` from autocomplete. Try:

```text
$popow:connecting-popow Check my Popow connection.
```

## Claude Code

For a direct CLI installation, run in a terminal:

```bash
claude plugin marketplace add popow-ai/plugin
claude plugin install popow@popow --scope user
```

Start a new Claude Code session. Run `/mcp`, select the plugin's `popow` server,
choose **Authenticate**, and sign in with your Popow account.
Type `/popow` and select `/popow:connecting-popow` from autocomplete. Try:

```text
/popow:connecting-popow Check my Popow connection.
```

## ChatGPT web and desktop Chat

Use an app connection this account can access together with the Popow skills.
Uploading the Git package as a ZIP can make it **Desktop only**. That does not
establish web support. Another person's app ID does not grant access to their app.

For a private plugin you own, use OpenAI's
[Plugin Creator](https://chatgpt.com/plugins/plugin_connector_1p_e1a10c53223481918a42f1510ec46c1e)
when its editing tools are available:

1. Inspect the installed Popow plugin and its app connection using the host's tools.
2. Fetch the latest skills from `https://github.com/popow-ai/plugin/tree/main/plugins/popow/skills`.
3. Update the same plugin, preserving its identity, app reference, permissions and
   account. Keep it web-capable. Do not replace the app reference with raw MCP setup.
4. Read back the saved skills, start a new conversation and check `whoami`.

If the host cannot fetch the complete skill files, do not reconstruct them
from search snippets. Ask the user to attach the
[published repository archive](https://github.com/popow-ai/plugin/archive/refs/heads/main.zip)
and continue with its `plugins/popow/skills/` files. This requires a file attachment.
Prompt-only updates are not established for every ChatGPT account.

Use the existing source's update path for a shared, reviewed or Git-managed plugin.
Do not create a duplicate to bypass editing restrictions. A private copy's version
can differ from the public release. Do not downgrade it to match the source version.

If no Popow app connection exists, open **Plugins → + → Add custom MCP server**
and use `https://latest.mcp.popow.ai/mcp` with the OAuth settings above.
Complete sign-in before adding the skills to an editable app-backed plugin.
An MCP-only connection does not install the skills.

If the host cannot inspect or update the plugin, report the missing capability
and the available UI action. Do not claim setup is complete from a capability
reply, a ZIP upload or a sign-in alone.
If tool names or schemas remain stale, open the connected Popow app's settings
and use **Refresh tools**, then start a new conversation. Refreshing tools and
updating bundled skills are separate actions.
See [OpenAI's connection guide](https://developers.openai.com/plugins/deploy/connect-chatgpt)
and [app-reference and access rules](https://learn.chatgpt.com/codex/enterprise/plugin-management).

## Check the connection

1. Check that the current host lists the Popow plugin and its skills as enabled.
2. Use `connecting-popow` and check that it calls Popow's `whoami`.
3. Check that `whoami` returns `authenticated: true` for the intended account
   before asking for references.

## Update

### Automatic updates

Plugin updates include the bundled skills. Updating the remote MCP server alone
does not update installed `SKILL.md` files.

**Claude web and desktop:** Use the Git marketplace's **Sync automatically** setting
described above. A manually uploaded ZIP does not establish source-based updates.

**Claude Code, direct CLI installation:** Open `/plugin` → **Marketplaces** → **popow** →
**Enable auto-update** once. After the first message in an interactive session,
Claude Code waits up to ten minutes before its background update check. Updated
plugins load on the next start. Use `/reload-plugins` to apply an update in the
current session.
See [Claude Code's update rules](https://code.claude.com/docs/en/plugins/loading#when-auto-update-runs).

**Codex CLI:** Keep `popow-ai/plugin` registered as the Git marketplace installed
above. Codex's startup flow automatically refreshes configured Git marketplaces
and their installed plugin files. Check startup warnings for update failures.
See the [official startup implementation](https://github.com/openai/codex/blob/rust-v0.167.0/codex-rs/core-plugins/src/manager.rs#L2891-L2970)
and [installed-plugin refresh](https://github.com/openai/codex/blob/rust-v0.167.0/codex-rs/core-plugins/src/manager.rs#L3048-L3108).
For ChatGPT desktop, check update behavior in that app. The CLI result alone
does not check the desktop app's automatic updates.

**ChatGPT personal web copies:** Use the app-backed update path above. Automatic
propagation from our Git repository to independently uploaded ZIP copies has not
been established. Workspace Git sync is a separate administrator-managed feature.

### Manual update

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
