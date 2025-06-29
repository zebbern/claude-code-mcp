
# PostgreSQL MCP

The PostgreSQL MCP provides Claude Code with read-only access to PostgreSQL databases, enabling it to perform schema inspection, data querying, and business intelligence tasks. Similar to the SQLite MCP, it focuses on safe, read-only operations to prevent unintended data modifications.

## Capabilities

*   **Read-Only Database Access**: Securely query data and inspect schemas without write permissions.
*   **Schema Inspection**: Understand table structures, columns, relationships, and other database objects.
*   **Data Querying**: Execute SQL `SELECT` statements to retrieve data.
*   **Business Intelligence**: Facilitate data analysis and reporting by querying large datasets.

## Configuration

To add the PostgreSQL MCP, you typically use `npx` to run the official server. You will need to provide the connection string for your PostgreSQL database.

```bash
claude mcp add postgres-server --command npx --args -y @modelcontextprotocol/server-postgres "postgresql://user:password@host:port/database"
```

*   Replace `"postgresql://user:password@host:port/database"` with your actual PostgreSQL connection string. Ensure proper escaping if your connection string contains special characters.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-postgres",
        "postgresql://readonly_user:secure_password@localhost:5432/my_app_db"
      ]
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the PostgreSQL MCP to interact with your database.

### 1. Inspecting Table Structure

Ask Claude to describe the structure of a specific table:

```
Describe the columns and their types for the 'orders' table in the PostgreSQL database.
```

Claude will provide a detailed description of the `orders` table schema.

### 2. Performing Data Analysis

Ask Claude to perform a data analysis query:

```
From the 'sales' table, find the total sales for each product category in the last month.
```

Claude will formulate and execute the appropriate SQL query, then present the results.

### 3. Understanding Relationships

Ask Claude to explain relationships between tables:

```
Explain the relationship between the 'customers' and 'orders' tables.
```

Claude will analyze the schema and describe how these tables are linked, likely through foreign keys.

## Best Practices

*   **Use Read-Only Users**: Always configure the PostgreSQL connection with a user that has only read permissions to prevent accidental data modification.
*   **Secure Credentials**: Avoid hardcoding sensitive credentials directly in the `.mcp.json` file. Consider using environment variables or a secure secrets management system.
*   **Optimize Queries**: For large databases, guide Claude to formulate efficient queries to avoid long execution times.

For more details, refer to the [official PostgreSQL MCP documentation](https://modelcontextprotocol.io/examples/postgres).

