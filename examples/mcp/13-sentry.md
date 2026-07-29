# MCP · Sentry — post-mortems and error triage

**Use case**: "what broke last night?" — production errors analyzed inside
the post-mortem note, with stack traces and frequencies.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "sentry": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.sentry.dev/mcp"]
    }
  }
}
```

> **Official** remote server (OAuth on first run). Self-hosted: the
> `@sentry/mcp-server` package over stdio with `SENTRY_ACCESS_TOKEN` and
> `SENTRY_HOST` in `env`.

**Exposed tools**: `find_issues`, `get_issue_details`, `find_errors_in_file`,
`update_issue`, `find_releases`, `get_trace_details`…

## Examples

### The morning after a deploy

```ai tools=sentry
Which new errors appeared in the last 24h on the "web-app" project?
For the top 3: message, frequency, users affected, and your reading of
the probable cause from the stack trace.
```

### Structured post-mortem

```ai tools=sentry
Detail issue WEB-APP-1234: first/last occurrence, volume, breadcrumbs.
Draft the start of a post-mortem: impact, cause hypothesis, proposed
actions.
```

### Code ↔ errors link

```ai tools=sentry.find_errors_in_file
Are there recent errors pointing at the file src/api/checkout.js?
If so, which ones and at which lines?
```

## Tips

- Combine with GitHub: "for each top-3 error, is there an open GitHub
  issue? If not, create it with the stack trace".
- The post-mortem note keeps the results: the incident's context is still
  readable six months later.
