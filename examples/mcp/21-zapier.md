# MCP · Zapier — ~7,000 apps behind one server

**Use case**: connect the tools that have no dedicated MCP server (Trello,
Mailchimp, HubSpot, Typeform, Calendly…) with nothing to install: Zapier
acts as the hub and you pick exactly which actions to expose.

## Prerequisites

1. Zapier account → [mcp.zapier.com](https://mcp.zapier.com)
2. Create an MCP server, add actions to it (e.g. "Trello: Add Card",
   "Calendly: List Events")
3. Copy the server URL (it contains your secret)

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "zapier": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.zapier.com/api/mcp/s/YOUR-ID/sse"]
    }
  }
}
```

> The URL **is** the authentication: don't commit it in a shared vault
> (`.znote/mcp.json` can stay out of git via `.gitignore`).

**Exposed tools**: exactly the actions you ticked on the Zapier side — you
define the surface.

## Examples

### Personal kanban

```ai tools=zapier
Add a Trello card "Prepare the demo" to the "This week" list on the
Product board, due Friday.
```

### Prospecting

```ai tools=zapier
Look up the "acme.com" contact in HubSpot: last exchange, open deals.
Summarize before my 3pm call.
```

### External calendar

```ai tools=zapier
List my booked Calendly slots this week and draft a personalized
confirmation message for each invitee.
```

## Tips

- Start with 3-5 targeted actions: too many tools dilutes the model's
  precision (and each tool costs context).
- For a non-developer this is the MCP gateway: no token to generate,
  everything is configured in the Zapier UI.
