# MCP Server Setup Guide
> Install Model Context Protocol (MCP) servers to extend **Claude Code**.

![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code?label=Claude%20Code)

## Table of Contents
- [Prerequisites](#prerequisites)
- [Understanding MCP](#understanding-mcp)
- [Installing MCP Servers](#installing-mcp-servers)
- [Server Scopes](#server-scopes)
- [Using MCP Servers](#using-mcp-servers)
- [Official MCP Servers](#official-mcp-servers)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)

---

## Prerequisites
- **Node.js 18+** verify with:
  ```bash
  node -v
  ```
- **Claude Code CLI** — install with:
  ```bash
  npm install -g @anthropic-ai/claude-code
  ```

---

## Understanding MCP
**Model Context Protocol (MCP)** lets tools run as separate _servers_ that Claude connects to at runtime. Each server exposes one or more capabilities (e.g., filesystem access, running shell commands, browser automation). You register a server with Claude, and Claude starts it with your specified command when needed.

Key ideas:
- **Server**: a process Claude launches (e.g., `npx -y @modelcontextprotocol/server-filesystem`).
- **Transport**: how Claude talks to the server (stdio by default).
- **Scope**: where the server registration is stored (user-wide or per-project).

---

## Installing MCP Servers
> You can use `npx` (no global install required). If you prefer global installs:

```bash
npm install -g @modelcontextprotocol/server-filesystem bash-mcp @playwright/mcp \
  better-qdrant-mcp-server @upstash/context7-mcp websearch-mcp
```

Register servers with **`claude mcp add`**. The `--` **separator is required** everything after it is the command Claude will run.

```bash
# Filesystem — grant access to specific folders (avoid "/")
claude mcp add filesystem --scope user -- npx -y @modelcontextprotocol/server-filesystem \
  ~/Documents ~/Desktop ~/Projects

# Bash — executes shell commands (enable only on trusted projects)
claude mcp add bash-runner --scope user -- npx -y bash-mcp

# Playwright — control browsers / automate sites
claude mcp add playwright --scope user -- npx -y @playwright/mcp@latest

# WebSearch — requires a running crawler API at API_URL
claude mcp add websearch --scope user \
  --env API_URL=https://YOUR-CRAWLER-URL \
  -- npx -y websearch-mcp

# Qdrant vector store — semantic search (set endpoint & key if required)
claude mcp add vectorstore --scope user \
  --env QDRANT_URL=http://localhost:6333 \
  # optional: --env QDRANT_API_KEY=YOUR_QDRANT_API_KEY \
  -- npx -y better-qdrant-mcp-server

# Context7 — live documentation / context stream (API key recommended)
claude mcp add context7 --scope user -- npx -y @upstash/context7-mcp --api-key YOUR_CONTEXT7_API_KEY
```

---

## Server Scopes
- **User scope** (`--scope user`): available in all projects on this machine/account.
- **Project scope** (omit `--scope`): stored locally for the current project/directory only.
- You can **remove** a server later:
  ```bash
  claude mcp remove <name>
  ```

---

## Using MCP Servers
Check status and details:
```bash
claude mcp list
claude mcp info <name>
```

Typical usage patterns in Claude:
- **Filesystem**: “Open `~/Projects/app/config.json` and show me the contents.”
- **Bash**: “Run `npm test` and return the output.”
- **Playwright**: “Visit `https://example.com`, click ‘Login’, and take a screenshot.”
- **Vectorstore (Qdrant)**: “Embed and upsert these docs, then search for similar passages.”
- **WebSearch**: “Search for recent articles on WebGPU and summarize the top three.”
- **Context7**: “Stream the latest docs for package `xyz` into this workspace.”

---

## Official MCP Servers
Packages maintained under the **`@modelcontextprotocol`** scope are considered official. Common ones include:
- `@modelcontextprotocol/server-filesystem` — Read/write specific directories you allow.

> Other servers in this guide (e.g., `bash-mcp`, `@playwright/mcp`, `better-qdrant-mcp-server`, `@upstash/context7-mcp`, `websearch-mcp`) are community or vendor-maintained and widely used, but not under the `@modelcontextprotocol` org.

---

## Troubleshooting
- **Server shows “Not Connected”**
  ```bash
  # Restart and recheck
  claude mcp list
  claude mcp --help
  claude --help
  ```
- **Permissions / Access denied**
  - macOS/Linux: try prefixing with `sudo` where appropriate.
  - Windows: run terminal as **Administrator**.
- **WebSearch won’t connect**
  - Ensure your crawler service is running and reachable at `API_URL`.
- **Qdrant errors**
  - Verify `QDRANT_URL` and any required `QDRANT_API_KEY`.
- **Playwright prompts during setup**
  - Use `@latest` and `-y` in the add command to auto-accept prompts.

---

## Best Practices
- **Least privilege**: Grant the filesystem server only the folders you need—avoid `/`.
- **Be cautious with Bash**: Treat it like a terminal; enable only for trusted codebases.
- **Pin versions when collaborating**: e.g., `@playwright/mcp@<version>` for deterministic setups.
- **Use project scope for untrusted repos**: Keep powerful servers out of global scope if unsure.
- **Document env vars**: Check them into `.env.example` (never real secrets).

---

### Quick Verify
```bash
claude mcp list
```
You should see each configured server with a ✓ **Connected** status once it starts successfully.
