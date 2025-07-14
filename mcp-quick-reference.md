# Claude Code MCP Quick Reference

## Essential Commands

### Installation Commands
```bash
# Add local stdio server
claude mcp add <n> <command> [args...]

# Add SSE/HTTP server
claude mcp add --transport sse <n> <url>

# Add with environment variables
claude mcp add <n> <command> -e KEY=value

# Add from JSON
claude mcp add-json <n> '<json>'

# Import from Claude Desktop (macOS/WSL only)
claude mcp import-from-claude-desktop
```

### Scope Flags
```bash
-s local     # Current project only (default)
-s project   # Team shared via .mcp.json
-s user      # All your projects
```

### Management Commands
```bash
# List all configured servers
claude mcp list

# Get details for a specific server
claude mcp get <n>

# Remove a server
claude mcp remove <n>

# Reset project approvals
claude mcp reset-project-choices
```

### In-Session Commands
```
/mcp                          # Check server status
/mcp__server__command         # Use server command
@server:resource              # Access server resource
```

## Official MCP Server Installations

### Filesystem Access
```bash
claude mcp add fs npx -y @modelcontextprotocol/server-filesystem ~/Documents
```

### GitHub Integration  
```bash
claude mcp add github npx -y @modelcontextprotocol/server-github \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=ghp_xxx
```

### PostgreSQL Database
```bash
claude mcp add postgres npx -y @modelcontextprotocol/server-postgres \
  "postgresql://user:pass@localhost:5432/db"
```

### Slack Integration
```bash
claude mcp add slack npx -y @modelcontextprotocol/server-slack
```

### Google Drive
```bash
claude mcp add gdrive npx -y @modelcontextprotocol/server-gdrive
```

### Memory (Persistent Context)
```bash
claude mcp add memory npx -y @modelcontextprotocol/server-memory
```

### Git (Python)
```bash
# With uvx (recommended)
claude mcp add git uvx mcp-server-git --repository /path/to/repo

# With pip
claude mcp add git python -m mcp_server_git --repository /path/to/repo
```

### Brave Search
```bash
claude mcp add brave npx -y @modelcontextprotocol/server-brave-search \
  -e BRAVE_API_KEY=xxx
```

### Puppeteer (Browser Automation)
```bash
claude mcp add puppeteer npx -y @modelcontextprotocol/server-puppeteer
```

### Sequential Thinking
```bash
claude mcp add thinking npx -y @modelcontextprotocol/server-sequentialthinking
```

## Environment Variables

### Timeout Configuration
```bash
MCP_TIMEOUT=10000 claude    # 10 second timeout (default: 5000ms)
```

### Debug Mode
```bash
MCP_DEBUG=true claude       # Enable debug logging
```

## Log Locations

```bash
# View logs directory
ls -la ~/.claude/logs/

# Follow all MCP server logs
tail -f ~/.claude/logs/mcp-server-*.log

# Follow specific server log
tail -f ~/.claude/logs/mcp-server-SERVERNAME.log
```

## Configuration Files

- **User config**: `~/.claude/.claude.json` (Linux/WSL)
- **Project config**: `./.mcp.json`
- **Logs**: `~/.claude/logs/`

## Direct Config Example

`~/.claude/.claude.json`:
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/home/user/docs"],
      "env": {}
    }
  }
}
```

## Security Reminders

1. ⚠️ Only use trusted MCP servers
2. 🔒 Review permissions before granting
3. 🌐 Be cautious with internet-connected servers (prompt injection risk)
4. 🔑 Keep API keys secure with environment variables
5. 📝 Use read-only access where possible
6. 🚫 Never commit tokens to version control

## Troubleshooting

```bash
# Verify Claude Code installation
claude /doctor

# Check server status in Claude Code
/mcp

# Manual test of npx command
npx -y @modelcontextprotocol/server-NAME

# Check if server is in config
claude mcp get SERVERNAME

# Reset project server approvals
claude mcp reset-project-choices
```