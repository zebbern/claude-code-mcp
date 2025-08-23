
# MCP Server Setup Guide
> This will help you install MCP (Model Context Protocol) servers to extend Claude Code's capabilities.

![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code?label=Claude%20Code)


### Prerequisites
- Node.js 18+ installed
- Claude Code installed
- Terminal/Command Prompt access

### 1. Install MCP Servers

Copy and paste these commands one by one:

```bash
# Install all MCP servers
npm install -g websearch-mcp
npm install -g @modelcontextprotocol/server-filesystem
npm install -g bash-mcp
npm install -g @playwright/mcp
npm install -g better-qdrant-mcp-server
npm install -g @upstash/context7-mcp
```

### 2. Add Servers to Claude Code

Run these commands to configure each server:

```bash
# Add each MCP server 
claude mcp add websearch npx websearch-mcp                                # Search the internet as Get current news, research topics 
claude mcp add filesystem npx @modelcontextprotocol/server-filesystem /   # Access files/folders / Read, write, organize files
claude mcp add bash-runner npx bash-mcp                                   # Run shell commands / Execute scripts, system operations
claude mcp add playwright npx @playwright/mcp                             # Control web browsers / Automate websites, scraping
claude mcp add vectorstore npx better-qdrant-mcp-server                   # Semantic search / Find similar content, embeddings
claude mcp add context7 npx @upstash/context7-mcp                         # Live documentation / `use context7` for updated docs
```
> [!Note]
> ### Verify Installation
> 
> *Check that all servers are working:*
> 
> ```bash
> claude mcp list
> ```
> 
> *You should see all servers with ✓ Connected status.*
> 
> ### Server not connecting?
> **Restart Claude Code and try again**
> ```bash
> claude mcp list
> claude mcp --help
> claude --help
> ```
> 
> **Permission errors?**
> - Run terminal as administrator (Windows)
> - Use `sudo` prefix (macOS/Linux)

