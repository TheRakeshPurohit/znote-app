# MCP · GitLab — for enterprise teams

**Use case**: same value as the GitHub server (standup, triage, MRs) but for
organizations on GitLab — often self-hosted in the enterprise.

## Prerequisites

A Personal Access Token (Preferences → Access Tokens), scope `api` or
`read_api` for read-only use.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "gitlab": {
      "command": "npx",
      "args": ["-y", "@zereight/mcp-gitlab"],
      "env": {
        "GITLAB_PERSONAL_ACCESS_TOKEN": "glpat-...",
        "GITLAB_API_URL": "https://gitlab.mycompany.com/api/v4",
        "GITLAB_READ_ONLY_MODE": "false"
      }
    }
  }
}
```

> `GITLAB_API_URL` points at your self-hosted instance (default:
> gitlab.com). `GITLAB_READ_ONLY_MODE=true` exposes only the read tools.

**Exposed tools**: `list_issues`, `create_issue`, `list_merge_requests`,
`get_merge_request_diffs`, `create_merge_request_note`, `list_pipelines`…

## Examples

### Pending MR review

```ai tools=gitlab
List the open merge requests in group/webapp waiting for review for
more than 2 days: title, author, diff size. Who is blocking what?
```

### Pipeline health

```ai tools=gitlab
The last 10 pipelines on the main branch: status, duration. If jobs
fail recurrently, which ones?
```

### Notes → issues

```ai tools=gitlab
Create one issue per action item from this retro in group/webapp,
label "retro-S31":
- automate the changelog
- document the rollback procedure
```

## Tips

- Read-only mode is ideal for giving the tool to the whole team without
  write risk.
- Self-hosted = no data leaves the infrastructure: consistent with a
  local-first setup.
