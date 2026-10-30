# Install Popow

Popow adds TikTok creative-reference search to Codex and Claude Code. Install
the plugin to get the Popow skill and its MCP connection together.
A Popow account is required.

Use the instructions for the app the user wants to connect. Run the commands
on the user's computer. If you cannot run commands there, give the user these
steps and wait for them to complete installation.

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

1. Check that the host lists `popow@popow` as installed and enabled.
2. Invoke the skill and check that its reply describes TikTok reference search.
3. Ask the host to call Popow's `whoami`. Check the returned account before
   asking for references.

Report installation, skill invocation and account connection separately.
A capability reply alone does not establish a successful account connection.
If authentication fails, report the exact error and use the host's sign-in flow.
Never ask the user to paste passwords or tokens into chat.

If a `popow` marketplace already exists, check its source in the host's plugin
settings before replacing it. Removing a Claude Code marketplace can also
remove its plugins and saved data. Keep an existing connection until the new
plugin works, then remove duplicate MCP registrations through the host settings.

## Update

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
