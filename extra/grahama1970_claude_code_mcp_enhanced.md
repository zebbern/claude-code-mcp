
# `grahama1970/claude-code-mcp-enhanced`: Enhanced Claude Code MCP Server

`grahama1970/claude-code-mcp-enhanced` is an enhanced Model Context Protocol (MCP) server that extends the capabilities of Claude Code, particularly focusing on orchestration, reliability, and self-contained execution patterns. It builds upon `steipete/claude-code-mcp` by adding robust error handling, task automation, and improved developer experience.

## Key Features

*   **Enhanced Reliability**: Includes robust error handling, automatic retries, graceful shutdown mechanisms, and request tracking to ensure more stable and consistent execution of Claude Code tasks.
*   **Task Orchestration**: Designed to break down complex workflows into specialized subtasks, allowing for more structured and manageable agentic operations.
*   **Task Automation**: Can convert human-readable Markdown task lists into executable MCP commands automatically, streamlining the process of defining and running multi-step tasks.
*   **Performance Optimization**: Features like configuration caching and resource efficiency contribute to improved execution speed.
*   **Better Monitoring**: Provides a health check API, detailed error reporting, and comprehensive logging for easier debugging and oversight.
*   **Developer Experience**: Offers hot reloading of configuration, flexible environment controls, and a simplified API for a more user-friendly development process.
*   **Direct Claude Code Interaction**: Allows LLMs to run Claude Code with all permissions bypassed (using `--dangerously-skip-permissions`) and execute any prompt without permission interruptions.
*   **File Editing and Git Operations**: Facilitates direct file editing capabilities and integration with Git for version control.

## Installation and Usage

This MCP server can be installed and used in several ways:

### 1. Install from GitHub (Recommended for Latest Version)

Add the following to your `.mcp.json` file:

```json
{
  "mcpServers": {
    "claude-code-mcp-enhanced": {
      "command": "npx",
      "args": [
        "github:grahama1970/claude-code-mcp-enhanced"
      ],
      "env": {
        "MCP_CLAUDE_DEBUG": "false",
        "MCP_HEARTBEAT_INTERVAL_MS": "15000",
        "MCP_EXECUTION_TIMEOUT_MS": "1800000"
      }
    }
  }
}
```

### 2. Install from npm (if published)

If the package is published to npm, you can install it using the npm package name:

```json
{
  "mcpServers": {
    "claude-code-mcp-enhanced": {
      "command": "npx",
      "args": [
        "-y",
        "@grahama1970/claude-code-mcp-enhanced@latest"
      ],
      "env": {
        "MCP_CLAUDE_DEBUG": "false",
        "MCP_HEARTBEAT_INTERVAL_MS": "15000",
        "MCP_EXECUTION_TIMEOUT_MS": "1800000"
      }
    }
  }
}
```

### 3. Run from Local Installation (for Development/Testing)

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/grahama1970/claude-code-mcp-enhanced.git
    cd claude-code-mcp-enhanced
    ```
2.  **Install dependencies and build**:
    ```bash
    npm install
    npm run build
    ```
3.  **Configure your `.mcp.json`** to use the local server:
    ```json
    {
      "mcpServers": {
        "claude-code-mcp-enhanced": {
          "command": "node",
          "args": [
            "/path/to/claude-code-mcp-enhanced/dist/server.js"
          ],
          "env": {
            "MCP_CLAUDE_DEBUG": "false",
            "MCP_HEARTBEAT_INTERVAL_MS": "15000",
            "MCP_EXECUTION_TIMEOUT_MS": "1800000"
          }
        }
      }
    }
    ```

### Prerequisites

*   **Node.js v20 or later**
*   **Claude CLI**: Must be installed locally (`npm install -g @anthropic-ai/claude-code`) and run manually once with `--dangerously-skip-permissions` to accept terms and allow non-interactive use by the MCP server.

### Client Configuration

After setting up the server, configure your MCP client (e.g., Cursor, Claude Desktop, Windsurf) by adding the server configuration to its `mcp.json` or `mcp_config.json` file. Common locations include:

*   **Cursor**: `~/.cursor/mcp.json` (macOS), `%APPDATA%\Cursor\mcp.json` (Windows), `~/.config/cursor/mcp.json` (Linux)
*   **Windsurf**: `~/.codeium/windsurf/mcp_config.json` (macOS), `%APPDATA%\Codeium\windsurf\mcp_config.json` (Windows), `~/.config/.codeium/windsurf/mcp_config.json` (Linux)

## Primary Tools Exposed

This server exposes a `claude_code` tool, which executes prompts directly using the Claude Code CLI with permissions bypassed.

**Arguments for `claude_code` tool**:

*   `prompt` (string, required): The prompt to send to Claude Code.
*   `workFolder` (string, optional): The working directory for the Claude CLI execution.
*   `parentTaskId` (string, optional): ID of the parent task for orchestration.
*   `returnMode` (string, optional): How results should be returned (`'summary'` or `'full'`). Defaults to `'full'`.
*   `taskDescription` (string, optional): Short description of the task.
*   `mode` (string, optional): Specifies the Roo mode to use when `MCP_USE_ROOMODES=true` (e.g., `'boomerang-mode'`, `'coder'`, `'designer'`).

## Best Practices

*   **Initial Setup**: Ensure the one-time `claude --dangerously-skip-permissions` setup is completed to avoid permission interruptions.
*   **Task Decomposition**: Leverage the orchestration capabilities by breaking down complex problems into smaller, manageable tasks that can be delegated to Claude via this MCP.
*   **Monitoring**: Utilize the health check API and detailed logging for effective monitoring and debugging of agentic workflows.

## Source

[https://github.com/grahama1970/claude-code-mcp-enhanced](https://github.com/grahama1970/claude-code-mcp-enhanced)


