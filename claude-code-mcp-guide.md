# Claude Code MCP Installation and Usage Guide

A comprehensive guide for installing and using Model Context Protocol (MCP) servers with Claude Code, suitable for both beginners and experienced users.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Understanding MCP](#understanding-mcp)
3. [Installing MCP Servers](#installing-mcp-servers)
4. [Server Scopes](#server-scopes)
5. [Using MCP Servers](#using-mcp-servers)
6. [Official MCP Servers](#official-mcp-servers)
7. [Troubleshooting](#troubleshooting)
8. [Best Practices](#best-practices)

## Prerequisites

Before you begin, ensure you have:

1. **Claude Code installed and working**
   - Run `claude /doctor` to verify installation
   - Accept the `--dangerously-skip-permissions` flag if prompted

2. **Node.js and npm/npx**
   - Required for many MCP servers
   - Verify with `node --version` and `npm --version`

3. **Python with uv/uvx (optional)**
   - Some MCP servers are Python-based
   - Install uv: Follow instructions at https://docs.astral.sh/uv/getting-started/installation/
   - Verify with `uvx --version`

## Understanding MCP

Model Context Protocol (MCP) is an open protocol that enables Claude Code to connect with external tools and data sources. Key concepts:

- **MCP Client**: Claude Code acts as the client
- **MCP Server**: Lightweight programs exposing specific capabilities
- **Transport Methods**: stdio (local) or SSE/HTTP (remote)
- **Capabilities**: Tools, Resources, and Prompts

## Installing MCP Servers

### Method 1: Basic Installation (stdio servers)

```bash
# Basic syntax
claude mcp add <n> <command> [args...]

# Example: Adding a filesystem server
claude mcp add filesystem npx -y @modelcontextprotocol/server-filesystem /path/to/allowed/files

# Example: Adding a GitHub server with environment variable
claude mcp add github npx -y @modelcontextprotocol/server-github -e GITHUB_TOKEN=ghp_yourtoken
```

### Method 2: SSE/HTTP Servers (Remote)

```bash
# Basic syntax for SSE servers
claude mcp add --transport sse <n> <url>

# Example: Adding an SSE server
claude mcp add --transport sse api-server https://api.example.com/mcp

# Example: With authentication headers
claude mcp add --transport sse github-server https://api.github.com/mcp --header "X-API-Key: your-key"
```

### Method 3: Environment Variables

```bash
# Adding a server with environment variables
claude mcp add postgres-server npx -y @modelcontextprotocol/server-postgres -e CONNECTION_STRING="postgresql://user:pass@localhost:5432/mydb"

# Multiple environment variables
claude mcp add my-server /path/to/server -e API_KEY=123 -e DEBUG=true -- arg1 arg2
```

### Method 4: JSON Configuration

```bash
# Add from JSON configuration
claude mcp add-json weather-api '{"type":"stdio","command":"/path/to/weather-cli","args":["--api-key","abc123"],"env":{"CACHE_DIR":"/tmp"}}'
```

### Method 5: Import from Claude Desktop

```bash
# Import servers already configured in Claude Desktop (macOS and WSL only)
claude mcp import-from-claude-desktop

# Import to user scope (available across all projects)
claude mcp import-from-claude-desktop -s user
```

## Server Scopes

MCP servers can be configured at three different scope levels:

### 1. Local Scope (Default)
- Available only to you in the current project
- Stored in project-specific user settings
- Takes highest precedence

```bash
claude mcp add local-server /path/to/server
# or explicitly:
claude mcp add local-server /path/to/server -s local
```

### 2. Project Scope
- Shared with team via `.mcp.json` file
- Check into version control
- Requires approval on first use

```bash
# Add a project-scoped server
claude mcp add shared-server /path/to/server -s project
```

Creates/updates `.mcp.json`:
```json
{
  "mcpServers": {
    "shared-server": {
      "command": "/path/to/server",
      "args": [],
      "env": {}
    }
  }
}
```

### 3. User Scope
- Available across all your projects
- Private to your user account

```bash
claude mcp add global-server /path/to/server -s user
```

## Using MCP Servers

### 1. Check Server Status
```bash
# Within Claude Code, use:
/mcp
```

This shows:
- Connected servers
- Authentication status
- Available tools/resources

### 2. Using MCP Tools
MCP prompts appear as slash commands:
```
/mcp__servername__promptname
```

Example:
```
/mcp__github__create_issue
```

### 3. Accessing Resources
Use the `@` symbol to access MCP resources:
```
@servername:resource
```

Example:
```
@github:issues
```

### 4. OAuth Authentication
For servers requiring OAuth 2.0 authentication:
```bash
# The server will prompt for OAuth when needed
claude mcp add --transport sse github-server https://api.github.com/mcp
```

### 5. Managing Servers
```bash
# List all configured servers
claude mcp list

# Get details for a specific server
claude mcp get my-server

# Remove a server
claude mcp remove my-server

# Reset project approval choices
claude mcp reset-project-choices
```

## Official MCP Servers

Here are the official MCP servers from the Model Context Protocol repository:

### 1. Filesystem Server
Secure file operations with configurable access controls.

```bash
claude mcp add filesystem npx -y @modelcontextprotocol/server-filesystem ~/Documents
```

### 2. GitHub Server
Repository management, file operations, and GitHub API integration.

```bash
claude mcp add github npx -y @modelcontextprotocol/server-github -e GITHUB_PERSONAL_ACCESS_TOKEN=ghp_yourtoken
```

### 3. PostgreSQL Server
Read-only database access with schema inspection.

```bash
claude mcp add postgres npx -y @modelcontextprotocol/server-postgres "postgresql://user:pass@localhost:5432/mydb"
```

### 4. Slack Server
Channel management and messaging capabilities.

```bash
claude mcp add slack npx -y @modelcontextprotocol/server-slack
```

### 5. Memory Server
Knowledge graph-based persistent memory system.

```bash
claude mcp add memory npx -y @modelcontextprotocol/server-memory
```

### 6. Git Server (Python)
Tools to read, search, and manipulate Git repositories.

```bash
# Using uvx (recommended)
claude mcp add git uvx mcp-server-git --repository /path/to/git/repo

# Using pip
pip install mcp-server-git
claude mcp add git python -m mcp_server_git --repository /path/to/git/repo
```

### 7. Google Drive Server
File access and search capabilities for Google Drive.

```bash
claude mcp add gdrive npx -y @modelcontextprotocol/server-gdrive
```

### 8. Brave Search Server
Web and local search using Brave's Search API.

```bash
claude mcp add brave-search npx -y @modelcontextprotocol/server-brave-search -e BRAVE_API_KEY=your-key
```

### 9. Puppeteer Server
Browser automation and web scraping.

```bash
claude mcp add puppeteer npx -y @modelcontextprotocol/server-puppeteer
```

### 10. Sequential Thinking Server
Dynamic and reflective problem-solving through thought sequences.

```bash
claude mcp add sequential-thinking npx -y @modelcontextprotocol/server-sequentialthinking
```

## Troubleshooting

### Common Issues

1. **"Command not found" errors**
   - Ensure npx is in your PATH
   - For Python servers, ensure uvx or pip is installed
   - Try using full paths to executables

2. **Connection timeouts**
   - Set custom timeout: `MCP_TIMEOUT=10000 claude`
   - Default is 5 seconds

3. **Permission issues**
   - Run `claude /doctor` and accept permissions
   - For project servers: `claude mcp reset-project-choices`

4. **Server not showing in /mcp**
   - Restart Claude Code
   - Check server logs

5. **OAuth authentication failures**
   - Use `/mcp` to check authentication status
   - Server will prompt for re-authentication if needed

### Viewing Logs
```bash
# List recent logs
ls -la ~/.claude/logs/

# Follow logs in real-time
tail -f ~/.claude/logs/mcp-server-*.log

# View specific server log
tail -f ~/.claude/logs/mcp-server-SERVERNAME.log
```

### Direct Configuration Editing

For complex setups or when the CLI has issues, you can edit the configuration file directly:

**Location**: `~/.claude/.claude.json` (Linux/WSL)

Example configuration:
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/home/user/Documents"],
      "env": {}
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_yourtoken"
      }
    }
  }
}
```

## Best Practices

### 1. Security
- **Only use trusted MCP servers** - third-party servers can access your data
- Be especially cautious with servers that access the internet (prompt injection risk)
- Review permissions before granting access
- Use read-only access where possible
- Never commit API keys or tokens to version control

### 2. Configuration Management
- Use project scope for team-shared servers
- Keep sensitive credentials in environment variables
- Document server purposes in your README
- Use `.env` files for local development (not committed)

### 3. Performance
- Start with minimal server set
- Monitor resource usage via logs
- Disable unused servers with `claude mcp remove`
- Set appropriate timeouts for slow servers

### 4. Team Collaboration
For team environments:

1. Create `.mcp.json` for shared servers:
```bash
claude mcp add team-db npx -y @modelcontextprotocol/server-postgres -s project
```

2. Use environment variables for secrets:
```json
{
  "mcpServers": {
    "team-db": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "CONNECTION_STRING": "${DATABASE_URL}"
      }
    }
  }
}
```

3. Add to version control:
```bash
git add .mcp.json
git commit -m "Add shared MCP servers"
```

4. Team members approve on first use

### 5. Debugging

When servers fail to connect:

1. Check the specific server log
2. Verify command syntax with manual execution
3. Ensure all dependencies are installed
4. Check environment variables are set correctly
5. Try increasing timeout if server is slow to start

## Additional Resources

- [Official MCP Documentation](https://modelcontextprotocol.io/introduction)
- [MCP Specification](https://spec.modelcontextprotocol.io)
- [Official MCP Servers Repository](https://github.com/modelcontextprotocol/servers)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code/mcp)
- [MCP SDK Documentation](https://github.com/modelcontextprotocol/typescript-sdk)

## Notes

- This guide is based on official Anthropic documentation and the Model Context Protocol repository
- MCP is actively evolving - check official docs for latest updates
- When in doubt, refer to the server's specific documentation in the official repository
- Always verify server authenticity before connecting, especially for third-party servers