
# Sequential Thinking MCP

The Sequential Thinking MCP enables Claude Code to perform dynamic problem-solving through structured thought sequences. This MCP is designed to guide Claude through a series of logical steps, allowing it to break down complex problems, reason through solutions, and execute tasks in a methodical manner.

## Capabilities

*   **Structured Reasoning**: Guides Claude through predefined or dynamically generated sequences of thought.
*   **Problem Decomposition**: Helps Claude break down large problems into smaller, manageable sub-problems.
*   **Iterative Execution**: Facilitates iterative refinement of solutions by allowing Claude to execute steps and evaluate outcomes.

## Configuration

To add the Sequential Thinking MCP, you typically use `npx` to run the official server.

```bash
claude mcp add sequential-thinking-server --command npx --args -y @modelcontextprotocol/server-sequential-thinking
```

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Sequential Thinking MCP to approach problems systematically.

### 1. Debugging a Code Snippet

Instruct Claude to debug a code snippet by following a sequence of steps:

```
Debug the following Python code using sequential thinking:

```python
def divide(a, b):
    return a / b

print(divide(10, 0))
```

Steps:
1. Analyze the code for potential errors.
2. Identify the source of the error.
3. Propose a fix.
4. Verify the fix with a test case.
```

Claude will go through each step, providing its reasoning and actions.

### 2. Developing a Feature

Guide Claude through the development of a new feature:

```
Develop a new user authentication module. Use sequential thinking.

Steps:
1. Design the database schema for users.
2. Implement user registration API endpoint.
3. Implement user login API endpoint.
4. Write unit tests for both endpoints.
5. Document the API.
```

Claude will proceed step-by-step, generating code, tests, and documentation as it goes.

## Best Practices

*   **Clear Steps**: Provide clear, concise, and actionable steps for Claude to follow.
*   **Granularity**: Break down complex tasks into sufficiently granular steps to ensure effective execution.
*   **Feedback Loop**: Continuously review Claude's output at each step and provide feedback to refine its approach.

For more details, refer to the [official Sequential Thinking MCP documentation](https://modelcontextprotocol.io/examples/sequential-thinking).

