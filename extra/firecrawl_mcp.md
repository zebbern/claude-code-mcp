
# `Firecrawl MCP`: Web Scraping and Content Extraction

**Official Firecrawl MCP Server** - Adds powerful web scraping to Cursor, Claude, and any other LLM clients.

This MCP server integrates with [Firecrawl](https://www.firecrawl.dev/) for robust web scraping capabilities, allowing Claude to:

*   Perform web scraping, crawling, and discovery.
*   Execute search and content extraction tasks.
*   Conduct deep research and batch scraping.
*   Handle automatic retries and rate limiting.
*   Support both cloud and self-hosted deployments.
*   Utilize Server-Sent Events (SSE) for real-time updates.

## Installation and Configuration

### Prerequisites

*   Node.js and npm installed.
*   A Firecrawl API key (obtainable from [https://www.firecrawl.dev/app/api-keys](https://www.firecrawl.dev/app/api-keys)).

### Global Installation (CLI)

```shell
npm install -g firecrawl-mcp
```

### Running Locally

```shell
env FIRECRAWL_API_KEY=fc-YOUR_API_KEY npx -y firecrawl-mcp
```

To run the server using Server-Sent Events (SSE) locally instead of the default stdio transport:

```shell
env SSE_LOCAL=true FIRECRAWL_API_KEY=fc-YOUR_API_KEY npx -y firecrawl-mcp
```

Use the URL: `http://localhost:3000/sse`

### Configuration for Claude Code / Desktop

#### For Claude Desktop (via `claude_desktop_config.json`)

Add the following to your `claude_desktop_config.json` file:

```json
{
  "mcpServers": {
    "mcp-server-firecrawl": {
      "command": "npx",
      "args": ["-y", "firecrawl-mcp"],
      "env": {
        "FIRECRAWL_API_KEY": "YOUR_API_KEY_HERE",

        "FIRECRAWL_RETRY_MAX_ATTEMPTS": "5",
        "FIRECRAWL_RETRY_INITIAL_DELAY": "2000",
        "FIRECRAWL_RETRY_MAX_DELAY": "30000",
        "FIRECRAWL_RETRY_BACKOFF_FACTOR": "3",

        "FIRECRAWL_CREDIT_WARNING_THRESHOLD": "2000",
        "FIRECRAWL_CREDIT_CRITICAL_THRESHOLD": "500"
      }
    }
  }
}
```

#### For VS Code (User Settings JSON)

Add this to your User Settings (JSON) file in VS Code (`Ctrl + Shift + P` and type `Preferences: Open User Settings (JSON)`):

```json
{
  "mcp": {
    "inputs": [
      {
        "type": "promptString",
        "id": "apiKey",
        "description": "Firecrawl API Key",
        "password": true
      }
    ],
    "servers": {
      "firecrawl": {
        "command": "npx",
        "args": ["-y", "firecrawl-mcp"],
        "env": {
          "FIRECRAWL_API_KEY": "${input:apiKey}"
        }
      }
    }
  }
}
```

#### For VS Code (Workspace `.vscode/mcp.json`)

Optionally, add it to a file called `.vscode/mcp.json` in your workspace to share the configuration:

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "apiKey",
      "description": "Firecrawl API Key",
      "password": true
    }
  ],
  "servers": {
    "firecrawl": {
      "command": "npx",
      "args": ["-y", "firecrawl-mcp"],
      "env": {
        "FIRECRAWL_API_KEY": "${input:apiKey}"
      }
    }
  }
}
```

### Environment Variables

The server includes several configurable parameters that can be set via environment variables:

*   `FIRECRAWL_API_KEY`: Your Firecrawl API key (Required for cloud API, optional for self-hosted).
*   `FIRECRAWL_API_URL` (Optional): Custom API endpoint for self-hosted instances (e.g., `https://firecrawl.your-domain.com`).
*   `FIRECRAWL_RETRY_MAX_ATTEMPTS`: Maximum number of retry attempts (default: `3`).
*   `FIRECRAWL_RETRY_INITIAL_DELAY`: Initial delay in milliseconds before first retry (default: `1000`).
*   `FIRECRAWL_RETRY_MAX_DELAY`: Maximum delay in milliseconds between retries (default: `10000`).
*   `FIRECRAWL_RETRY_BACKOFF_FACTOR`: Exponential backoff multiplier (default: `2`).
*   `FIRECRAWL_CREDIT_WARNING_THRESHOLD`: Credit usage warning threshold (default: `1000`).
*   `FIRECRAWL_CREDIT_CRITICAL_THRESHOLD`: Credit usage critical threshold (default: `100`).

## Usage Examples

Once configured, Claude can utilize Firecrawl MCP for various web scraping tasks. For instance, you can explicitly request it by describing your web scraping needs. Access the Composer via Command+L (Mac), select "Agent" next to the submit button, and enter your query.

```
/scrape-url https://example.com
```

This will instruct Claude to use the Firecrawl MCP to scrape the content of `https://example.com`.

