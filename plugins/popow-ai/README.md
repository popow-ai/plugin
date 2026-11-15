# Popow

Popow helps people making short-form content find reference videos and understand viewer comments. A Popow sign-in is required.

Search the analyzed TikTok library and live TikTok and Instagram sources. Ask for a topic, scene, date range or recorded-view threshold. Your AI app uses returned evidence to explain and group references, identify useful comments, and compare videos. Source failures and missing evidence are reported.

Save a reference with a note on request, find it again, update its note or remove the save. Show references as video cards or comparison sheets where the host supports MCP Apps.

Metrics are observations, not guarantees of current counts or performance. Creator and audience countries and demographics are not verified. Popow does not publish videos, message creators, remove watermarks or grant reuse rights.

## Getting started

Install the Popow plugin in your supported Claude app, then connect the Popow MCP server and sign in to your Popow account when prompted. Ask: "Find sunscreen reviews. Show the useful references and tell me what viewers said." To check the connected account, ask: "Check my Popow connection."

This package contains eleven workflow skills and connects to `https://mcp.popow.ai/mcp`. The MCP server runs remotely; this package does not start a local server.

[Documentation](https://popow.ai/plugin) · [Support](https://popow.ai/support) · [Privacy policy](https://popow.ai/privacy) · [Terms](https://popow.ai/terms)

## Data and network access

The plugin sends search requests, selected video links, and requested saves or notes to the declared Popow MCP server. Popow verifies the signed-in account and stores personal reference saves and notes and supports requests to change or remove them. Search and usage records may contain user-provided text and the verified account identifier.

For web research and connection recovery, skills may use the host app's search or browser tools to send search queries to its search provider, open public TikTok, Instagram, YouTube, or other source pages, and read the Popow installation guide on GitHub. Those host-managed requests are outside the declared Popow MCP connection and follow the host's permissions. The package contains no scripts, hooks, or local executable code.

## License

MIT. See [LICENSE](LICENSE).
