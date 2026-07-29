# MCP · Slack — the native standup digest

**Use case**: summarize a channel after a vacation, Monday-morning digest,
post a recap — the "Standup digest" workflow with no glue code.

## Prerequisites

A Slack app (api.slack.com/apps) with a token. Scopes:
`channels:history`, `channels:read`, `users:read`, and `chat:write` to
post. Install the app in the workspace and invite the bot to the channels
it should read.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "slack-mcp-server@latest", "--transport", "stdio"],
      "env": {
        "SLACK_MCP_XOXP_TOKEN": "xoxp-your-token"
      }
    }
  }
}
```

> The community `slack-mcp-server` (korotovsky) is the most complete. It
> accepts a bot (`xoxb`) or user (`xoxp`) token.

**Exposed tools**: `conversations_history`, `conversations_replies`,
`channels_list`, `search_messages`, `conversations_add_message`…

## Examples

### Monday digest

```ai tools=slack
Summarize the #engineering channel activity since Friday: decisions
made, problems raised, questions left unanswered. Monday-morning brief
format, 10 lines max.
```

### Back from vacation

```ai tools=slack
Summarize what I missed in #product and #general over the last 7 days.
Group by topic, mention who owns each one.
```

### Post a recap

```ai tools=slack
Post a 5-bullet summary of this meeting note to #product, prefixed
with "📋 Today's product sync recap:".
```

## Tips

- Cross-reference with Linear/GitHub: "what was said in #bugs but doesn't
  exist as an issue yet".
- A **user** token reads what you read; a **bot** token only reads where
  it's invited — choose based on workspace sensitivity.
