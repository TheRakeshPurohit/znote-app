# MCP · Linear — tickets and cycles from your notes

**Use case**: specs → Linear issues, current-cycle summary, planning prep —
the modern alternative to Jira, in high demand with product teams.

## Configuration (.znote/mcp.json)

Linear exposes an official **remote** server. Until Znote supports HTTP
natively, the `mcp-remote` proxy bridges it over stdio and opens the browser
for OAuth on first launch:

```json
{
  "mcpServers": {
    "linear": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.linear.app/sse"]
    }
  }
}
```

> First run: a Linear page opens to authorize access; the token is cached
> locally (`~/.mcp-auth`).

**Exposed tools**: `list_issues`, `create_issue`, `update_issue`,
`list_projects`, `list_cycles`, `create_comment`, `search_documentation`…

## Examples

### Specs → issues

```ai tools=linear
Break these specs into user stories and create them in the "Product"
team, project "Onboarding v2", with a rough point estimate each:

The new onboarding must detect the system language, offer 3 workspace
templates on first launch, and allow importing an existing folder of
markdown files in one click.
```

### Cycle summary

```ai tools=linear
Summarize the Product team's current cycle: issues done, in progress,
not started. Flag what's at risk of slipping and why.
```

### My day

```ai tools=linear.list_issues
List my assigned issues sorted by priority, with their status and age.
Bold anything marked "urgent".
```

## Tips

- Keep the specs note: the "what we wrote → what was created" trail stays
  in the vault, dated.
- `tools=linear,github` in one block: "link each Linear issue in the cycle
  to its matching GitHub PR".
