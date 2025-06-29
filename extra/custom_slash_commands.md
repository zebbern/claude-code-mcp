
# Custom Slash Commands: Streamlining Workflows in Claude Code

Custom slash commands in Claude Code allow you to store and reuse prompt templates for repeated workflows. This feature significantly enhances productivity by enabling you to trigger complex sequences of instructions with a simple command, making your interactions with Claude more efficient and consistent.

## What are Custom Slash Commands?

Custom slash commands are essentially pre-defined prompt templates that you can invoke within Claude Code by typing `/` followed by the command name (e.g., `/debug-issue`, `/generate-tests`). They can include placeholders for arguments, allowing for dynamic input at the time of execution.

## Creating Custom Slash Commands

To create a custom slash command, you store your prompt templates in Markdown files within the `.claude/commands` folder of your project or home directory.

### Location:

*   **Project-specific**: `.claude/commands/` within your project directory. These commands are available only when working in that project and can be checked into version control for team sharing.
*   **Global**: `~/.claude/commands/` in your home directory. These commands are available across all your Claude Code sessions.

### File Structure:

Each custom slash command should be a separate Markdown file (e.g., `debug-issue.md`, `generate-tests.md`). The content of the file is the prompt template.

### Example: `debug-issue.md`

```markdown
Please analyze and fix the GitHub issue: $ARGUMENTS.

Follow these steps:

1. Use `gh issue view` to get the issue details
2. Understand the problem described in the issue
3. Search the codebase for relevant files
4. Implement the necessary changes to fix the issue
5. Write and run tests to verify the fix
6. Ensure code passes linting and type checking
7. Create a descriptive commit message
```

In this example, `$ARGUMENTS` is a special keyword that will be replaced by any text you provide after the slash command when you invoke it.

## Usage Examples

Once you have created a custom slash command, it becomes available in Claude Code.

### 1. Discovering Commands

Type `/` in your Claude Code session to see a list of all available commands, including your custom ones.

### 2. Executing a Command Without Arguments

If your command doesn't require arguments, simply type the command name:

```
/run-linter
```

### 3. Executing a Command With Arguments

If your command uses the `$ARGUMENTS` placeholder, provide the arguments space-separated after the command name:

```
/debug-issue #123
```

Claude will then execute the prompt template, replacing `$ARGUMENTS` with `#123`.

## Best Practices

*   **Modularity**: Break down complex workflows into smaller, reusable slash commands.
*   **Clear Naming**: Use descriptive and intuitive names for your command files.
*   **Argument Usage**: Clearly define what `$ARGUMENTS` expects in your prompt template.
*   **Version Control**: For team-specific commands, check them into your project's `.claude/commands/` directory to ensure consistency across the team.
*   **Iterative Refinement**: Just like `CLAUDE.md` files, refine your slash command prompts over time to optimize Claude's performance and output.

Custom slash commands are a powerful way to automate repetitive tasks and standardize complex workflows, making Claude Code an even more efficient and indispensable tool in your development toolkit.

