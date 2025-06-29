
# Sentry MCP

The Sentry MCP allows Claude Code to retrieve and analyze issues from Sentry.io, a popular error tracking and performance monitoring platform. This integration enables Claude to assist with debugging, incident response, and understanding application health by providing direct access to error data.

## Capabilities

*   **Issue Retrieval**: Fetch details of specific issues or a list of issues from Sentry.
*   **Error Analysis**: Analyze error logs, stack traces, and event data.
*   **Performance Monitoring**: Potentially access performance metrics and transaction data (depending on server implementation).

## Configuration

To add the Sentry MCP, you typically use `npx` to run the official server. You will need to provide your Sentry DSN (Data Source Name) or API key for authentication.

```bash
claude mcp add sentry-server --command npx --args -y @modelcontextprotocol/server-sentry --env SENTRY_DSN=<YOUR_DSN>
```

*   Replace `<YOUR_DSN>` with your actual Sentry DSN.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "sentry": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sentry"
      ],
      "env": {
        "SENTRY_DSN": "<YOUR_DSN>"
      }
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Sentry MCP to interact with your Sentry projects.

### 1. Investigating a Specific Issue

Ask Claude to investigate a Sentry issue by its ID:

```
Investigate Sentry issue ID 12345 in project 'my-project'.
```

Claude will retrieve the issue details, including stack traces, events, and user context, to help with debugging.

### 2. Listing Recent Errors

Ask Claude to list recent critical errors:

```
List the 5 most recent critical errors from Sentry project 'my-project'.
```

Claude will query Sentry and provide a summary of the requested errors.

### 3. Analyzing Error Trends

Instruct Claude to analyze error trends over a period:

```
Analyze the trend of errors in Sentry project 'my-project' over the last 24 hours.
```

Claude can help identify spikes or patterns in error occurrences.

## Best Practices

*   **Secure Credentials**: Protect your Sentry DSN or API key. Use environment variables or a secure secrets management system.
*   **Scope Permissions**: Ensure the Sentry token or DSN has only the necessary permissions (e.g., read-only access to events).
*   **Contextual Queries**: Provide Claude with sufficient context (e.g., project name, time range) when querying Sentry to get accurate results.

For more details, refer to the [official Sentry MCP documentation](https://modelcontextprotocol.io/examples/sentry).


# Sentry MCP (Archived)

**⚠️ IMPORTANT: This MCP server is archived and no longer maintained. For the latest information and actively maintained servers, please visit the [official MCP servers repository](https://github.com/modelcontextprotocol/servers).**

The Sentry MCP allows Claude Code to retrieve and analyze issues from Sentry.io, a popular error tracking and performance monitoring platform. This integration is valuable for developers who want Claude to assist with debugging, incident response, and understanding application health.

## Capabilities

*   **Issue Retrieval**: Fetch details about specific issues, including error messages, stack traces, and event data.
*   **Issue Search**: Search for issues based on various criteria (e.g., project, environment, status, tags).
*   **Event Analysis**: Access and analyze individual error events associated with an issue.

## Configuration

Since this MCP is archived, the original configuration methods may no longer be applicable. Typically, configuring this MCP would involve providing Sentry API keys and project DSNs.

## Usage Examples

### 1. Retrieving a Specific Sentry Issue

Ask Claude to get details about a Sentry issue given its ID:

```
Using the Sentry MCP, retrieve the details for issue ID `12345` from the `my-web-app` project.
```

### 2. Searching for Critical Errors

Instruct Claude to find all critical errors in a specific environment:

```
Using the Sentry MCP, find all issues with a `fatal` level in the `production` environment for the `backend-service` project.
```

## Best Practices

*   **Access Control**: Ensure that the Sentry API key used by the MCP server has only the necessary permissions.
*   **Contextual Queries**: Provide Claude with enough context (project name, environment, time range) to narrow down Sentry queries effectively.
*   **Actionable Insights**: Guide Claude to not just retrieve data but to analyze it and suggest potential causes or solutions.

For historical reference, you can find the source code for this archived MCP in the [servers-archived repository](https://github.com/modelcontextprotocol/servers-archived).


