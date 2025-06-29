
# GitLab MCP

The GitLab MCP integrates Claude Code with GitLab, allowing it to interact with GitLab repositories, issues, merge requests, and other API functionalities. This is particularly useful for teams and individuals who use GitLab for their software development lifecycle.

## Capabilities

*   **Repository Interaction**: Access and manage files within GitLab repositories.
*   **Issue & Merge Request Management**: Create, update, and comment on issues and merge requests.
*   **CI/CD Pipeline Interaction**: Potentially trigger or monitor CI/CD pipelines (depending on server implementation and permissions).
*   **GitLab API Integration**: Direct access to various GitLab API functionalities.

## Configuration

To add the GitLab MCP, you typically use `npx` to run the official server. You will need to provide a GitLab Personal Access Token for authentication. It's highly recommended to use environment variables for sensitive tokens.

```bash
claude mcp add gitlab-server --command npx --args -y @modelcontextprotocol/server-gitlab --env GITLAB_PERSONAL_ACCESS_TOKEN=<YOUR_TOKEN> --env GITLAB_URL=<YOUR_GITLAB_URL>
```

*   Replace `<YOUR_TOKEN>` with your actual GitLab Personal Access Token.
*   Replace `<YOUR_GITLAB_URL>` with the URL of your GitLab instance (e.g., `https://gitlab.com`).

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "gitlab": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-gitlab"
      ],
      "env": {
        "GITLAB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>",
        "GITLAB_URL": "https://gitlab.com"
      }
    }
  }
}
```

## Usage Examples

Once configured and authenticated, Claude can use the GitLab MCP to interact with your GitLab projects.

### 1. Creating a New Issue

Ask Claude to create a new issue in a specified GitLab project:

```
Create a new issue in the project ID 12345 with the title 'Feature: Implement dark mode' and description 'Users should be able to switch to a dark theme.'.
```

Claude will create the issue on GitLab.

### 2. Reading a File from a Repository

Instruct Claude to read the content of a file from a GitLab repository:

```
Read the content of 'src/config.js' from the project 'my-group/my-project'.
```

Claude will fetch and display the file's content.

### 3. Commenting on a Merge Request

Ask Claude to add a comment to a merge request:

```
Add a comment to merge request !42 in 'my-group/my-project' saying 'Looks good, ready for review.'.
```

Claude will post the comment on the specified merge request.

## Best Practices

*   **Token Security**: Store your GitLab PAT securely using environment variables or a secrets manager.
*   **Least Privilege**: Grant your PAT only the minimum necessary scopes required for the intended operations.
*   **Review Actions**: Always review Claude's proposed actions before confirming, especially for actions that modify your GitLab projects.

For more details, refer to the [official GitLab MCP documentation](https://modelcontextprotocol.io/examples/gitlab).

