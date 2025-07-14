# Practical MCP Workflow Example

## Scenario: Setting Up a Development Environment

This example demonstrates setting up MCP servers for a typical development workflow with GitHub, PostgreSQL, and filesystem access.

### Step 1: Initial Setup

First, verify Claude Code is working:
```bash
claude /doctor
```

If prompted, accept the `--dangerously-skip-permissions` flag.

### Step 2: Install Essential MCP Servers

#### A. Filesystem Server (for code access)
```bash
# Grant access to your projects directory
claude mcp add filesystem npx -y @modelcontextprotocol/server-filesystem ~/projects
```

#### B. GitHub Server (for repository management)
```bash
# First, create a GitHub token at https://github.com/settings/tokens
# Grant necessary permissions (repo, read:org, etc.)
# Then add the server:
claude mcp add github npx -y @modelcontextprotocol/server-github \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=ghp_yourtoken
```

#### C. PostgreSQL Server (for database queries)
```bash
# Add your development database (read-only access)
claude mcp add devdb npx -y @modelcontextprotocol/server-postgres \
  "postgresql://devuser:devpass@localhost:5432/myapp_dev"
```

### Step 3: Verify Installation

In Claude Code, check all servers are connected:
```
/mcp
```

Expected output:
```
⎿ MCP Server Status ⎿
⎿ • filesystem: connected ⎿
⎿ • github: connected ⎿  
⎿ • devdb: connected ⎿
```

### Step 4: Using the Servers

#### Example 1: Analyze Project Structure
```
Can you analyze the structure of the project at ~/projects/my-app and summarize what it does?
```
Claude will use the filesystem server to read and analyze your project.

#### Example 2: Check GitHub Issues
```
What are the open issues in my repository username/my-app?
```
Claude will use the GitHub server to fetch and summarize issues.

#### Example 3: Database Schema Analysis
```
Can you describe the database schema and list all tables with their relationships?
```
Claude will use the PostgreSQL server to inspect your database.

#### Example 4: Combined Workflow
```
I need to implement the feature described in GitHub issue #42. Can you:
1. Read the issue details
2. Check the current code implementation 
3. Query the database to understand the data model
4. Suggest an implementation approach
```

### Step 5: Team Collaboration Setup

To share these servers with your team:

1. Convert to project scope:
```bash
# Remove local servers first
claude mcp remove filesystem
claude mcp remove github
claude mcp remove devdb

# Re-add as project-scoped
claude mcp add filesystem npx -y @modelcontextprotocol/server-filesystem ~/projects -s project
claude mcp add github npx -y @modelcontextprotocol/server-github -s project
claude mcp add devdb npx -y @modelcontextprotocol/server-postgres -s project
```

2. This creates `.mcp.json`:
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "~/projects"],
      "env": {}
    },
    "github": {
      "command": "npx", 
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {}
    },
    "devdb": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {}
    }
  }
}
```

3. Create `.env.example` for team:
```bash
# .env.example
GITHUB_PERSONAL_ACCESS_TOKEN=ghp_yourtoken
DATABASE_URL=postgresql://user:pass@localhost:5432/db
```

4. Update `.mcp.json` to use environment variables:
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_PERSONAL_ACCESS_TOKEN}"
      }
    },
    "devdb": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "${DATABASE_URL}"]
    }
  }
}
```

5. Commit to version control:
```bash
git add .mcp.json .env.example
git commit -m "Add MCP server configuration for team"
```

6. Add to `.gitignore`:
```bash
echo ".env" >> .gitignore
```

### Step 6: Advanced Usage

#### Using Multiple Servers Together
```
Based on the error logs in ~/projects/my-app/logs/error.log, find related GitHub issues and check if any database migrations might fix the problem.
```

#### Automated Workflows
```
Every time I say "status update", I want you to:
1. Check my GitHub notifications
2. List today's commits in my repositories  
3. Show any new errors from the application logs
4. Query the database for today's user signups
```

### Step 7: Adding More Servers

As your needs grow, add more servers:

#### Memory Server (for persistent context)
```bash
claude mcp add memory npx -y @modelcontextprotocol/server-memory -s user
```

#### Git Server (for detailed repo analysis)
```bash
# Using Python's uvx
claude mcp add git uvx mcp-server-git --repository ~/projects/my-app
```

#### Brave Search (for web searches)
```bash
# Get API key from https://api.search.brave.com/
claude mcp add search npx -y @modelcontextprotocol/server-brave-search \
  -e BRAVE_API_KEY=your-key
```

### Troubleshooting Tips

1. **Server not responding**: Check logs
   ```bash
   tail -f ~/.claude/logs/mcp-server-*.log
   ```

2. **Permission denied**: Re-run with proper scope
   ```bash
   claude mcp remove servername
   claude mcp add servername ... -s user
   ```

3. **Team member can't use servers**: Have them approve
   ```bash
   # They should run:
   claude mcp reset-project-choices
   # Then restart Claude Code
   ```

4. **Environment variables not working**: Check they're exported
   ```bash
   export GITHUB_PERSONAL_ACCESS_TOKEN=ghp_yourtoken
   claude
   ```

### Best Practices Demonstrated

1. **Start small**: Add one server at a time and test
2. **Verify each server**: Use `/mcp` after each addition
3. **Use meaningful names**: `devdb` vs just `postgres`
4. **Document for team**: Include setup in README
5. **Secure credentials**: Never commit tokens, use environment variables
6. **Appropriate access**: Filesystem only to needed directories
7. **Scope appropriately**: User scope for personal tools, project for team

### Example README.md Section

```markdown
## MCP Setup for Development

This project uses MCP servers for enhanced AI assistance. To set up:

1. Copy `.env.example` to `.env` and fill in your credentials
2. Run Claude Code in this directory
3. When prompted, approve the project MCP servers

Available servers:
- `filesystem`: Access to project files
- `github`: GitHub integration (issues, PRs)  
- `devdb`: Read-only database access

For issues, check logs at `~/.claude/logs/`
```

### Next Steps

1. Explore more official servers at https://github.com/modelcontextprotocol/servers
2. Consider building custom MCP servers for your specific needs
3. Join the MCP community for tips and new server announcements
4. Keep servers updated with latest versions for bug fixes and features