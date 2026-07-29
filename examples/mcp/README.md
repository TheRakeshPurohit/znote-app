# MCP examples for Znote

One file per MCP server, in roadmap priority order. Every note is a
**ready-to-run** example: open this folder as a Znote vault (or copy a note
into your own vault), click the "＋ mcp.json" button on the config block (or
paste it via Settings → MCP → *Open mcp.json*), then run the ```ai blocks
with ▶.

## Syntax

- `tools=<server>` — exposes **all** the server's tools to the model.
- `tools=<server>.<tool>` — exposes a single tool.
- `tools=github,postgres` — several servers (and JS functions) combine freely.

## Requirements: server runtimes

Servers launch with `npx` (**Node.js** ecosystem) or `uvx` (**Python**
ecosystem, the [uv](https://docs.astral.sh/uv/) tool). If the Test in
Settings → MCP shows `command 'uvx' not found` (or `npx`), install the
matching runtime, then Test again (**Windows: restart Znote first** — a
running app doesn't see a freshly installed runtime):

| OS | Node.js (`npx`) | uv (`uvx`) |
|----|-----------------|------------|
| **macOS** | `brew install node` | `brew install uv` |
| **Windows** | `winget install OpenJS.NodeJS.LTS` | `winget install astral-sh.uv` |
| **Linux** | `apt install nodejs npm` (or [nvm](https://github.com/nvm-sh/nvm)) | `curl -LsSf https://astral.sh/uv/install.sh \| sh` |

Without a package manager: [nodejs.org](https://nodejs.org) and
[docs.astral.sh/uv/getting-started/installation](https://docs.astral.sh/uv/getting-started/installation/).
Znote looks for binaries in the standard locations (Homebrew,
`~/.local/bin`, `~/.cargo/bin`); for an exotic install, put the binary's
absolute path in `"command"` (given by `which uvx` / `where npx`).

## Phase 1 — stdio, no OAuth

| # | Server | Note |
|---|--------|------|
| 1 | Filesystem | [01-filesystem.md](01-filesystem.md) |
| 2 | Postgres | [02-postgres.md](02-postgres.md) |
| 3 | SQLite | [03-sqlite.md](03-sqlite.md) |
| 4 | Fetch | [04-fetch.md](04-fetch.md) |
| 5 | GitHub | [05-github.md](05-github.md) |
| 6 | Playwright | [06-playwright.md](06-playwright.md) |

## Phase 2 — remote / tokens

| # | Server | Note |
|---|--------|------|
| 7 | Linear | [07-linear.md](07-linear.md) |
| 8 | Atlassian (Jira/Confluence) | [08-atlassian.md](08-atlassian.md) |
| 9 | Notion | [09-notion.md](09-notion.md) |
| 10 | Slack | [10-slack.md](10-slack.md) |
| 11 | Google Workspace | [11-google-workspace.md](11-google-workspace.md) |
| 12 | Stripe | [12-stripe.md](12-stripe.md) |

## Phase 3 — broader ecosystem

| # | Server | Note |
|---|--------|------|
| 13 | Sentry | [13-sentry.md](13-sentry.md) |
| 14 | PostHog | [14-posthog.md](14-posthog.md) |
| 15 | Brave Search | [15-brave-search.md](15-brave-search.md) |
| 16 | GitLab | [16-gitlab.md](16-gitlab.md) |
| 17 | Figma | [17-figma.md](17-figma.md) |
| 18 | Grafana | [18-grafana.md](18-grafana.md) |
| 19 | Docker / Kubernetes | [19-docker-kubernetes.md](19-docker-kubernetes.md) |
| 20 | Supabase / Neon / Vercel / Cloudflare | [20-cloud-infra.md](20-cloud-infra.md) |

## Phase 4 — meta-servers

| # | Server | Note |
|---|--------|------|
| 21 | Zapier | [21-zapier.md](21-zapier.md) |
| 22 | Composio | [22-composio.md](22-composio.md) |

> **Remote HTTP/SSE**: Znote's current client speaks **stdio**. Remote
> servers (Linear, Notion…) connect through the `mcp-remote` proxy
> (`npx -y mcp-remote <url>`), which also handles the browser OAuth flow —
> each relevant note shows the exact config.
