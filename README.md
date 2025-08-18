# Claude Code MCP Setup Guide

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MCP Version](https://img.shields.io/badge/MCP-Protocol-blue)](https://modelcontextprotocol.io)
[![Claude Code](https://img.shields.io/badge/Claude-Code-orange)](https://docs.anthropic.com/en/docs/claude-code)

![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code?label=Claude%20Code)

![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code?style=flat-square)

[![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code)](https://www.npmjs.com/package/@anthropic-ai/claude-code)

A practical guide for setting up Model Context Protocol (MCP) servers with Claude Code.

### Basic Installation

```bash
# Add a filesystem server
claude mcp add filesystem npx -y @modelcontextprotocol/server-filesystem ~/Documents

# Add GitHub integration
claude mcp add github npx -y @modelcontextprotocol/server-github \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=ghp_yourtoken

# Check server status
/mcp
```

## Common MCP Servers

| Server | Installation | Purpose |
|--------|-------------|---------|
| Filesystem | `claude mcp add fs npx -y @modelcontextprotocol/server-filesystem ~/path` | File access |
| GitHub | `claude mcp add github npx -y @modelcontextprotocol/server-github -e GITHUB_PERSONAL_ACCESS_TOKEN=token` | Repo management |
| PostgreSQL | `claude mcp add postgres npx -y @modelcontextprotocol/server-postgres "postgresql://..."` | Database queries |
| Memory | `claude mcp add memory "npx -y @modelcontextprotocol/server-memory"` | Persistent context |
| Slack | `claude mcp add slack "npx -y @modelcontextprotocol/server-slack"` | Team messaging |
| Brave Search | `claude mcp add brave npx -y @modelcontextprotocol/server-brave-search -e BRAVE_API_KEY=key` | Web search |

## Server Scopes

- **Local** (default): Current project only
- **Project** (`-s project`): Team shared via `.mcp.json`  
- **User** (`-s user`): All your projects

## Team Setup

1. Add servers with project scope:
```bash
claude mcp add github npx -y @modelcontextprotocol/server-github -s project
```

2. This creates `.mcp.json`:
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    }
  }
}
```

3. Create `.env.example`:
```
GITHUB_TOKEN=ghp_your_token_here
DATABASE_URL=postgresql://user:pass@localhost:5432/db
```

4. Commit to version control:
```bash
git add .mcp.json .env.example
echo ".env" >> .gitignore
git commit -m "Add MCP configuration"
```

## Usage in Claude Code

- `/mcp` - Check server status
- `/mcp__servername__command` - Use server commands
- `@servername:resource` - Access server resources

## Managing Servers

```bash
claude mcp list                    # List all servers
claude mcp get servername          # Get server details
claude mcp remove servername       # Remove a server
claude mcp reset-project-choices   # Reset project approvals
```

## Troubleshooting

### Logs
```bash
tail -f ~/.claude/logs/mcp-server-*.log
```

### Direct Config Edit
Location: `~/.claude/.claude.json`

### Common Issues
- **"Command not found"**: Ensure npx is in PATH
- **Server not showing**: Restart Claude Code
- **Permission denied**: Run `claude /doctor`

## Security

⚠️ **Important**: 
- Only use trusted MCP servers
- Be cautious with internet-connected servers
- Never commit API keys to version control
- Use read-only database access where possible

## Resources

- [Official MCP Documentation](https://modelcontextprotocol.io)
- [MCP Servers Repository](https://github.com/modelcontextprotocol/servers)
- [Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code/mcp)

## License

This guide is provided under MIT License. MCP is open source by Anthropic.
