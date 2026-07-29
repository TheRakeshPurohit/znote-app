# MCP · Playwright — a browser driven from the note

**Use case**: scrape a dynamic (JS) page, fill a form, take screenshots,
verify a user flow works — the AI drives a real Chrome.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```

> First run: `npx` installs the package and the browser. Add
> `"--headless"` to the args for an invisible run; without it you **watch**
> the browser act — perfect for a demo.

**Exposed tools**: `browser_navigate`, `browser_click`, `browser_type`,
`browser_snapshot` (accessibility), `browser_take_screenshot`,
`browser_fill_form`, `browser_evaluate`…

## Examples

### Scrape a dynamic page

```ai tools=playwright
Go to https://news.ycombinator.com, grab the first 10 titles with their
scores, and render them as a markdown table sorted by score.
```

### Verify a critical flow

```ai tools=playwright
Open https://app.example.com, click "Sign in", enter
demo@example.com / demo1234, and tell me whether the dashboard loads.
Describe what you see at every step.
```

### Quick landing-page audit

```ai tools=playwright
Load https://example.com, list the broken links in the menu and the
footer, and check that the download buttons point to URLs that respond.
```

## Tips

- The accessibility snapshot (default) costs fewer tokens than a
  screenshot — the model "sees" the structure, not the pixels.
- Stay on sites where automation is allowed; for heavy, repeated scraping
  prefer an official API.
