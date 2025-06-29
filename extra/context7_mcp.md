
# Context 7 MCP

Context 7 is a built-in Model Context Protocol (MCP) server within Claude Code that automatically pulls relevant context into prompts. It is particularly useful for providing Claude with immediate access to project-specific information, coding standards, and operational guidelines.

## Key Features

*   **Automatic Context Injection**: Claude automatically incorporates information from `CLAUDE.md` files into its context, reducing the need for manual copy-pasting.
*   **Project-Specific Guidance**: Ideal for documenting common bash commands, core files, code style guidelines, testing instructions, repository etiquette, developer environment setup, and project-specific warnings.
*   **Monorepo Support**: Can be configured to pull context from parent directories (for monorepos) or child directories (on demand).
*   **Home Folder Integration**: A global `CLAUDE.md` file can be placed in `~/.claude/CLAUDE.md` for general instructions.

## Configuration and Usage

Context 7 is typically built-in and does not require explicit `claude mcp add` commands. Its behavior is primarily controlled through `CLAUDE.md` files.

### `CLAUDE.md` Files

`CLAUDE.md` files are special Markdown files that Claude Code automatically reads to understand the project context. They can be placed in various locations:

*   **Repository Root**: For general project-wide instructions.
*   **Parent Directories**: In monorepos, for context relevant to multiple sub-projects.
*   **Child Directories**: For context specific to a particular module or component.
*   **Home Folder**: `~/.claude/CLAUDE.md` for user-specific global instructions.

### Example `CLAUDE.md` Content

```markdown
# Project Guidelines

## Coding Standards

*   All Python code must adhere to PEP 8.
*   Use type hints for all function arguments and return values.

## Testing Instructions

To run tests, execute: `pytest --strict-markers`

## Important Notes

*   **IMPORTANT**: Do not modify files in the `dist/` directory directly. They are generated automatically.
*   **YOU MUST**: Ensure all new features have corresponding unit tests.

## Common Commands

*   `npm run build`: Builds the project.
*   `npm test`: Runs all tests.
```

### Tuning `CLAUDE.md` Files

*   **Treat as Living Documents**: Regularly update `CLAUDE.md` files as your project evolves.
*   **Use `#` Key**: In Claude Code, use the `#` key to automatically incorporate instructions into `CLAUDE.md` based on your conversation.
*   **Emphasize Critical Instructions**: Use terms like "IMPORTANT" or "YOU MUST" for crucial guidelines.

## Best Practices

*   **Granularity**: Break down complex instructions into smaller, digestible sections within `CLAUDE.md`.
*   **Clarity**: Write clear, concise, and unambiguous instructions.
*   **Version Control**: Keep `CLAUDE.md` files under version control to track changes and ensure consistency across the team.
*   **Avoid Redundancy**: Do not duplicate information that is readily available elsewhere (e.g., in official documentation), but summarize key points relevant to Claude.

## Source

Context 7 is a core component of Claude Code. For more details, refer to the official Anthropic documentation on Claude Code best practices, particularly the section on `CLAUDE.md` files.

*   [Claude Code: Best practices for agentic coding - Anthropic](https://www.anthropic.com/engineering/claude-code-best-practices)



ver that provides context to Claude from your current working directory. It helps Claude understand the project structure, files, and relevant information without explicit prompting.

**Key Features:**
*   **Automatic Context**: Automatically provides Claude with relevant files and directory structure.
*   **Seamless Integration**: Works out-of-the-box with Claude Code.
*   **Improved Understanding**: Helps Claude better understand the project and generate more accurate responses.

**Usage:**
Context 7 is typically enabled by default in Claude Code. You can verify its status and configuration through the Claude Code interface or by checking your `.claude/settings.json` file.

**Source**: Often a built-in or default component of Claude Code environments, though specific documentation might be integrated within the main Claude Code documentation.

