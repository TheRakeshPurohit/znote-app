# MCP · Atlassian — official Jira and Confluence

**Use case**: the classic "specs → Jira" workflow without a hand-built
plugin: Atlassian's official server covers Jira **and** Confluence, with
OAuth handled by Atlassian.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.atlassian.com/v1/sse"]
    }
  }
}
```

> First run: browser OAuth on your `*.atlassian.net` site. Self-hosted /
> API-token alternative: the community `mcp-atlassian` server (Python,
> `uvx mcp-atlassian`) with `JIRA_URL`, `JIRA_USERNAME` and
> `JIRA_API_TOKEN` in `env`.

**Exposed tools**: `createJiraIssue`, `searchJiraIssuesUsingJql`,
`editJiraIssue`, `getConfluencePage`, `createConfluencePage`,
`searchConfluenceUsingCql`…

## Examples

### Specs → tickets (the classic demo)

```ai tools=atlassian
Read @specs/onboarding-v2.md and break it into user stories in the
Jira project APP: one ticket per story, acceptance criteria in the
description, label "onboarding-v2".
```

### Morning brief

```ai tools=atlassian
JQL: the tickets in project APP's active sprint. Summarize: done /
in progress / blocked, and list the tickets without an assignee.
```

### Meeting notes → Confluence

```ai tools=atlassian
Turn this meeting note into a clean Confluence page in the "PRODUCT"
space, under the "Meeting notes" page, titled with today's date.
```

## Tips

- One block can mix both products: "create the Jira ticket AND the
  Confluence kickoff page".
- For read-only access (reporting), the community server accepts a
  reduced-scope token.
