# Connect Claude Code

## With the plugin (connector and skill)

```text
/plugin marketplace add zuperbase/zuperbase-mcp
/plugin install zuperbase@zuperbase
```

Restart Claude Code, type `/mcp`, choose **zuperbase** and sign in in the browser window that opens.

## Connector only

```bash
claude mcp add --transport http zuperbase https://mcp.zuperbase.co/mcp
```

Then `/mcp` › **zuperbase** › sign in.

The connector's prompts appear as commands, for example `/mcp__zuperbase__setup_interview` and
`/mcp__zuperbase__month_end`.
