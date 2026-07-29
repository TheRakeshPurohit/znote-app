# MCP · Fetch — a URL becomes markdown context

**Use case**: pull a web page's content (docs, article, changelog, competitor
pricing) into the answer — converted to clean markdown, more targeted than
web search.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "fetch": {
      "command": "uvx",
      "args": ["mcp-server-fetch"]
    }
  }
}
```

> Python reference server, launched by `uvx` (install
> [uv](https://docs.astral.sh/uv/)). It paginates long pages automatically
> (`start_index`).

**Exposed tool**: `fetch(url, max_length, start_index, raw)`.

## Examples

### Summarize an article

```ai tools=fetch
Fetch https://example.com/blog/important-post and give me a 5-bullet
summary with the key quotes.
```

### Competitive watch

```ai tools=fetch
Compare the pricing pages at https://competitor-a.com/pricing and
https://competitor-b.com/pricing: table of plans, prices, and
positioning differences.
```

### Track a changelog

```ai tools=fetch
Read https://github.com/electron/electron/releases and tell me what
changed since v36 that could impact an app in production.
```

## Tips

- Combine with `websearch=true`: the search finds the URLs, fetch reads
  them in depth.
- The result stays in the note: your research becomes a dated history.
