<img align="right" src="https://img.shields.io/npm/v/@anthropic-ai/claude-code?label=Claude%20Code"/>

# MCP Server Setup 
> **Model Context Protocol (MCP)** lets tools run as separate _servers_ that Claude connects to at runtime. Each server exposes one or more capabilities (e.g., filesystem access, running shell commands, browser automation). You register a server with Claude, and Claude starts it with your specified command when needed.

---

> [!Important]
> **Install Node.js 18+** ⮞ <kbd>node -v</kbd><br>
> > <img width="209" height="47" alt="image" src="https://github.com/user-attachments/assets/44107d4b-c92b-49e3-a721-8ec8d0c5b854" />
>  
> **Install Claude Code** ⮞ <kbd>npm install -g @anthropic-ai/claude-code</kbd><br>
> > <img width="505" height="120" alt="image" src="https://github.com/user-attachments/assets/97b930d0-1a1e-48d1-8c03-3d2f564f8137" />

> ### Official Docs You May Want:
> 
> > **[Build MCP Server](https://modelcontextprotocol.io/quickstart/server) | [Build MCP Client](https://modelcontextprotocol.io/quickstart/client) | [Server Examples](https://github.com/modelcontextprotocol/servers) | [Popular MCP servers](https://docs.anthropic.com/en/docs/claude-code/mcp)**


> ### Community Docs You May Want:
> 
> > Adding soon..

<table><td>
  
## Quick Start
> **If you're in a hurry, here's the fastest way to add:**

```bash
# Add file system access (most commonly used)
claude mcp add filesystem -s user -- npx -y @modelcontextprotocol/server-filesystem ~/Documents ~/Desktop

# Verify if successful
claude mcp list
```
> **Responce if it worked like it should:**
<img width="868" height="192" alt="image" src="https://github.com/user-attachments/assets/8e7b23c7-ccfb-49aa-9203-e37f07c2514e" />
</td></table>

## Additional Methods:

<table><td>
  
### 1. Command Line Addition 
> **Claude Code provides simple command line tools to add MCP servers:**

```bash
# Basic syntax
claude mcp add <name> <command> [parameters...]

# Actual example: Add local file system access
claude mcp add my-filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents

# Example with environment variables
claude mcp add api-server -e API_KEY=your-key-here -- /path/to/server
```

</td></table>

<table><td>

### 2. Direct Configuration File Editing 
> Many developers find CLI wizards too cumbersome, especially when you have to restart if you make a mistake.
> 
> Direct configuration file editing is more efficient:

**1. Find configuration file location:**
- macOS/Linux: `~/.claude.json`
- Windows: `%USERPROFILE%\.claude.json`

**2. Edit configuration file:**

```json
{
  "mcpServers": {
    "filesystem": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/username/Documents"],
      "env": {}
    },
    "github": {
      "type": "stdio", 
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}
```
**3. Restart Claude Code to take effect**

</td></table>
<table><td>

### 3. Project-level Configuration (Recommended for team collaboration)
> If you want team members to all use the same MCP configuration:

```bash
# Add project-level MCP server
claude mcp add shared-tools -s project -- npx -y @your-team/mcp-tools
```

**This will create a `.mcp.json` file in the project root directory:**

```json
{
  "mcpServers": {
    "shared-tools": {
      "command": "npx",
      "args": ["-y", "@your-team/mcp-tools"],
      "env": {}
    }
  }
}
```

</td></table>

## MCP Server Scope Detailed

Understanding scope is crucial to avoid "server not found" errors:

### 1. Local Scope (Default)
- Only available in current directory
- Configuration stored in the projects section of `~/.claude.json`
- Suitable for: Personal project-specific tools

### 2. User Scope (Global)
- Available in all projects
- Added using `-s user` flag
- Suitable for: Common tools like file systems, database clients

### 3. Project Scope (Team shared)
- Shared through `.mcp.json` file
- Added using `-s project` flag
- Suitable for: Team-shared project-specific tools

## Practical MCP Server Recommendations
> **Here's the most worthwhile MCP server list to install:**

### 1. File System Access
```bash
claude mcp add filesystem -s user -- npx -y @modelcontextprotocol/server-filesystem ~/Documents ~/Projects ~/Desktop
```
Use: Let Claude directly read and write files, modify code

### 2. GitHub Integration
```bash
claude mcp add github -s user -e GITHUB_TOKEN=your-token -- npx -y @modelcontextprotocol/server-github
```
Use: Manage issues, PRs, code reviews

### 3. Web Browser Control
```bash
claude mcp add puppeteer -s user -- npx -y @modelcontextprotocol/server-puppeteer
```
Use: Automated web operations, crawling, testing

### 4. Database Connection (PostgreSQL)
```bash
claude mcp add postgres -s user -e DATABASE_URL=your-db-url -- npx -y @modelcontextprotocol/server-postgres
```
Use: Directly query and manipulate databases

### 5. Fetch Tool (API Calls)
```bash
claude mcp add fetch -s user -- npx -y @kazuph/mcp-fetch
```
Use: Call various REST APIs

### 6. Search Engine
```bash
claude mcp add search -s user -e BRAVE_API_KEY=your-key -- npx -y @modelcontextprotocol/server-brave-search
```
Use: Search for latest information

### 7. Slack Integration
```bash
claude mcp add slack -s user -e SLACK_TOKEN=your-token -- npx -y @modelcontextprotocol/server-slack
```
Use: Send messages, manage channels

### 8. Time Management
```bash
claude mcp add time -s user -- npx -y @modelcontextprotocol/server-time
```
Use: Time zone conversion, date calculation

### 9. Memory Storage
```bash
claude mcp add memory -s user -- npx -y @modelcontextprotocol/server-memory
```
Use: Save information across conversations

### 10. Sequential Thinking (Thought Chain)
```bash
claude mcp add thinking -s user -- npx -y @modelcontextprotocol/server-sequential-thinking
```
Use: Step-by-step thinking for complex problems

## Common Errors and Solutions

### Error 1: Tool Name Validation Failed
```
API Error 400: "tools.11.custom.name: String should match pattern '^[a-zA-Z0-9_-]{1,64}$'"
```

**Solution**:
- Ensure server name only contains letters, numbers, underscores and hyphens
- Name length should not exceed 64 characters
- Don't use special characters or spaces

### Error 2: MCP Server Not Found
```
MCP server 'my-server' not found
```

**Solution**:
1. Check if scope settings are correct
2. Run `claude mcp list` to confirm server has been added
3. Ensure you're in the correct directory (for local scope)
4. Restart Claude Code

### Error 3: Protocol Version Error
```
"protocolVersion": "Required"
```

**Solution**: This is a known bug in Claude Code, temporary solutions:
1. Use wrapper scripts
2. Ensure MCP server returns correct protocol version
3. Update to latest version of Claude Code

### Error 4: Windows Path Issues
```
Error: Cannot find module 'C:UsersusernameDocuments'
```

**Solution**: Windows paths need to use forward slashes or double backslashes:

```bash
# Wrong
claude mcp add fs -- npx -y @modelcontextprotocol/server-filesystem C:\Users\username\Documents

# Correct
claude mcp add fs -- npx -y @modelcontextprotocol/server-filesystem C:/Users/username/Documents
# or
claude mcp add fs -- npx -y @modelcontextprotocol/server-filesystem C:\\Users\\username\\Documents
```

### Error 5: Permission Issues
```
Permission denied
```

**Solution**:
1. macOS/Linux: Use `sudo` (not recommended) or modify file permissions
2. Windows: Run as administrator
3. Best method: Install MCP servers in user directory

## Debugging Techniques

When encountering problems, these debugging methods can help you quickly locate issues:

### 1. Enable Debug Mode
```bash
claude --mcp-debug
```

### 2. View MCP Status
In Claude Code, enter:
```
/mcp
```

### 3. View Log Files

**macOS/Linux:**
```bash
tail -f ~/Library/Logs/Claude/mcp*.log
```

**Windows:**
```cmd
type "%APPDATA%\Claude\logs\mcp*.log"
```

### 4. Manually Test Server
```bash
# Directly run server command to see if there's output
npx -y @modelcontextprotocol/server-filesystem ~/Documents
```

## Special Notes for International Users

### 1. Non-English Path Issues
Avoid using non-English characters in paths:

```bash
# Avoid
claude mcp add fs -- npx -y @modelcontextprotocol/server-filesystem ~/文档

# Recommended
claude mcp add fs -- npx -y @modelcontextprotocol/server-filesystem ~/Documents
```

### 2. Proxy Configuration
If you're using a proxy:

```bash
# Set npm proxy
npm config set proxy http://your-proxy:port
npm config set https-proxy http://your-proxy:port

# Then add MCP server
claude mcp add ...
```

### 3. Mirror Sources
Use mirror sources to accelerate downloads:

```bash
# Temporary use
claude mcp add fs -- npx -y --registry=https://registry.npmjs.org @modelcontextprotocol/server-filesystem ~/Documents

# Or permanent setting
npm config set registry https://registry.npmjs.org
```

## Best Practice Recommendations

1. **Add as needed**: Don't add too many MCP servers at once, it will affect performance
2. **Regular cleanup**: Use `claude mcp remove <name>` to delete unused servers
3. **Security first**: Only add trusted MCP servers, especially those requiring network access
4. **Backup configuration**: Regularly backup `~/.claude.json` file
5. **Team collaboration**: Use project scope to share common configurations

## Advanced Techniques

### 1. Create Custom MCP Server

If existing MCP servers can't meet your needs, you can create your own:

```javascript
// my-mcp-server.js
import { Server } from '@modelcontextprotocol/sdk';

const server = new Server({
  name: 'my-custom-server',
  version: '1.0.0',
});

server.setRequestHandler('tools/list', async () => {
  return {
    tools: [{
      name: 'my_custom_tool',
      description: 'Custom tool',
      inputSchema: {
        type: 'object',
        properties: {
          input: { type: 'string' }
        }
      }
    }]
  };
});

server.start();
```

### 2. Batch Configuration Script

Create a script to configure all common MCP servers at once:

```bash
#!/bin/bash
# setup-mcp.sh

echo "Configuring common MCP servers..."

# File system
claude mcp add filesystem -s user -- npx -y @modelcontextprotocol/server-filesystem ~/Documents ~/Projects

# GitHub
read -p "Enter GitHub Token: " github_token
claude mcp add github -s user -e GITHUB_TOKEN=$github_token -- npx -y @modelcontextprotocol/server-github

# Other servers...

echo "MCP servers configured successfully!"
```


