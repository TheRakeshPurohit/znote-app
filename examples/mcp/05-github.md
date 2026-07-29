# MCP · GitHub — issues, PRs and code from a note

**Use case**: automatic standup, issue triage, PR review, creating issues
from meeting notes — all versioned in your vault.

## Prerequisites

A Personal Access Token (fine-grained): GitHub → Settings → Developer
settings → Tokens. Useful scopes: `repo` (or read-only: `public_repo`,
`read:org`).

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": { "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_token" }
    }
  }
}
```

> Official Go alternative: `github-mcp-server` (binary or Docker), more
> complete (Actions, code scanning). The npx config above is enough to
> get started.

**Exposed tools**: `search_repositories`, `list_issues`, `create_issue`,
`get_pull_request`, `list_commits`, `search_code`, `create_pull_request`…

## Examples

### Morning standup

```ai tools=github
On the acme/webapp repo: list the open PRs with their age, the issues
created in the last 24h, and yesterday's commits on main.
Format: a 3-section standup brief.
```

### Meeting notes → issues

```ai tools=github
Here are my meeting notes. Create one issue per decided action on the
acme/webapp repo, with a clear title and the context as description:

- the login crash on Safari needs to be re-tested
- add a keyboard shortcut to close all tabs
- the Linux install docs are outdated
```

### Triage

```ai tools=github
List the open unlabeled issues on acme/webapp and propose a label for
each (bug / feature / docs / question) with a one-line justification.
```

## Tips

- `tools=github.list_issues` for strictly read-only access.
- Cross-reference with the vault: "compare the roadmap in @roadmap.md
  with the open issues — what's missing?"
