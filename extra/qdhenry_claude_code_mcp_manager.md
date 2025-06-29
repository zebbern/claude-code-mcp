
# `qdhenry/Claude-Code-MCP-Manager`: A Comprehensive MCP Configuration Tool

`qdhenry/Claude-Code-MCP-Manager` is a comprehensive bash script designed to simplify the management of Model Context Protocol (MCP) configurations for Claude Code. It provides a user-friendly command-line interface to add, remove, list, and automatically load MCP configurations, significantly streamlining the setup process for developers.

## Key Features

*   **List MCPs**: View all configured MCPs in a clear, organized format.
*   **Add/Remove MCPs**: Interactively manage your MCP configurations.
*   **Batch Operations**: Add multiple MCPs at once without individual prompts.
*   **Auto-loading**: Automatically load MCPs when starting Claude Code, ensuring your tools are always ready.
*   **Import/Export**: Save and restore your MCP configurations, facilitating backup and sharing.
*   **Sample Configurations**: Initialize your setup with common and useful MCP configurations.

## Prerequisites

*   **Bash shell**: Compatible with both bash and zsh.
*   **`jq`**: A lightweight and flexible command-line JSON processor. Installation instructions:
    *   **macOS**: `brew install jq`
    *   **Ubuntu/Debian**: `sudo apt-get install jq`
    *   **RHEL/CentOS**: `sudo yum install jq`
    *   **Arch Linux**: `sudo pacman -S jq`

## Installation

You can install the MCP Manager by either downloading the script directly or cloning the GitHub repository.

### Option 1: Download the Script

```bash
# Download the script
curl -O https://raw.githubusercontent.com/qdhenry/Claude-Code-MCP-Manager/main/mcp-manager.sh

# Make it executable
chmod +x mcp-manager.sh

# (Optional) Move to a location in your PATH
sudo mv mcp-manager.sh /usr/local/bin/mcp-manager
```

### Option 2: Clone the Repository

```bash
# Clone the repository
git clone https://github.com/qdhenry/Claude-Code-MCP-Manager.git

# Navigate to the directory
cd Claude-Code-MCP-Manager

# Make the script executable
chmod +x mcp-manager.sh

# (Optional) Create a symbolic link
sudo ln -s $(pwd)/mcp-manager.sh /usr/local/bin/mcp-manager
```

## Basic Usage

1.  **Initialize with sample MCPs**:
    ```bash
    ./mcp-manager.sh init
    ```
2.  **Edit the configuration to add your tokens** (replace `<your-token>` placeholders):
    ```bash
    nano ~/.config/claude/mcp_config.json
    ```
3.  **List all MCPs**:
    ```bash
    ./mcp-manager.sh list
    ```
4.  **Add all MCPs to Claude**:
    ```bash
    ./mcp-manager.sh add-all
    ```

## Command Reference

*   **`list` / `ls`**: List all configured MCPs.
*   **`add`**: Add a new MCP interactively.
*   **`add-all`**: Add all MCPs defined in the configuration without prompts.
*   **`remove <mcp_name>` / `rm <mcp_name>`**: Remove a specific MCP.
*   **`show <mcp_name>`**: Show details of a specific MCP.
*   **`export [filename]`**: Export configurations to a file.
*   **`import <filename>`**: Import configurations from a file.
*   **`init`**: Initialize with sample MCPs.
*   **`setup-auto`**: Set up automatic loading of MCPs when Claude Code starts.
*   **`help`**: Display help information.

## Configuration File

The MCP Manager stores its configuration in `~/.config/claude/mcp_config.json`. The structure is a JSON array of MCP objects, each with `name`, `type` (`npx` or `env`), `path`, and `options`.

### Example Configuration (`~/.config/claude/mcp_config.json`)

```json
{
  "mcps": [
    {
      "name": "supabase",
      "type": "npx",
      "path": "supabase/mcp-server-supabase@latest",
      "options": "--access-token YOUR_TOKEN_HERE"
    },
    {
      "name": "digitalocean",
      "type": "env",
      "path": "DIGITALOCEAN_API_TOKEN=YOUR_TOKEN_HERE",
      "options": "npx -y @digitalocean/mcp"
    }
  ]
}
```

## Automatic Loading

To automatically load all MCPs when starting Claude Code:

1.  Run the setup command:
    ```bash
    ./mcp-manager.sh setup-auto
    ```
2.  Reload your shell (e.g., `source ~/.bashrc` or `source ~/.zshrc`).
3.  Start Claude Code (e.g., `claude-code` or the alias `cc`).

## Best Practices

*   **Secure Tokens**: Never commit your configuration file with real API tokens to public repositories.
*   **Regular Backups**: Export your configuration regularly.
*   **Version Control**: Consider keeping your MCP configurations in a private Git repository.
*   **Team Sharing**: Use import/export functionality to share configurations (excluding sensitive tokens) with your team.
*   **Minimal MCPs**: Only load the MCPs you actively need to optimize performance.

## Source

[https://github.com/qdhenry/Claude-Code-MCP-Manager](https://github.com/qdhenry/Claude-Code-MCP-Manager)


