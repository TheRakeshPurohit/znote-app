# MCP · Composio — the developer-oriented integration hub

**Use case**: like Zapier, a single server for hundreds of apps (~250:
GitHub, Notion, Slack, Salesforce, Discord…), but developer-minded: OAuth
handled by Composio, fine-grained tool selection, an SDK if needed.

## Prerequisites

1. Account at [composio.dev](https://composio.dev) → API key
2. In the dashboard, connect the apps you want (2-click OAuth per app)
3. Create an MCP server and copy its URL

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "composio": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.composio.dev/composio/server/YOUR-ID/mcp"]
    }
  }
}
```

> Same caution as Zapier: the URL carries the access. Per-app variant:
> Composio also publishes single-app servers if you prefer one server =
> one app.

**Exposed tools**: those of the connected apps, with clean schemas and
well-written descriptions (good tool-call success rate).

## Examples

### Multi-app in one prompt

```ai tools=composio
Summarize the last 5 GitHub issues of the acme/webapp repo, post the
summary to the #dev Slack channel, and add a line to my "Daily log"
Notion database with today's date.
```

### CRM

```ai tools=composio
In Salesforce: the opportunities closing this month, sorted by amount.
Which ones have had no activity for 7 days?
```

### Community

```ai tools=composio
Read the last 20 messages in the Discord #feedback channel and group
the feature requests by theme with a count.
```

## Tips

- Composio vs Zapier: Composio has a more generous free tier for
  developers and more reliable tool schemas; Zapier covers more
  mainstream apps.
- Limit the tools exposed per server (dashboard → tool selection): the
  model chooses better among 10 tools than among 200.
