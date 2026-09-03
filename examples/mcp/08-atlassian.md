# MCP · Atlassian — official Jira and Confluence

**Use case**: the classic “specs → Jira” workflow without a custom plugin: the community server `mcp-atlassian` exposes both Jira **and** Confluence, with authentication via URL, email, and an Atlassian API token.

## Configuration (`.znote/mcp.json`)

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "uvx",
      "args": ["mcp-atlassian"],
      "env": {
        "JIRA_URL": "https://your-site.atlassian.net",
        "JIRA_USERNAME": "you@example.com",
        "JIRA_API_TOKEN": "your_api_token",
        "CONFLUENCE_URL": "https://your-company.atlassian.net/wiki",
        "CONFLUENCE_USERNAME": "your.email@company.com",
        "CONFLUENCE_API_TOKEN": "your_api_token"
      }
    }
  }
}
```

> To create an Atlassian API token, open  
> `https://id.atlassian.com/manage-profile/security/api-tokens`, create a token, then set its value in `JIRA_API_TOKEN`.  
> `JIRA_URL` must point to your `*.atlassian.net` site, and `JIRA_USERNAME` is usually your Atlassian email address.

**Tools exposed**: `createJiraIssue`, `searchJiraIssuesUsingJql`, `editJiraIssue`, `getConfluencePage`, `createConfluencePage`, `searchConfluenceUsingCql`…

## Examples

### Show me my current tickets

```ai tools=atlassian
Show me my current tickets in Jira: the issues assigned to me that are
in progress or in the active sprint. Summarize them by status and flag
anything blocked.
```

### Specs → tickets (the classic demo)

```ai tools=atlassian
Read @specs/onboarding-v2.md and break it into user stories in the
Jira project APP: one ticket per story, acceptance criteria in the
description, label "onboarding-v2".
```

### Meeting notes → Confluence

```ai tools=atlassian
Turn this @meetins/review.md note into a clean Confluence page in the "PRODUCT" space, under the "Meeting notes" page, titled with today's date.
```

## Tips

- A single block can mix both products: “create the Jira ticket AND the Confluence kickoff page”.
- For read-only access (reporting), the community server also supports a reduced-scope token.
