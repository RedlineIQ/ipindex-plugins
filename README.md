# IPIndex plugins

Official IPIndex plugin for Claude, published by BroadNarrow Labs, LLC.

IPIndex searches official patent, trademark, and copyright records in the
United States (USPTO and U.S. Copyright Office), Europe and worldwide (EPO
DOCDB/INPADOC patent publications), and Canada (CIPO patents and trademarks).
It traces recorded assignments and builds citation-backed IP diligence reports,
all through the hosted IPIndex service at `https://mcp.ipindex.ai/mcp`.

| Plugin | Folder |
| --- | --- |
| IPIndex for Claude | [`ipindex-claude-plugin/`](ipindex-claude-plugin/) |

## Install

Add IPIndex from the Claude directory. To install it from this repository in
Claude Code instead:

```
/plugin install ipindex --marketplace RedlineIQ/ipindex-plugins
```

Then choose **Connect**, sign in to IPIndex, and approve access. IPIndex
requires an account with an IPIndex Pro subscription.

The plugin contains one skill and one remote MCP server connection. It runs no
local programs, hooks, or scripts and contains no credentials.

## Links

- Help: https://mcp.ipindex.ai/support
- Website: https://www.ipindex.ai
- Privacy: https://www.ipindex.ai/privacy
- Terms: https://www.ipindex.ai/terms
- Email: info@ipindex.ai
