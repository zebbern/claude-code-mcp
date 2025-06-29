
# Redis MCP (Archived)

**⚠️ IMPORTANT: This MCP server is archived and no longer maintained. For the latest information and actively maintained servers, please visit the [official MCP servers repository](https://github.com/modelcontextprotocol/servers).**

The Redis MCP provides Claude Code with the ability to interact with Redis key-value stores. This is useful for tasks that require caching, session management, or real-time data manipulation.

## Capabilities

*   **Key-Value Operations**: Perform standard Redis operations such as `GET`, `SET`, `DEL`, `EXISTS`, etc.
*   **Data Structures**: Interact with Redis data structures like lists, sets, and hashes.
*   **Database Management**: Manage Redis databases, including flushing and selecting databases.

## Configuration

Since this MCP is archived, the original configuration methods may no longer be applicable. However, a typical configuration would have involved providing the Redis server connection details (host, port, password) to the MCP server.

## Usage Examples

### 1. Storing and Retrieving Data

Ask Claude to store a value in Redis and then retrieve it:

```
Using the Redis MCP, set the key `user:123` to the value `{"name": "John Doe", "email": "john.doe@example.com"}`.

Now, retrieve the value for the key `user:123`.
```

### 2. Working with Lists

Instruct Claude to add items to a Redis list:

```
Using the Redis MCP, add the items "apple", "banana", and "cherry" to the list `my-favorite-fruits`.
```

## Best Practices

*   **Data Serialization**: When storing complex data structures, ensure they are properly serialized (e.g., as JSON strings) before sending them to Redis.
*   **Error Handling**: Be prepared to handle potential Redis errors, such as connection failures or key-not-found errors.
*   **Security**: When connecting to a production Redis instance, ensure that the connection is secure and that the MCP server has the necessary credentials.

For historical reference, you can find the source code for this archived MCP in the [servers-archived repository](https://github.com/modelcontextprotocol/servers-archived).


