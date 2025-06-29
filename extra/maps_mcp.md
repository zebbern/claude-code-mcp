
# Maps MCP

The Maps MCP integrates Claude Code with mapping services, enabling it to provide location-based information, directions, and details about places. This is useful for applications requiring geographical context, travel planning, or local search functionalities.

## Capabilities

*   **Location Services**: Get coordinates for addresses, or addresses for coordinates.
*   **Directions**: Calculate routes and provide turn-by-turn directions between locations.
*   **Place Details**: Retrieve information about points of interest, businesses, and landmarks.
*   **Geocoding/Reverse Geocoding**: Convert between human-readable addresses and geographical coordinates.

## Configuration

To add the Maps MCP, you typically use `npx` to run the official server. You will likely need an API key from a mapping service (e.g., Google Maps API, OpenStreetMap).

```bash
claude mcp add maps-server --command npx --args -y @modelcontextprotocol/server-maps --env MAPS_API_KEY=<YOUR_API_KEY>
```

*   Replace `<YOUR_API_KEY>` with your actual mapping service API key.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "maps": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-maps"
      ],
      "env": {
        "MAPS_API_KEY": "<YOUR_API_KEY>"
      }
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Maps MCP to provide location-based information.

### 1. Getting Directions

Ask Claude for directions between two locations:

```
Give me walking directions from "Eiffel Tower, Paris" to "Louvre Museum, Paris".
```

Claude will provide a step-by-step route.

### 2. Finding Place Details

Instruct Claude to find details about a specific place:

```
What is the address and phone number of "The British Museum, London"?
```

Claude will retrieve and display the requested information.

### 3. Geocoding an Address

Ask Claude to convert an address to coordinates:

```
What are the geographical coordinates for "1600 Amphitheatre Parkway, Mountain View, CA"?
```

Claude will return the latitude and longitude.

## Best Practices

*   **API Key Security**: Protect your mapping service API key. Use environment variables or a secure secrets management system.
*   **Rate Limits**: Be aware of and respect the rate limits of the mapping service API to avoid service interruptions.
*   **Clarity in Queries**: Provide clear and unambiguous location names or addresses to ensure accurate results.

For more details, refer to the [official Maps MCP documentation](https://modelcontextprotocol.io/examples/maps).

