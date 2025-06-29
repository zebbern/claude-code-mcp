# Git MCP

## Overview
The Git MCP provides Claude with comprehensive Git version control capabilities, enabling repository management, commit operations, branch handling, and collaboration workflows. This MCP is essential for any development workflow involving version control.

## Installation

### Prerequisites
- Git installed on your system
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Access to Git repositories

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx @modelcontextprotocol/server-git
```

#### Option 2: Global Installation
```bash
npm install -g @modelcontextprotocol/server-git
```

#### Option 3: From Source
```bash
git clone https://github.com/modelcontextprotocol/servers.git
cd servers/src/git
npm install
npm run build
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "git": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-git"]
    }
  }
}
```

### With Specific Repository
```json
{
  "mcpServers": {
    "git": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "--repository", "/path/to/repository"
      ]
    }
  }
}
```

### Multiple Repositories
```json
{
  "mcpServers": {
    "git": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "--repositories", "/path/to/repo1,/path/to/repo2"
      ]
    }
  }
}
```

## Usage Examples

### Basic Git Operations
```
# Check repository status
What's the current status of the Git repository?

# View commit history
Show me the last 10 commits in this repository.

# Create a new branch
Create a new branch called "feature/new-functionality".

# Switch branches
Switch to the main branch.

# Stage and commit changes
Stage all modified files and commit with message "Fix bug in user authentication".
```

### Advanced Git Workflows
```
# Interactive rebase
Help me rebase the last 3 commits interactively.

# Merge branches
Merge the feature branch into main with a merge commit.

# Cherry-pick commits
Cherry-pick commit abc123 from the develop branch.

# Resolve merge conflicts
Show me the current merge conflicts and help resolve them.

# Create and apply patches
Create a patch file for the last commit.
```

### Repository Management
```
# Clone repositories
Clone the repository from https://github.com/user/repo.git

# Add remotes
Add a new remote called "upstream" pointing to the original repository.

# Fetch and pull updates
Fetch all updates from origin and merge them into the current branch.

# Push changes
Push the current branch to origin with upstream tracking.
```

### Code Analysis with Git
```
# Blame analysis
Show me who last modified each line in this file.

# Diff analysis
Compare the current working directory with the last commit.

# Log analysis
Find all commits that modified the authentication module.

# Statistics
Generate a summary of repository activity over the last month.
```

## Features

### Core Git Operations
- **Repository Status**: Check working directory and staging area
- **Commit Management**: Create, view, and modify commits
- **Branch Operations**: Create, switch, merge, and delete branches
- **Remote Operations**: Fetch, pull, push, and manage remotes
- **Staging**: Add, remove, and reset staged changes
- **History**: View and search commit history

### Advanced Features
- **Interactive Rebase**: Modify commit history
- **Cherry-picking**: Apply specific commits
- **Stashing**: Save and restore work-in-progress
- **Tagging**: Create and manage release tags
- **Submodules**: Handle Git submodules
- **Hooks**: Manage Git hooks

### Analysis Capabilities
- **Blame**: Track line-by-line authorship
- **Diff**: Compare changes between commits/branches
- **Log Search**: Find commits by message, author, or file
- **Statistics**: Repository activity and contribution metrics
- **Conflict Resolution**: Identify and resolve merge conflicts

### Integration Features
- **GitHub Integration**: Work with GitHub repositories
- **GitLab Support**: Compatible with GitLab workflows
- **Bitbucket**: Support for Bitbucket repositories
- **SSH Keys**: Handle SSH authentication
- **GPG Signing**: Support for signed commits

## Requirements

### System Requirements
- **Git**: Version 2.20 or higher
- **Operating System**: Windows, macOS, or Linux
- **Node.js**: Version 16 or higher
- **Memory**: 50MB+ available RAM
- **Disk Space**: Varies by repository size

### Authentication
- SSH keys configured for remote repositories
- Git credentials properly set up
- Access tokens for private repositories
- GPG keys for signed commits (optional)

### Permissions
- Read/write access to Git repositories
- Network access for remote operations
- File system permissions for repository directories

## Security Considerations

### Best Practices
- **SSH Keys**: Use SSH keys instead of passwords
- **Access Tokens**: Use personal access tokens for HTTPS
- **Repository Scope**: Limit access to necessary repositories
- **Credential Storage**: Use secure credential storage
- **Signed Commits**: Enable GPG signing for verification

### Configuration Security
```json
{
  "mcpServers": {
    "git": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "--safe-mode",
        "--repository", "/trusted/repo/path"
      ]
    }
  }
}
```

## Troubleshooting

### Common Issues

#### Authentication Failed
**Problem**: Cannot access remote repositories
**Solution**:
- Check SSH key configuration: `ssh -T git@github.com`
- Verify access tokens are valid
- Update Git credentials: `git config --global credential.helper`

#### Permission Denied
**Problem**: Cannot perform Git operations
**Solution**:
- Check file system permissions
- Verify repository ownership
- Ensure Git is properly installed

#### Merge Conflicts
**Problem**: Conflicts during merge operations
**Solution**:
- Use `git status` to identify conflicted files
- Manually resolve conflicts in affected files
- Stage resolved files and complete merge

#### Repository Not Found
**Problem**: Cannot locate Git repository
**Solution**:
- Verify repository path in configuration
- Check if directory is a Git repository: `git status`
- Initialize repository if needed: `git init`

### Configuration Validation
```bash
# Test Git installation
git --version

# Verify repository access
git status

# Check remote configuration
git remote -v
```

## Advanced Configuration

### Custom Git Commands
```json
{
  "mcpServers": {
    "git": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "--custom-commands", "/path/to/git-aliases.json"
      ]
    }
  }
}
```

### Environment Variables
```bash
export GIT_AUTHOR_NAME="Your Name"
export GIT_AUTHOR_EMAIL="your.email@example.com"
export GIT_EDITOR="code --wait"
```

### Git Hooks Integration
```bash
# Pre-commit hook example
#!/bin/sh
echo "Running pre-commit checks..."
npm test
```

## Workflow Examples

### Feature Development
```
1. Create feature branch: git checkout -b feature/new-feature
2. Make changes and commit regularly
3. Push branch: git push -u origin feature/new-feature
4. Create pull request
5. Merge after review
```

### Release Management
```
1. Create release branch: git checkout -b release/v1.2.0
2. Update version numbers
3. Create release tag: git tag -a v1.2.0 -m "Release v1.2.0"
4. Push tag: git push origin v1.2.0
```

### Hotfix Workflow
```
1. Create hotfix branch from main
2. Fix critical issue
3. Test thoroughly
4. Merge to main and develop
5. Tag hotfix release
```

## Integration with Other MCPs

### With Filesystem MCP
```
# Combined workflow
1. Use filesystem MCP to read/write files
2. Use git MCP to track changes
3. Commit and push updates
```

### With GitHub MCP
```
# Enhanced GitHub workflow
1. Use git MCP for local operations
2. Use github MCP for pull requests
3. Coordinate between local and remote
```

## Links

- [Official Git MCP Repository](https://github.com/modelcontextprotocol/servers/tree/main/src/git)
- [Git Documentation](https://git-scm.com/doc)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [Pro Git Book](https://git-scm.com/book)
- [Git Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)

## Community Resources

- [Git Community](https://git-scm.com/community)
- [MCP Discord](https://discord.gg/mcp)
- [Git Best Practices](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)
- [Troubleshooting Guide](https://git-scm.com/docs/git-help)

