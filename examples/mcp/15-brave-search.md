# MCP · Brave Search — structured web search

**Use case**: research, comparisons, fact-checking — a web search whose
results (titles, URLs, snippets) reach the model structured, complementing
Znote's built-in `websearch=true`.

## Prerequisites

A free API key at [brave.com/search/api](https://brave.com/search/api)
(2,000 requests/month included).

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "brave": {
      "command": "npx",
      "args": ["-y", "@brave/brave-search-mcp-server"],
      "env": { "BRAVE_API_KEY": "BSA..." }
    }
  }
}
```

> Paid, more AI-oriented alternatives: Exa (`exa-mcp-server`) for semantic
> search, Tavily (`tavily-mcp`) for search + extraction.

**Exposed tools**: `brave_web_search`, `brave_news_search`,
`brave_local_search`, `brave_image_search`, `brave_summarizer`…

## Examples

### Targeted research

```ai tools=brave
Search for announcements from the last 30 days about the Model Context
Protocol: new integrations, spec changes. Give sources with dates.
```

### Sourced comparison

```ai tools=brave
Compare markdown note apps with code execution (2026). Table: name,
price, local-first or cloud, strengths. Cite your sources.
```

### News in context

```ai tools=brave.brave_news_search
What's this week's news about Electron? Keep what concerns security or
breaking changes.
```

## Tips

- Brave via MCP gives the model **control** of the search (successive
  queries, reformulation) — more agentic than the built-in websearch.
- Chain with fetch: brave finds, fetch reads the full article.
