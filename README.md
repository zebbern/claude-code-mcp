# MCP Server Setup Guide
> Install Model Context Protocol (MCP) servers to extend **Claude Code**.

![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code?label=Claude%20Code)

> [!NOTE]
> ### Prerequisites
> - **[Node.js 18+](https://nodejs.org/en/download/current)**
> - **Install the CLI:** `npm install -g @anthropic-ai/claude-code`

---

## 1) Install MCP servers (optional)
You can run all servers via `npx` (shown below). If you prefer global installs:

```bash
npm install -g @modelcontextprotocol/server-filesystem bash-mcp @playwright/mcp \
  better-qdrant-mcp-server @upstash/context7-mcp websearch-mcp
```

> [!TIP]
> Global installs are optional. The `claude mcp add ... -- npx -y <pkg>` commands work without global installs.

---

## 2) Add servers to Claude Code
The **`--` separator is required**. Everything after `--` is the server command that Claude will run.

```bash
# Filesystem — pick specific directories (avoid "/" for safety)
claude mcp add filesystem --scope user -- npx -y @modelcontextprotocol/server-filesystem \
  ~/Documents ~/Desktop ~/Projects

# Bash — runs shell commands (powerful; use on trusted projects)
claude mcp add bash-runner --scope user -- npx -y bash-mcp

# Playwright — control browsers / automate sites
claude mcp add playwright --scope user -- npx -y @playwright/mcp@latest

# WebSearch — requires a running crawler API (set your URL)
#   Example: https://crawler.example.com or http://localhost:3001
claude mcp add websearch --scope user \
  --env API_URL=https://YOUR-CRAWLER-URL \
  -- npx -y websearch-mcp

# Qdrant vector store — semantic search (set your endpoint & key if needed)
claude mcp add vectorstore --scope user \
  --env QDRANT_URL=http://localhost:6333 \
  # optional: --env QDRANT_API_KEY=YOUR_QDRANT_API_KEY \
  -- npx -y better-qdrant-mcp-server

# Context7 — live docs/context feed (API key recommended)
claude mcp add context7 --scope user -- npx -y @upstash/context7-mcp --api-key YOUR_CONTEXT7_API_KEY
```

> [!IMPORTANT]
> - **Filesystem:** avoid giving access to `/` (root). Grant only folders you intend to use.
> - **WebSearch:** make sure your crawler service is running and reachable at `API_URL`.
> - **Qdrant:** if your instance requires auth, set `QDRANT_API_KEY`. Configure embedding/model envs per your setup.
> - **Bash:** executes arbitrary shell commands—enable only when you trust the codebase.

---

## 3) Verify installation
```bash
claude mcp list
```
You should see each server with a ✓ **Connected** status once the server starts up correctly.

---

## Troubleshooting
- **Server not connecting?** Restart Claude Code, then run:
  ```bash
  claude mcp list
  claude mcp --help
  claude --help
  ```
- **Permission errors?**
  - Windows: run terminal as **Administrator**
  - macOS/Linux: prefix with `sudo` where appropriate
- **Remove a server:**
  ```bash
  claude mcp remove <name>
  ```

---

## Security notes
- Grant the filesystem server access only to directories you actually need.
- Treat the Bash server as you would a terminal on your machine.
- Prefer project-level servers when collaborating on untrusted code.
