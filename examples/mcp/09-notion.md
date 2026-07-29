# MCP · Notion — read, write… and migrate to the vault

**Use case**: keep a foot in Notion during a transition, publish meeting
recaps to the team space, or **migrate** Notion pages into local markdown
notes.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.notion.com/sse"]
    }
  }
}
```

> Official remote server, OAuth on first run. Token alternative:
> `npx -y @notionhq/notion-mcp-server` with
> `"env": { "NOTION_TOKEN": "ntn_..." }` (create an internal integration at
> notion.so/my-integrations, share the pages with it).

**Exposed tools**: `search`, `fetch`, `create_pages`, `update_page`,
`move_pages`, `notion_create_comment`…

## Examples

### Notion → vault migration

```ai tools=notion
Find the "Product roadmap 2026" page in Notion, fetch its full content
(including subpages) and rewrite it here as clean markdown: headings,
tables, lists. I'll keep it as a local note.
```

### Publish a recap

```ai tools=notion
Create a "Weekly sync — July 28" page in the "Team" space with a
summary of this note, formatted with To do / Decisions sections.
```

### Cross-workspace search

```ai tools=notion.search
Find every Notion page mentioning "pricing v3" and give me the link
plus one line of context for each.
```

## Tips

- The migration angle is a strong one: "your Notion pages become .md
  files you own".
- Limit a token-based integration to the shared pages: minimal scope.
