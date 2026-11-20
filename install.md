# Install Popow

You need a Popow account. Choose your app below, install the plugin, then sign in.

## Claude web, desktop Chat and Cowork

1. Open **Customize → Plugins → Add → Add marketplace → Add from repository**.
2. Enter `https://github.com/popow-ai/plugin`, keep **Sync automatically** on, and add **Popow**.
3. Open **Popow → Connectors → Connect → Continue**.
4. Choose **Sign in now → Use your own OAuth client** and enter:
   - **Client ID:** `b459679b-695c-4f8c-bd33-c901f8156c41`
   - **Client secret:** leave empty.
5. Complete sign-in, then ask Claude: **“Check my Popow connection with whoami.”**

The result should be `authenticated: true`. If it is false, use the connector's
**Disconnect → Connect** once, complete sign-in, and check again.

<details>
<summary>Connection problems</summary>

- Choose **Sign in now** even if Claude detects **No authentication**. Use the
  client settings above; automatic registration and Claude's published ID are
  not supported by the current Popow connection.
- If the server URL already exists, open the existing connector. Do not create a
  duplicate. Changing OAuth settings may require removing and adding it again;
  check who uses it before removing a shared connector.
- For an unapproved request-header error, contact Popow Support with the exact
  error. Reinstalling will not approve the header.
- If skills are outdated, use the marketplace's **Check for updates**, then
  start a new conversation.

[Claude connector settings](https://claude.com/docs/connectors/custom/add-unlisted#edit-or-remove-a-connector)

</details>

## Codex CLI and desktop Code/Work

Run in a terminal:

```bash
codex plugin marketplace add popow-ai/plugin
codex plugin add popow@popow --json
codex -c mcp_oauth_callback_port=39603
```

Complete the Popow sign-in prompt in the new session, then ask:

```text
$popow:getting-started-with-popow Check my Popow connection and show me where to start.
```

## Claude Code

If Popow is already synced from your Claude account, use that installation.
For a direct CLI installation, run:

```bash
claude plugin marketplace add popow-ai/plugin
claude plugin install popow@popow --scope user
```

Start a new session. Run `/mcp`, select Popow, and choose **Authenticate**.
After signing in, ask:

```text
/popow:getting-started-with-popow Check my Popow connection and show me where to start.
```

## ChatGPT web and desktop Chat

Use a Popow app connection available to your account together with the Popow
plugin's skills. A connection alone does not install the skills.

If no connection exists, open **Plugins → + → Add custom MCP server**:

- **Server URL:** `https://latest.mcp.popow.ai/mcp`
- **Authentication:** OAuth
- **Client ID:** `b459679b-695c-4f8c-bd33-c901f8156c41`
- **Client secret:** leave empty.

Complete sign-in. For a private plugin you own, use
[Plugin Creator](https://chatgpt.com/plugins/plugin_connector_1p_e1a10c53223481918a42f1510ec46c1e)
to add or update the [published Popow skills](https://github.com/popow-ai/plugin/tree/main/plugins/popow/skills)
with that app connection. Then start a new conversation and ask it to check
Popow's `whoami`.

<details>
<summary>Private plugin setup and recovery</summary>

Preserve the existing plugin, app connection, permissions and account when
updating. For shared or Git-managed plugins, use their existing update path.
Do not create duplicates or replace an app reference with a raw MCP entry.

Uploading the Git package as a ZIP can produce a **Desktop only** plugin.
Another person's app ID does not grant access to their app. If Plugin Creator
cannot read the full skills, attach the
[published repository archive](https://github.com/popow-ai/plugin/archive/refs/heads/main.zip)
and use its `plugins/popow/skills/` files.

If tools are stale, use **Refresh tools** in the connected app's settings and
start a new conversation. Updating tools and updating skills are separate steps.
If the host cannot inspect or update the plugin, report the missing capability
and the exact UI action needed. Do not claim completion from a ZIP upload alone.

[OpenAI connection guide](https://developers.openai.com/plugins/deploy/connect-chatgpt)

</details>

## Updates

- **Claude web/desktop:** keep marketplace **Sync automatically** on.
- **Claude Code, direct CLI install:** open `/plugin → Marketplaces → popow → Enable auto-update`.
- **Codex CLI:** the registered Git marketplace refreshes at startup.
- **ChatGPT private copies:** update through Plugin Creator; automatic Git updates are not established.

Start a new session after updating. For manual CLI updates:

```bash
# Codex
codex plugin marketplace upgrade popow
codex plugin add popow@popow --json

# Claude Code
claude plugin marketplace update popow
claude plugin update popow@popow
```

## Ask your assistant to set up Popow

```text
Follow https://raw.githubusercontent.com/popow-ai/plugin/main/install.md to install or repair Popow in my current app.
Preserve my existing connection and enable automatic updates where supported.
Verify that the plugin skills are enabled and whoami returns authenticated: true.
If I need to do something, give me the exact next step for this app.
```

[Support](https://popow.ai/support) · [Privacy Policy](https://popow.ai/privacy) · [Terms of Service](https://popow.ai/terms)
