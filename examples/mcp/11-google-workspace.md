# MCP · Google Workspace — Gmail, Drive, Calendar, Sheets

**Use case**: email triage and drafts, plus calendar and spreadsheets:
morning brief, guided reply drafts, reading a shared Sheet.

## Prerequisites

A Google Cloud project with a "Desktop app" OAuth client (client ID +
secret) and the Gmail / Drive / Calendar / Sheets APIs enabled.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "google": {
      "command": "uvx",
      "args": ["workspace-mcp"],
      "env": {
        "GOOGLE_OAUTH_CLIENT_ID": "xxx.apps.googleusercontent.com",
        "GOOGLE_OAUTH_CLIENT_SECRET": "GOCSPX-..."
      }
    }
  }
}
```

> `workspace-mcp` (taylorwilsdon) covers Gmail + Drive + Calendar + Sheets +
> Docs in a single Python server (launched via `uvx`). First run: browser
> OAuth. Single-product alternative: `@shinzolabs/gmail-mcp`.

**Exposed tools** (extract): `search_gmail_messages`, `draft_gmail_message`,
`list_calendar_events`, `create_event`, `read_sheet_values`, `search_drive`…

## Examples

### Morning brief

```ai tools=google
My brief for today: my meetings, then the important unread emails from
the last 24h (skip the newsletters). End with the 3 priorities you
infer from them.
```

### Guided reply draft

```ai tools=google
Find the latest email from sarah@acme.com about the partnership.
Draft a reply: we politely decline for this quarter, we suggest
revisiting in October. Save as draft, do not send.
```

### Read a Sheet

```ai tools=google
Read the "Pipeline" tab of the "Sales 2026" spreadsheet and give me
the deals in "negotiation" worth over $10k, sorted by closing date.
```

## Tips

- **Always draft, never send** in email prompts: you keep the final say
  before anything goes out.
- Calendar + Gmail in the same block makes the "morning brief" a
  spectacular demo.
