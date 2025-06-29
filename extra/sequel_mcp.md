
# `haxzie/sequel-mcp`: Database MCP Servers for Claude

`haxzie/sequel-mcp` provides Model Context Protocol (MCP) servers specifically designed for interacting with various databases. This allows Claude Code to query, manage, and interact with your databases directly from the terminal, eliminating the need for manual copy-pasting of SQL queries or schema information.

## Key Features

*   **Database Querying**: Execute SQL queries against supported databases.
*   **Schema Retrieval**: Get database schemas, enabling Claude to understand the database structure.
*   **Database Backups**: Potentially perform database backup operations (depending on specific implementation).
*   **Multi-Database Support**: Supports popular databases like PostgreSQL, MySQL, and ClickHouse.
*   **Client Compatibility**: Designed to work with Claude, Cursor, and Windsurf MCP clients.

## Supported Databases

*   **PostgreSQL**: `postgresql`
*   **MySQL**: `mysql`
*   **ClickHouse**: `clickhouse`

## Installation and Usage

To install and use the `sequel-mcp` server, you typically use `npx`:

### Install the MCP server to your client

```bash
npx -y @sequelsh/mcp@latest install
```

### Install a specific database MCP server

```bash
npx -y @sequelsh/mcp@latest install -d <database>
```

Replace `<database>` with one of the supported database names (e.g., `postgresql`, `mysql`, `clickhouse`).

### Install for a specific client

```bash
npx -y @sequelsh/mcp@latest install -c <client>
```

Replace `<client>` with `claude`, `cursor`, or `windsurf`.

### Development Setup (if contributing or running locally)

This project uses `Bun`, so ensure you have `Bun` installed.

```bash
bun install
bun run build
bun run mcp:install
```

## Usage Examples

Once installed, you can instruct Claude to interact with your database. The exact phrasing will depend on the tools exposed by the MCP server, but generally, it would involve natural language commands.

### 1. Querying Data

Ask Claude to retrieve data from a table:

```
Using the SQL MCP, query the `users` table and return the `name` and `email` for all users.
```

### 2. Getting Database Schema

Instruct Claude to provide the schema for a specific database or table:

```
Using the SQL MCP, provide the schema for the `products` table in the `ecommerce_db` database.
```

### 3. Performing Database Operations

Ask Claude to perform an update or insert (with caution and proper permissions):

```
Using the SQL MCP, update the `status` of order `12345` to `shipped` in the `orders` table.
```

## Best Practices

*   **Security**: Always ensure that the database credentials used by the MCP server have the principle of least privilege. Never expose sensitive production databases directly to an MCP server without strict access controls.
*   **Permissions**: Be mindful of the permissions granted to Claude Code and the MCP server, especially when dealing with write operations to databases.
*   **Clear Instructions**: Provide Claude with clear and unambiguous instructions for database interactions to avoid unintended consequences.
*   **Error Handling**: Be prepared to handle potential database errors or query failures.

## Source

[https://github.com/haxzie/sequel-mcp](https://github.com/haxzie/sequel-mcp)


