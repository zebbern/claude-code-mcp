
# Memory MCP

The Memory MCP provides Claude Code with a knowledge graph-based persistent memory system. This allows Claude to store and retrieve information across conversations, enabling it to build a long-term understanding of your project, preferences, and previous interactions.

## Capabilities

*   **Persistent Storage**: Store key-value pairs, notes, and other information that persists across sessions.
*   **Knowledge Graph**: Organizes information in a graph structure, allowing for more complex relationships and queries.
*   **Information Retrieval**: Retrieve stored information based on keywords, concepts, or relationships.

## Configuration

To add the Memory MCP, you typically use `npx` to run the official server.

```bash
claude mcp add memory-server --command npx --args -y @modelcontextprotocol/server-memory
```

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "memory": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-memory"
      ]
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Memory MCP to store and retrieve information.

### 1. Storing Information

Ask Claude to remember a specific piece of information:

```
Remember that the project's primary color is #4A90E2. Use the key 'primary-color'.
```

Claude will store this information in its memory.

### 2. Retrieving Information

Ask Claude to recall previously stored information:

```
What is the project's primary color?
```

Claude will retrieve the value associated with 'primary-color' from its memory and provide the answer.

### 3. Using Memory in Workflows

Instruct Claude to use its memory to perform a task:

```
Generate a CSS file using the project's primary color for the main button class.
```

Claude will retrieve the primary color from its memory and use it in the generated CSS.

## Best Practices

*   **Be Specific**: When storing information, use clear and descriptive keys to avoid ambiguity.
*   **Regularly Review**: Periodically review the information stored in Claude's memory to ensure it is still relevant and accurate.
*   **Combine with Other MCPs**: Use the Memory MCP in conjunction with other MCPs to create powerful, context-aware workflows.

For more details, refer to the [official Memory MCP documentation](https://modelcontextprotocol.io/examples/memory).

