# MCP · Grafana — metrics and alerts in the post-mortem

**Use case**: during an incident or in a post-mortem, query dashboards,
Prometheus/Loki datasources and alerts — the numbers land in the note that
documents the incident.

## Prerequisites

A Grafana service account token (Administration → Service accounts), the
Viewer role is enough for reading.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "grafana": {
      "command": "docker",
      "args": [
        "run", "--rm", "-i",
        "-e", "GRAFANA_URL", "-e", "GRAFANA_SERVICE_ACCOUNT_TOKEN",
        "mcp/grafana", "-t", "stdio"
      ],
      "env": {
        "GRAFANA_URL": "https://grafana.mycompany.com",
        "GRAFANA_SERVICE_ACCOUNT_TOKEN": "glsa_..."
      }
    }
  }
}
```

> **Official** Grafana Labs server (Go). Without Docker: download the
> `mcp-grafana` binary from the GitHub releases and put its path in
> `command`.

**Exposed tools**: `search_dashboards`, `query_prometheus`, `query_loki_logs`,
`list_alert_rules`, `get_dashboard_by_uid`, `list_incidents`…

## Examples

### During the incident

```ai tools=grafana
Which alerts are currently firing? For each: since when, on which
service, and the current value versus the threshold.
```

### Post-mortem with numbers

```ai tools=grafana
Prometheus query: the API's p99 latency between 2pm and 6pm yesterday.
When did the spike start, and does it correlate with the 5xx error
rate?
```

### Targeted logs

```ai tools=grafana.query_loki_logs
The error logs of the "checkout" service between 2:30pm and 3pm
yesterday: which messages dominate?
```

## Tips

- The incident timeline writes itself into the note while you
  investigate — the post-mortem is already half drafted.
- Combine with Sentry: metrics (Grafana) + stack traces (Sentry) in the
  same analysis block.
