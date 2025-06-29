
# CLAUDE.md Files: Enhancing Claude's Contextual Understanding

`CLAUDE.md` files are a powerful feature in Claude Code that allow you to provide Claude with project-specific context, guidelines, and information. These files are automatically pulled into Claude's context at the start of a conversation, making them an ideal place to document anything you want Claude to remember or adhere to during your coding sessions.

## What to Include in `CLAUDE.md`

`CLAUDE.md` files are highly flexible, but here are common and effective types of information to include:

*   **Common Bash Commands**: Frequently used commands for building, testing, or deploying your project.
*   **Core Files and Utility Functions**: Pointers to important files or helper functions that Claude should be aware of.
*   **Code Style Guidelines**: Specific formatting rules, naming conventions, or architectural patterns to follow.
*   **Testing Instructions**: How to run tests, specific test commands, or testing methodologies.
*   **Repository Etiquette**: Guidelines for branching, commit message formats, pull request procedures, etc.
*   **Developer Environment Setup**: Instructions for setting up the development environment, including tool versions or dependencies.
*   **Unexpected Behaviors or Warnings**: Any known quirks, common pitfalls, or warnings specific to the project.
*   **Project Overview**: A high-level summary of the project's purpose, architecture, or key modules.

There is no strict format for `CLAUDE.md` files; they should be concise and human-readable, similar to a well-maintained project README.

## Placement of `CLAUDE.md` Files

`CLAUDE.md` files can be placed in several strategic locations, and Claude will automatically discover them based on your current working directory:

*   **Root of Your Repository**: The most common usage. Name it `CLAUDE.md` and check it into Git to share with your team. You can also use `CLAUDE.local.md` and `.gitignore` it for personal, unshared context.
*   **Parent Directories**: In monorepos, Claude will pull `CLAUDE.md` files from any parent directory of where you run `claude`. This allows for shared context across multiple sub-projects.
*   **Child Directories**: Claude will pull `CLAUDE.md` files on demand when you work with files within child directories.
*   **Your Home Folder (`~/.claude/CLAUDE.md`)**: This file applies to all your Claude Code sessions, providing global context.

When you run the `/init` command in Claude Code, it can automatically generate a basic `CLAUDE.md` file for you.

## Tuning Your `CLAUDE.md` Files

Treat your `CLAUDE.md` files as living documents that evolve with your project. Regularly refine their content to maximize Claude's effectiveness:

*   **Iterate on Effectiveness**: Experiment with different phrasing and content to see what produces the best instruction following from Claude.
*   **Manual Editing**: Directly edit the `CLAUDE.md` file using your preferred text editor.
*   **In-Session Updates**: Use the `#` key within Claude Code to give Claude an instruction that it will automatically incorporate into the relevant `CLAUDE.md` file. Many engineers use this frequently to document commands, files, and style guidelines on the fly.
*   **Prompt Engineering**: Occasionally run your `CLAUDE.md` files through prompt improvers or add emphasis (e.g., `IMPORTANT:`, `YOU MUST:`) to critical instructions to improve Claude's adherence.

## Best Practices

*   **Conciseness**: Keep `CLAUDE.md` files focused and to the point. Avoid unnecessary verbosity.
*   **Actionable Information**: Prioritize information that directly helps Claude understand its task and environment.
*   **Version Control**: For team projects, always check `CLAUDE.md` files into version control to ensure consistency across the team.
*   **Security**: Be cautious about including sensitive information (e.g., API keys, passwords) directly in `CLAUDE.md` files, especially if they are checked into public repositories. Use environment variables or secure secrets management instead.

By effectively utilizing `CLAUDE.md` files, you can significantly improve Claude Code's performance, reduce the need for repetitive instructions, and ensure consistent behavior across your projects.

