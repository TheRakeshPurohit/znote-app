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

> First run: `npx` installs the package. Add `"--headless"` to the args
> for an invisible run; without it you **watch** the browser act —
> perfect for a demo.
>
> ⚠️ **The server drives your installed Chrome.** On a machine without
> Chrome, the first navigation fails and the AI just answers "I'm unable
> to access the page due to a browser error". Fix it without leaving the
> note — the server ships a tool for exactly this:
>
> ````markdown
> ```ai tools=playwright.browser_install
> Install the browser.
> ```
> ````
>
> (or run `npx playwright install chrome` in a terminal.)

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

## Debugging: see the real error, not the paraphrase

When a browser tool fails, the model tends to summarize ("a browser
error occurred") instead of showing the cause. Ask for the raw error —
this works for any MCP server, not just Playwright:

```ai tools=playwright
Navigate to https://example.com and if it fails, show me the EXACT
raw error message from the tool, verbatim, without rephrasing.
```

A message like `Chromium distribution 'chrome' is not found` means the
browser is missing → run the `browser_install` block above.

## Tips

- The accessibility snapshot (default) costs fewer tokens than a
  screenshot — the model "sees" the structure, not the pixels.
- Stay on sites where automation is allowed; for heavy, repeated scraping
  prefer an official API.
