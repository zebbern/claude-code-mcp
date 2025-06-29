
# Puppeteer MCP (Archived)

**⚠️ IMPORTANT: This MCP server is archived and no longer maintained. For the latest information and actively maintained servers, please visit the [official MCP servers repository](https://github.com/modelcontextprotocol/servers).**

The Puppeteer MCP was designed to enable Claude Code to perform browser automation and web scraping tasks. This allows Claude to interact with web pages, fill forms, click elements, and extract information, extending its capabilities to the dynamic world of web content.

## Capabilities

*   **Browser Navigation**: Navigate to specified URLs.
*   **Element Interaction**: Click on elements, input text into fields.
*   **Content Extraction**: Extract text, HTML, or specific data from web pages.
*   **Screenshot Capture**: Capture screenshots of web pages.
*   **JavaScript Execution**: Execute custom JavaScript in the browser context.

## Configuration

As an archived MCP, specific configuration details may be outdated. Typically, configuring this MCP would involve setting up a headless Chrome instance and providing its connection details.

## Usage Examples

### 1. Navigating to a Website and Extracting Content

Ask Claude to visit a website and extract its main heading:

```
Using the Puppeteer MCP, navigate to example.com and extract the text content of the main heading (h1 tag).
```

### 2. Filling a Form and Submitting

Instruct Claude to fill out a simple form on a web page:

```
Using the Puppeteer MCP, navigate to a form page, input "John Doe" into the name field, "john.doe@example.com" into the email field, and then click the submit button.
```

## Best Practices

*   **Ethical Scraping**: Always respect `robots.txt` and website terms of service. Avoid excessive requests that could overload a server.
*   **Error Handling**: Implement robust error handling for network issues, element not found, or unexpected page structures.
*   **Headless vs. Headful**: For most automation, headless mode is sufficient. For debugging, a headful browser might be useful.
*   **Selectors**: Use stable and specific CSS selectors or XPath expressions to target elements reliably.

For historical reference, you can find the source code for this archived MCP in the [servers-archived repository](https://github.com/modelcontextprotocol/servers-archived).


