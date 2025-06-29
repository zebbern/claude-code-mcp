
# Time MCP

The Time MCP provides Claude Code with capabilities related to time and timezone conversions. This is useful for tasks that require precise time information, scheduling, or handling time differences across various geographical locations.

## Capabilities

*   **Current Time**: Get the current time in various formats and timezones.
*   **Timezone Conversion**: Convert time from one timezone to another.
*   **Time Calculations**: Perform calculations involving dates and times (e.g., adding/subtracting durations).
*   **Timezone Information**: Retrieve details about specific timezones.

## Configuration

To add the Time MCP, you typically use `npx` to run the official server.

```bash
claude mcp add time-server --command npx --args -y @modelcontextprotocol/server-time
```

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "time": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-time"
      ]
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Time MCP to handle time-related queries.

### 1. Getting the Current Time in a Specific Timezone

Ask Claude for the current time in a particular city:

```
What is the current time in Tokyo?
```

Claude will use the Time MCP to provide the accurate current time in JST.

### 2. Converting Time Between Timezones

Instruct Claude to convert a time from one timezone to another:

```
If it's 3 PM in London, what time is it in New York?
```

Claude will perform the timezone conversion and provide the result.

### 3. Calculating Future Dates

Ask Claude to calculate a future date based on a given duration:

```
What will be the date and time exactly 72 hours from now?
```

Claude will use the Time MCP to perform the calculation.

## Best Practices

*   **Specify Timezones**: Always specify timezones clearly (e.g., "EST", "UTC", "Europe/London") to avoid ambiguity.
*   **Format Clarity**: If you need time in a specific format (e.g., 24-hour, with seconds), mention it in your prompt.
*   **Contextual Use**: Integrate time information into broader workflows, such as scheduling meetings or logging events with timestamps.

For more details, refer to the [official Time MCP documentation](https://modelcontextprotocol.io/examples/time).




**Note**: The Time MCP is actively maintained in the [official MCP servers repository](https://github.com/modelcontextprotocol/servers).

