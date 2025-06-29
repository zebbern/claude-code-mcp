
# Google Drive MCP

The Google Drive MCP allows Claude Code to access and manage files within your Google Drive. This enables Claude to search for documents, read their content, and potentially organize files, making it a powerful tool for document-heavy workflows.

## Capabilities

*   **File Access**: Read content of files stored in Google Drive.
*   **File Search**: Search for files by name, type, or content.
*   **File Organization**: Potentially move, copy, or delete files (requires appropriate permissions and careful use).

## Configuration

To add the Google Drive MCP, you typically use `npx` to run the official server. This MCP will likely require OAuth 2.0 authentication to access your Google Drive account.

```bash
claude mcp add google-drive-server --command npx --args -y @modelcontextprotocol/server-google-drive
```

After adding the server, you will need to authenticate it using the `/mcp` command within Claude Code, which will guide you through the OAuth flow in your browser.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "google-drive": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-google-drive"
      ]
    }
  }
}
```

## Usage Examples

Once configured and authenticated, Claude can use the Google Drive MCP to interact with your files.

### 1. Searching for a Document

Ask Claude to find a specific document in your Google Drive:

```
Find the document titled 'Project Proposal Q3' in my Google Drive.
```

Claude will search your Google Drive and provide links or information about the found document.

### 2. Reading Document Content

Instruct Claude to read the content of a Google Doc:

```
Read the content of the document at @google-drive:file://<document_id_or_path>.
```

Claude will fetch the content of the specified document.

### 3. Organizing Files (Use with Caution)

While possible, use file organization commands with extreme caution and explicit confirmation.

```
Move the file 'Old Report.docx' from 'Reports/2024' to 'Archive/2024' in Google Drive.
```

Claude will prompt for confirmation before performing such an action.

## Best Practices

*   **Strict Permissions**: Only grant the necessary permissions during the OAuth flow. Prefer read-only access if write operations are not strictly required.
*   **Explicit Instructions**: Be very clear and specific when asking Claude to perform actions on your Google Drive, especially for modifications.
*   **Regular Review**: Periodically review the permissions granted to the Google Drive MCP and revoke access if no longer needed.

For more details, refer to the [official Google Drive MCP documentation](https://modelcontextprotocol.io/examples/google-drive).

