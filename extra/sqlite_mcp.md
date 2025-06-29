
# SQLite MCP

The SQLite MCP provides Claude Code with read-only access to SQLite databases. This allows Claude to inspect database schemas, query data, and understand the structure of your application's data without the risk of accidental modifications.

## Capabilities

*   **Read-Only Access**: Securely query data and inspect schemas without write permissions.
*   **Schema Inspection**: Understand table structures, columns, and relationships.
*   **Data Querying**: Execute SQL `SELECT` statements to retrieve data.

## Configuration

To add the SQLite MCP, you typically use `npx` to run the official server. You will need to provide the path to your SQLite database file.

```bash
claude mcp add sqlite-server --command npx --args -y @modelcontextprotocol/server-sqlite /path/to/your/database.db
```

*   Replace `/path/to/your/database.db` with the actual path to your SQLite database file.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "sqlite": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sqlite",
        "./data/app.db"
      ]
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the SQLite MCP to interact with your database.

### 1. Inspecting Database Schema

Ask Claude to describe the schema of a table:

```
Describe the schema of the 'users' table in the SQLite database.
```

Claude will provide details about the columns, data types, and constraints of the `users` table.

### 2. Querying Data

Ask Claude to retrieve data from a table:

```
Get the names and emails of all users from the 'users' table where 'age' is greater than 30.
```

Claude will execute the appropriate SQL query and return the results.

## Best Practices

*   **Read-Only for Safety**: The read-only nature of this MCP is a security feature. Avoid using it for operations that require data modification.
*   **Specific Queries**: Guide Claude with specific questions to get precise results from the database.
*   **Error Handling**: Be prepared for Claude to report SQL errors if queries are malformed or refer to non-existent tables/columns.

For more details, refer to the [official SQLite MCP documentation](https://modelcontextprotocol.io/examples/sqlite).




**Note**: The SQLite MCP is actively maintained in the [official MCP servers repository](https://github.com/modelcontextprotocol/servers).

