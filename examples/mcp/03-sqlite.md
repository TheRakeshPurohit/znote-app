# MCP · SQLite — query a local database

**Use case**: dig into a .db/.sqlite export (local analytics, an app's
database, a client file) without installing a GUI tool.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "sqlite": {
      "command": "uvx",
      "args": ["--with", "mcp<2", "mcp-server-sqlite", "--db-path", "~/data/app.db"]
    }
  }
}
```

> This server is Python: `uvx` (ships with [uv](https://docs.astral.sh/uv/),
> `brew install uv`) runs it without installing. The `--with mcp<2` pin is
> required: this archived reference server breaks with the MCP 2.x SDK
> (`AttributeError: 'Server' object has no attribute 'list_resources'`).
> Node alternative, no Python: `npx -y mcp-sqlite ~/data/app.db`.
>
> ⚠️ **The path must point at an existing database**: SQLite silently
> creates an empty file when the path is new — the model will then answer
> "no tables". Check with `ls` before configuring.

**Exposed tools**: `read_query`, `write_query`, `list_tables`,
`describe_table`, `create_table`…

## Examples

### Discovering the database

```ai tools=sqlite
List the tables in this database, describe the columns of the 3 largest,
and tell me what this database seems to store.
```

### Analysis

```ai tools=sqlite.read_query
What are the 10 most frequent events in the events table over the last
30 days? Add the trend versus the previous month.
```

### Guided cleanup (writes)

```ai tools=sqlite
Find the duplicates in the contacts table (same email), show them to me,
then propose the DELETE query — do not run it without my approval.
```

## Tips

- `tools=sqlite.read_query` = read-only guardrail.
- Work on a **copy** of the .sqlite file for any session that involves
  writes.
