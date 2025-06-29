
# Browser MCP

The Browser MCP empowers Claude Code with web browsing and automation capabilities. This allows Claude to navigate web pages, interact with elements, fill forms, and extract information, making it a powerful tool for tasks like data collection, testing web applications, and interacting with online services.

## Capabilities

*   **Web Navigation**: Open URLs and navigate between web pages.
*   **Element Interaction**: Click buttons, fill text fields, select dropdown options.
*   **Content Extraction**: Extract text, images, and other data from web pages.
*   **Form Submission**: Automate form filling and submission.
*   **Screenshot Capture**: Capture screenshots of web pages.

## Configuration

To add the Browser MCP, you typically use `npx` to run the official server. This MCP often relies on headless browser technologies like Puppeteer.

```bash
claude mcp add browser-server --command npx --args -y @modelcontextprotocol/server-browser
```

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "browser": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-browser"
      ]
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Browser MCP to automate web interactions.

### 1. Navigating to a Website and Extracting Text

Ask Claude to visit a website and extract specific text:

```
Go to https://www.example.com and extract the main heading text.
```

Claude will navigate to the page and return the requested text.

### 2. Filling a Form and Submitting

Instruct Claude to fill out a web form:

```
On the page @browser:url://https://www.example.com/contact, fill the 'name' field with 'John Doe', the 'email' field with 'john.doe@example.com', and click the 'Submit' button.
```

Claude will perform the actions as instructed.

### 3. Taking a Screenshot

Ask Claude to capture a screenshot of a web page:

```
Take a screenshot of @browser:url://https://www.example.com and save it as 'example_homepage.png'.
```

Claude will save the screenshot to your local file system (requires Filesystem MCP or similar for saving).

## Best Practices

*   **Ethical Use**: Always ensure your automated browsing complies with website terms of service and legal regulations.
*   **Error Handling**: Instruct Claude on how to handle unexpected pop-ups, redirects, or element not found errors.
*   **Rate Limiting**: Implement delays between actions to avoid being blocked by websites.
*   **Headless vs. Headful**: Consider whether a headless browser (no visible UI) or a headful browser (with UI) is more appropriate for your task.

For more details, refer to the [official Browser MCP documentation](https://modelcontextprotocol.io/examples/browser).

