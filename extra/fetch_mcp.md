
# Fetch MCP

The Fetch MCP enables Claude Code to access and process web content, optimizing it for LLM consumption. This is particularly useful for tasks that require Claude to gather information from the internet, summarize articles, or extract data from web pages.

## Capabilities

*   **Web Content Fetching**: Retrieve content from specified URLs.
*   **Content Conversion**: Convert fetched web content into a format optimized for LLM processing (e.g., plain text, Markdown).
*   **Error Handling**: Manages common web fetching issues like timeouts or network errors.

## Configuration

To add the Fetch MCP, you typically use `npx` to run the official server.

```bash
claude mcp add fetch-server --command npx --args -y @modelcontextprotocol/server-fetch
```

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "fetch": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-fetch"
      ]
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Fetch MCP to interact with web content.

### 1. Fetching and Summarizing a Web Page

Ask Claude to fetch a URL and then summarize its content:

```
Summarize the main points from the article at @fetch:url://https://www.example.com/article.
```

Claude will fetch the content and provide a summary based on its understanding.

### 2. Extracting Specific Information

Instruct Claude to extract specific data from a web page:

```
From the page at @fetch:url://https://www.example.com/products, list all product names and their prices.
```

Claude will attempt to parse the page and extract the requested information.

## Best Practices

*   **Respect Robots.txt**: Ensure your usage complies with the website's `robots.txt` file and terms of service.
*   **Rate Limiting**: Be mindful of the frequency of requests to avoid overwhelming target servers.
*   **Error Handling**: Instruct Claude on how to handle cases where web content cannot be fetched or is not in the expected format.

For more details, refer to the [official Fetch MCP documentation](https://modelcontextprotocol.io/examples/fetch).

