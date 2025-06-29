
# MCP Server Configuration

This document provides detailed instructions on how to configure Model Context Protocol (MCP) servers with Claude Code, covering different server types, scope levels, and authentication methods.

## Understanding MCP Server Types

Claude Code supports various MCP server types, enabling flexible integration with external tools and data sources:

*   **Stdio Server**: A fundamental server type that communicates via standard input/output streams. This is often used for simple, local integrations.
*   **SSE (Server-Sent Events) Server**: Designed for real-time, one-way communication from the server to the client. Ideal for continuous data streams or event-driven updates.
*   **HTTP Server**: A standard web-based server that communicates over HTTP/HTTPS. This is commonly used for integrating with web APIs and services.

## Adding MCP Servers

To add an MCP server to Claude Code, use the `claude mcp add` command. The basic syntax is as follows:

```bash
claude mcp add <name> <command> [args...]
```

*   `<name>`: A unique identifier for your MCP server (e.g., `my-filesystem`, `github-api`).
*   `<command>`: The executable command that starts your MCP server (e.g., `npx @modelcontextprotocol/server-filesystem`, `python my_custom_server.py`).
*   `[args...]`: Optional arguments to pass to your MCP server command.

### Examples of Adding Servers:

#### 1. Adding a Local Stdio Server

This example demonstrates adding a local server that might perform file operations. You can also pass environment variables using the `-e` or `--env` flag.

```bash
claude mcp add my-local-server -e API_KEY=your_secret_key -- /path/to/your/local_mcp_server_executable arg1 arg2
```

#### 2. Adding an SSE Server

For servers that communicate using Server-Sent Events, specify the `--transport sse` flag and the server's URL.

```bash
claude mcp add --transport sse my-sse-server https://api.example.com/events
```

#### 3. Adding an HTTP Server

For standard HTTP/HTTPS based servers, use the `--transport http` flag and the server's endpoint URL.

```bash
claude mcp add --transport http my-http-server https://api.example.com/data
```

## Managing MCP Servers

Claude Code provides several commands to manage your configured MCP servers:

*   **List all configured servers**: To see a list of all MCP servers you have added, along with their names and types:
    ```bash
    claude mcp list
    ```
*   **Remove a server**: To remove a previously added MCP server:
    ```bash
    claude mcp remove <server-name>
    ```
*   **Check server status within Claude Code**: While interacting with Claude Code, you can use the `/mcp` command to view the connection status of all configured servers, authenticate with remote servers, and view server capabilities.

## MCP Server Scope Levels

MCP server configurations can be set at three distinct scope levels, each serving different purposes for accessibility and sharing. Understanding these scopes is crucial for effective management of your MCP integrations.

### 1. Local Scope (Default)

*   **Description**: This is the default configuration level. Servers configured with local scope are stored in your project-specific user settings.
*   **Accessibility**: They remain private to you and are only accessible when working within the current project directory.
*   **Use Case**: Ideal for personal development servers, experimental configurations, or servers containing sensitive credentials that should not be shared with others.

### 2. Project Scope

*   **Description**: Project-scoped servers facilitate team collaboration. Their configurations are stored in a `.mcp.json` file located at your project’s root directory.
*   **Accessibility**: This `.mcp.json` file is designed to be checked into version control (e.g., Git), ensuring that all team members have access to the same MCP tools and services.
*   **Use Case**: When you add a project-scoped server, Claude Code automatically creates or updates this file with the appropriate configuration structure. For security, Claude Code prompts for approval before using project-scoped servers from `.mcp.json` files. You can reset these approvals using `claude mcp reset-project-choices`.

### 3. User Scope

*   **Description**: User-scoped servers provide cross-project accessibility. They are available across all projects on your machine but remain private to your user account.
*   **Accessibility**: These configurations are stored in your user-specific Claude Code settings.
*   **Use Case**: Works well for personal utility servers, development tools, or services you frequently use across different projects, without needing to configure them for each new project.

### Setting Scope:

To specify the scope when adding a server, use the `-s` or `--scope` flag:

*   For local scope (default, often omitted): `claude mcp add -s local my-server ...`
*   For project scope: `claude mcp add -s project my-team-server ...`
*   For user scope: `claude mcp add -s user my-global-server ...`

## Authentication with Remote MCP Servers

Many remote MCP servers require authentication to ensure secure access. Claude Code supports the OAuth 2.0 authentication flow for these secure connections.

### Steps for Authentication:

1.  **Add the remote server**: First, add the remote server using the `claude mcp add` command as you would any other server.
2.  **Initiate authentication**: Within Claude Code, type the `/mcp` command. This will open an interactive menu where you can:
    *   View the connection status for all your configured servers.
    *   Authenticate with servers that require OAuth.
    *   Clear existing authentication tokens.
    *   View the capabilities exposed by each server.
3.  **Complete the OAuth flow**: When you select 
