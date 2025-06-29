
# Slack MCP

The Slack MCP integrates Claude Code with Slack, enabling it to manage channels, send messages, and interact with your team within the Slack environment. This is particularly useful for automating communication, summarizing discussions, or triggering actions based on Slack events.

## Capabilities

*   **Channel Management**: List, create, or join Slack channels.
*   **Messaging**: Send messages to channels or direct messages to users.
*   **Information Retrieval**: Read messages from channels or threads.
*   **User Interaction**: Mention users, react to messages.

## Configuration

To add the Slack MCP, you typically use `npx` to run the official server. You will need to provide a Slack Bot Token or User Token for authentication. It is highly recommended to use environment variables for sensitive tokens.

```bash
claude mcp add slack-server --command npx --args -y @modelcontextprotocol/server-slack --env SLACK_BOT_TOKEN=<YOUR_TOKEN>
```

*   Replace `<YOUR_TOKEN>` with your actual Slack Bot Token. Ensure it has the necessary scopes for the operations you intend to perform.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-slack"
      ],
      "env": {
        "SLACK_BOT_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

## Usage Examples

Once configured and authenticated, Claude can use the Slack MCP to interact with Slack.

### 1. Sending a Message to a Channel

Ask Claude to send a message to a specific Slack channel:

```
Send a message to the #general channel in Slack: "Daily standup reminder: Please post your updates!"
```

Claude will post the message to the `#general` channel.

### 2. Summarizing a Channel Discussion

Instruct Claude to read recent messages from a channel and summarize them:

```
Summarize the last 10 messages from the #development channel in Slack.
```

Claude will fetch the messages and provide a concise summary.

### 3. Listing Users in a Channel

Ask Claude to list all members of a specific channel:

```
List all users in the #project-x channel in Slack.
```

Claude will provide a list of user names or IDs.

## Best Practices

*   **Token Security**: Protect your Slack tokens. Use environment variables or a secure secrets management system.
*   **Least Privilege**: Grant your Slack app or bot only the minimum necessary scopes to perform its intended tasks.
*   **User Experience**: Be mindful of message frequency and content to avoid spamming channels or overwhelming users.
*   **Error Handling**: Instruct Claude on how to handle cases where channels or users are not found, or API limits are hit.

For more details, refer to the [official Slack MCP documentation](https://modelcontextprotocol.io/examples/slack).


# Slack MCP (Archived)

**⚠️ IMPORTANT: This MCP server is archived and no longer maintained. For the latest information and actively maintained servers, please visit the [official MCP servers repository](https://github.com/modelcontextprotocol/servers).**

The Slack MCP provides Claude Code with capabilities to interact with Slack, enabling channel management and messaging. This can be useful for automating team communications, sending notifications, or summarizing discussions within Claude Code.

## Capabilities

*   **Channel Management**: Create, archive, or retrieve information about Slack channels.
*   **Messaging**: Send messages to specific channels or users.
*   **Discussion Summarization**: Potentially summarize conversations from Slack channels (requires further integration logic).

## Configuration

Since this MCP is archived, the original configuration methods may no longer be applicable. Typically, configuring this MCP would involve providing Slack API tokens and workspace details.

## Usage Examples

### 1. Sending a Message to a Channel

Ask Claude to send a message to a specific Slack channel:

```
Using the Slack MCP, send the message "Daily standup reminder: Please post your updates!" to the #daily-standup channel.
```

### 2. Creating a New Channel

Instruct Claude to create a new Slack channel:

```
Using the Slack MCP, create a new public channel named #project-alpha-updates.
```

## Best Practices

*   **Permissions**: Ensure the Slack bot token or user token used by the MCP server has only the necessary permissions (e.g., `chat:write`, `channels:read`).
*   **Rate Limiting**: Be mindful of Slack API rate limits to avoid being blocked.
*   **Contextual Communication**: Use Claude to draft and send messages that are relevant to the current task or project context.

For historical reference, you can find the source code for this archived MCP in the [servers-archived repository](https://github.com/modelcontextprotocol/servers-archived).


