
# Brave Search MCP

The Brave Search MCP integrates Claude Code with Brave Search, enabling it to perform web and local searches. This powerful integration allows Claude to gather up-to-date information from the internet, making it an invaluable tool for research, fact-checking, and staying current with real-world data.

## Capabilities

*   **Web Search**: Perform searches across the internet using Brave Search.
*   **Local Search**: Potentially search local files or indexed content (depending on Brave Search configuration and server implementation).
*   **Information Retrieval**: Extract relevant snippets, links, and summaries from search results.

## Configuration

To add the Brave Search MCP, you typically use `npx` to run the official server. You might need to configure an API key if Brave Search requires one for programmatic access.

```bash
claude mcp add brave-search-server --command npx --args -y @modelcontextprotocol/server-brave-search
```

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "brave-search": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-brave-search"
      ]
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Brave Search MCP to perform searches.

### 1. Performing a Web Search

Ask Claude to search for information on a specific topic:

```
Search Brave for the latest news on Model Context Protocol developments.
```

Claude will execute the search and provide a summary of the top results, including relevant links.

### 2. Fact-Checking Information

Instruct Claude to verify a piece of information:

```
Is it true that the Model Context Protocol was released in 2023? Verify this using Brave Search.
```

Claude will search for the information and report its findings, indicating whether the statement is accurate.

### 3. Researching a Topic

Ask Claude to conduct research on a broader topic:

```
Research the key features of the latest Claude AI model using Brave Search.
```

Claude will provide a comprehensive overview based on its search results.

## Best Practices

*   **Specific Queries**: Formulate clear and concise search queries to get the most relevant results.
*   **Evaluate Sources**: Remind Claude to critically evaluate the credibility of sources, especially for sensitive information.
*   **Rate Limiting**: Be mindful of any rate limits imposed by the Brave Search API to avoid service interruptions.

For more details, refer to the [official Brave Search MCP documentation](https://modelcontextprotocol.io/examples/brave-search).

