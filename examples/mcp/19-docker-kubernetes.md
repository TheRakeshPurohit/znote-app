# MCP · Docker & Kubernetes — infrastructure state, inline

**Use case**: living runbooks — "what's running?", "why does this pod keep
restarting?" — the answer inside the ops note, next to the procedure.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "docker": {
      "command": "uvx",
      "args": ["mcp-server-docker"]
    },
    "kubernetes": {
      "command": "npx",
      "args": ["-y", "mcp-server-kubernetes"],
      "env": { "ALLOW_ONLY_NON_DESTRUCTIVE_TOOLS": "true" }
    }
  }
}
```

> `mcp-server-docker` talks to the local Docker daemon;
> `mcp-server-kubernetes` (Flux159) uses your current kubeconfig. The
> `ALLOW_ONLY_NON_DESTRUCTIVE_TOOLS` flag removes delete/exec —
> recommended.

**Exposed tools**: Docker → `list_containers`, `fetch_container_logs`,
`create_container`… · K8s → `kubectl_get`, `kubectl_describe`,
`kubectl_logs`, `kubectl_rollout`…

## Examples

### Local diagnosis

```ai tools=docker
List the running containers with their uptime and usage. Does the
"postgres-dev" container show errors in its last 50 log lines?
```

### Namespace health

```ai tools=kubernetes
In the "production" namespace: which pods are not Running or restarted
in the last 24h? For each, the probable reason from describe and the
latest logs.
```

### Living runbook

```ai tools=kubernetes
Check the "api" deployment: ready replicas, image version, last
rollout. Compare with the procedure in @runbooks/deploy-api.md and
flag any drift.
```

## Tips

- A runbook note = the procedure in markdown **plus** the blocks that
  check the real state: documentation and diagnosis in one place.
- Keep the non-destructive mode; actions (restart, scale) deserve a human
  in the loop.
