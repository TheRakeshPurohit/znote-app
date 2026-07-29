# MCP · PostHog — product analytics in plain language

**Use case**: funnels, usage trends, feature flags — product questions asked
in plain language, the answers landing in the sprint-review note.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "posthog": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.posthog.com/mcp"],
      "env": {}
    }
  }
}
```

> **Official** remote server. Authentication via a personal API key
> (PostHog → Settings → Personal API keys), passed as a header with
> `mcp-remote --header "Authorization: Bearer phx_..."` when OAuth isn't
> offered on your instance.

**Exposed tools**: `insights-get-all`, `query-run`, `dashboards-get-all`,
`feature-flag-get-all`, `error-tracking-list`, `experiments-get-all`…

## Examples

### Sprint review

```ai tools=posthog
Over the last 14 days: active-user trend, top 5 events, and the
signup → first_project → first_export funnel. Where do we lose the
most people?
```

### Check a launch

```ai tools=posthog
The "dark-mode" feature shipped two weeks ago. How many users triggered
the dark_mode_enabled event, and does that segment's D7 retention
differ from the rest?
```

### Flag cleanup

```ai tools=posthog.feature-flag-get-all
List the feature flags at 100% rollout for more than 30 days —
candidates for removal from the code.
```

## Tips

- The numbers persisted in the note = the sprint recap writes itself.
- Cross with Stripe: "do paying users use the export feature more than
  free users?"
