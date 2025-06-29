
# `DigitalOcean MCP`: Cloud Infrastructure Management for Claude

`DigitalOcean MCP` is a powerful Model Context Protocol (MCP) server that connects Claude Code to your DigitalOcean account. This integration allows Claude to directly interact with your cloud infrastructure, enabling it to deploy applications, fetch logs, restart services, and perform various other cloud management tasks through natural language commands.

## Key Features

*   **Cloud Resource Management**: Control DigitalOcean resources like Droplets, App Platform, and more.
*   **Application Deployment**: Deploy applications directly from GitHub repositories.
*   **Monitoring and Logging**: Fetch application logs and monitor environments.
*   **Service Control**: Restart or delete services on your DigitalOcean account.
*   **Contextual Understanding**: Claude can understand and act upon your cloud infrastructure based on the provided context.

## How it Works

The `DigitalOcean MCP` server acts as an intermediary between Claude Code and the DigitalOcean API. You configure the MCP server with a DigitalOcean personal access token (with appropriate scopes), and then Claude can send requests to this server. The server translates Claude's natural language commands into API calls to DigitalOcean, executes them, and returns the results to Claude.

## Installation and Usage

To set up the DigitalOcean MCP, you typically need to:

1.  **Generate a DigitalOcean Personal Access Token**: This token needs to have read/write access to the App Platform (or other services you want Claude to manage).
2.  **Install Claude Code**: Ensure Claude Code CLI is installed and configured on your local machine.
3.  **Add the DigitalOcean MCP Server**: Use the `claude mcp add` command to register the DigitalOcean MCP server with Claude Code, providing your personal access token as an environment variable.

### Example Command (Conceptual)

```bash
claude mcp add digitalocean-mcp-local -e DIGITALOCEAN_TOKEN="YOUR_TOKEN" -- npx "@digitalocean/mcp"
```

Once configured, you can then use natural language prompts within Claude Code to manage your DigitalOcean resources:

```
List all my apps on DigitalOcean
Create a new app from this GitHub repo: https://github.com/do-community/do-one-click-deploy-flask
```

Claude will ask for approval before executing the tool calls.

## Use Cases

*   **Automated Deployments**: Deploy new versions of your applications with a simple natural language command.
*   **Infrastructure as Code (AI-driven)**: Manage your cloud infrastructure using conversational AI.
*   **Troubleshooting and Diagnostics**: Quickly fetch logs or restart services to diagnose issues.
*   **Resource Optimization**: Monitor and manage cloud resources efficiently.

## Source

For more detailed instructions and the official GitHub repository, refer to the DigitalOcean community tutorial:

*   [Setting Up the DigitalOcean MCP Server in Claude Code | DigitalOcean](https://www.digitalocean.com/community/tutorials/claude-code-mcp-server)


