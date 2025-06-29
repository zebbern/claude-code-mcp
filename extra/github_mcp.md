
# GitHub MCP

The GitHub MCP extends Claude Code's capabilities to interact with GitHub repositories, providing advanced features for repository management, file operations, and direct integration with the GitHub API. This is invaluable for developers working on open-source projects or within teams that heavily rely on GitHub.

## Capabilities

*   **Repository Management**: Create, delete, or modify repositories.
*   **File Operations**: Read, write, and manage files within GitHub repositories.
*   **Issue & Pull Request Management**: Create, update, and comment on issues and pull requests.
*   **GitHub API Integration**: Direct access to various GitHub API functionalities.

## Configuration

To add the GitHub MCP, you typically use `npx` to run the official server. You will need to provide a GitHub Personal Access Token (PAT) for authentication. It's highly recommended to use environment variables for sensitive tokens.

```bash
claude mcp add github-server --command npx --args -y @modelcontextprotocol/server-github --env GITHUB_PERSONAL_ACCESS_TOKEN=<YOUR_TOKEN>
```

*   Replace `<YOUR_TOKEN>` with your actual GitHub Personal Access Token. Ensure it has the necessary scopes for the operations you intend to perform.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

## Usage Examples

Once configured and authenticated, Claude can use the GitHub MCP to interact with your GitHub repositories.

### 1. Creating a New Issue

Ask Claude to create a new issue in a specified repository:

```
Create a new issue in the 'my-org/my-repo' repository with the title 'Bug: Login button not working' and description 'The login button on the homepage does not respond when clicked.'.
```

Claude will create the issue on GitHub.

### 2. Reading a File from a Repository

Instruct Claude to read the content of a file from a GitHub repository:

```
Read the content of 'src/main.js' from the 'my-org/my-repo' repository.
```

Claude will fetch and display the file's content.

### 3. Commenting on a Pull Request

Ask Claude to add a comment to a pull request:

```
Add a comment to pull request #123 in 'my-org/my-repo' saying 'Looks good, but please address the linter warnings.'.
```

Claude will post the comment on the specified pull request.

## Best Practices

*   **Token Security**: Never hardcode your PAT directly in scripts or public files. Use environment variables or secure secrets management.
*   **Least Privilege**: Grant your PAT only the minimum necessary scopes to perform its intended tasks.
*   **Review Actions**: Always review Claude's proposed actions before confirming, especially for destructive operations like deleting repositories or force-pushing.

For more details, refer to the [official GitHub MCP documentation](https://modelcontextprotocol.io/examples/github).

