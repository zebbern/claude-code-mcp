
# `disler/quick-data-mcp`: Prompt-Focused Data Analytics for Claude Code

`disler/quick-data-mcp` is an MCP server specifically designed for agentic data analytics on `.json` and `.csv` files within Claude Code. Its purpose is to maximize the value of custom-built MCP servers by integrating tools, resources, and prompts to create reusable agentic workflows (ADWs).

## Key Features

*   **Data Analysis**: Provides arbitrary data analysis capabilities on `.json` and `.csv` file formats.
*   **Agentic Workflows**: Focuses on creating structured prompts with integrated tools and resources for repeatable data analysis tasks.
*   **Tools, Resources, and Prompts**: Leverages the three core building blocks of MCP to extend AI model capabilities:
    *   **Tools**: For AI to perform actions (e.g., `create_task`).
    *   **Resources**: For AI to read data (e.g., `get_user_profile`).
    *   **Prompts**: Pre-built conversation templates for structured workflows (e.g., `code_review`).

## How it Works

This MCP server allows Claude Code to perform data analysis by providing it with the necessary tools to interact with data files. It emphasizes the combination of tools, resources, and prompts to create efficient and reusable workflows for data-related tasks.

## Installation and Usage

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/disler/quick-data-mcp.git
    cd quick-data-mcp/
    ```
2.  **Configure for your MCP client**:
    ```bash
    cp .mcp.json.sample .mcp.json
    # Edit .mcp.json and update the --directory path to your absolute path
    # Example: "/Users/yourusername/path/to/quick-data-mcp"
    ```
3.  **Test the server**:
    ```bash
    uv run python main.py
    ```

## Use Cases

*   **Automated Data Processing**: Process and analyze `.json` and `.csv` files automatically.
*   **Data Insights**: Extract insights from structured data using natural language queries.
*   **Custom Data Workflows**: Build and automate custom data analysis workflows within Claude Code.

## Source

*   [GitHub Repository: `disler/quick-data-mcp`](https://github.com/disler/quick-data-mcp)


