# MCP · Figma — design context inside the specs

**Use case**: write specs that reference the real mockups — components,
copy, measurements — without the Figma ↔ editor round-trips.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "figma": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.figma.com/mcp"]
    }
  }
}
```

> **Official** Figma remote server (OAuth on first run, a Dev/Full seat is
> required for some tools). Local alternative: the Figma desktop app's Dev
> Mode MCP server (`http://127.0.0.1:3845/mcp` when enabled in
> Preferences), same config through `mcp-remote`.

**Exposed tools**: `get_design_context`, `get_screenshot`, `get_metadata`,
`get_variable_defs`…

## Examples

### Specs from a mockup

```ai tools=figma
Here is the onboarding screen frame:
https://www.figma.com/design/AbC123/App?node-id=42-7
Describe each screen, the exact copy, and draft the acceptance
criteria for implementation.
```

### Extract the tokens

```ai tools=figma.get_variable_defs
From the file https://www.figma.com/design/AbC123/Design-System:
list the color and spacing variables as a table
name → light value / dark value.
```

### Check the implementation

```ai tools=figma
Compare the mockup node-id=42-7 with what @notes/onboarding-impl.md
describes: what diverges (copy, step order, missing states)?
```

## Tips

- Paste the exact node URL (right click → Copy link to selection): the
  context is smaller and more reliable.
- Powerful combined with GitHub: "the mockup changed — which issues
  should we open?"
