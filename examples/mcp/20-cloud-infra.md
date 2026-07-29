# MCP · Supabase, Neon, Vercel, Cloudflare — the modern stack

**Use case**: the typical indie-dev stack — Supabase/Neon database, frontend
on Vercel, DNS/workers on Cloudflare — administered and queried from project
notes. All four have **official** MCP servers.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "supabase": {
      "command": "npx",
      "args": ["-y", "@supabase/mcp-server-supabase@latest", "--read-only"],
      "env": { "SUPABASE_ACCESS_TOKEN": "sbp_..." }
    },
    "neon": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.neon.tech/sse"]
    },
    "vercel": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.vercel.com"]
    },
    "cloudflare": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://observability.mcp.cloudflare.com/sse"]
    }
  }
}
```

> Supabase: personal token + the recommended `--read-only` flag. Neon,
> Vercel and Cloudflare: remote servers with OAuth through `mcp-remote`.

## Examples

### Supabase — schema and data

```ai tools=supabase
On my Supabase project: list the tables with their row counts, and
flag the ones without Row Level Security enabled.
```

### Vercel — deployment status

```ai tools=vercel
The last 5 deployments of the "marketing-site" project: status,
duration, branch. Does the latest build have warnings?
```

### Cloudflare — traffic and errors

```ai tools=cloudflare
On the example.com zone: requests and error rate over the last 24h.
Is there an unusual spike, and from which countries?
```

### Neon — database branches

```ai tools=neon
List my Neon database branches with their sizes. Can the ones created
for previews more than 30 days ago be deleted?
```

## Tips

- One "infra.md" note per project with these four blocks = a small
  actionable status page, re-runnable before every production push.
- Always `--read-only` / minimal-scope tokens: reading covers 90% of the
  use cases.
