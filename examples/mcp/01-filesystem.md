# MCP · Filesystem — the AI reads files outside your vault

**Use case**: analyze logs, summarize a specs folder, inventory a repo —
without linking the files into the vault. The ideal server to try MCP with:
no token, no account.

## Configuration (.znote/mcp.json)

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/me/Projects", "/Users/me/Downloads"]
    }
  }
}
```

> Every path passed as an argument is an **allowed** directory — the server
> refuses anything outside them. First launch: `npx` downloads the package,
> allow a few seconds.

**Exposed tools**: `read_text_file`, `write_file`, `list_directory`,
`directory_tree`, `search_files`, `get_file_info`, `move_file`…

## Examples

### Folder inventory

```ai tools=filesystem
List the contents of /Users/me/Projects, then give me a table of the
subfolders with their last-modified dates.
```

### Log analysis

```ai tools=filesystem
Read /Users/me/Projects/api/logs/error.log and give me the top 5 most
frequent errors with one sample stack trace each.
```

### Multi-file search

```ai tools=filesystem
Find every TODO.md file under /Users/me/Projects and consolidate their
open items into a single prioritized list.
```

### A single tool, read-only

```ai tools=filesystem.read_text_file
Read /Users/me/Downloads/export.csv and tell me how many rows have an
empty "status" field.
```

## Tips

- `tools=filesystem.read_text_file` restricts the model to reading: no
  accidental writes possible.
- Combine with your notes: "compare @specs/api.md with the actual code in
  /Users/me/Projects/api/routes/".
