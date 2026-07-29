# MCP · Postgres — natural-language SQL, schema included

**Use case**: query your production database (read-only) without writing the
SQL yourself. The server exposes the **introspected schema**, so the model
knows your tables and columns — no more hallucinated queries.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-postgres",
        "postgresql://readonly_user:password@localhost:5432/mydb"
      ]
    }
  }
}
```

> Create a dedicated **readonly** role: the reference server only runs
> read queries, but a restricted role stays best practice.

**Exposed tools**: `query` (read-only SQL) + the table schemas published as
resources.

## Examples

### Direct business question

```ai tools=postgres
How many orders were placed this month, broken down by acquisition
channel? Present the result as a table with each channel's % of total.
```

### Schema exploration

```ai tools=postgres
Which tables reference the users table (foreign keys)? For each one,
give the column and an estimated row count.
```

### Reusable weekly report

```ai tools=postgres
Build the weekly report: new customers, MRR, churn. Compare with the
previous week and flag any variation above 10%.
```

## Tips

- Keep the note: re-running the block next week regenerates the report —
  it's your saved query, in plain English.
- For hand-written SQL with an inline chart, the ```js block + DB plugin
  stays complementary: MCP shines for exploration, js for the repeatable.
