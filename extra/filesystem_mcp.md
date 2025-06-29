# Filesystem MCP

## Overview
The Filesystem MCP provides Claude with secure access to your local filesystem, enabling file and directory operations. This is one of the most fundamental MCPs for local development workflows, allowing Claude to read, write, create, and manage files and directories on your system.

## Installation

### Prerequisites
- Node.js 16+ or Python 3.8+
- Claude Desktop application

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx @modelcontextprotocol/server-filesystem
```

#### Option 2: Global Installation
```bash
npm install -g @modelcontextprotocol/server-filesystem
```

#### Option 3: Python Implementation
```bash
pip install mcp-server-filesystem
```

## Configuration

### Claude Desktop Configuration
Add to your Claude Desktop configuration file:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "/path/to/allowed/directory"
      ]
    }
  }
}
```

### Python Configuration
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "python",
      "args": [
        "-m", "mcp_server_filesystem",
        "/path/to/allowed/directory"
      ]
    }
  }
}
```

### Multiple Directory Access
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "/home/user/projects",
        "/home/user/documents",
        "/home/user/scripts"
      ]
    }
  }
}
```

## Usage Examples

### Basic File Operations
```
# Read a file
Can you read the contents of /path/to/file.txt?

# Write to a file
Please create a new file called example.py with a simple "Hello World" script.

# List directory contents
Show me all files in the /path/to/directory folder.

# Create directories
Create a new directory structure: /projects/new-app/src/components
```

### Advanced Operations
```
# Search for files
Find all Python files in the project directory that contain the word "database".

# File analysis
Analyze the structure of this codebase and create a summary of the main components.

# Batch operations
Rename all .txt files in this directory to have a .md extension.

# File comparison
Compare these two configuration files and show me the differences.
```

### Development Workflows
```
# Project setup
Create a new React project structure with all necessary files and folders.

# Code review
Review all JavaScript files in the src/ directory for potential improvements.

# Documentation generation
Generate README files for each subdirectory based on the code contents.

# File organization
Organize these files into appropriate directories based on their content and purpose.
```

## Features

### Core Capabilities
- **File Reading**: Read text and binary files
- **File Writing**: Create and modify files
- **Directory Operations**: Create, list, and navigate directories
- **File Management**: Copy, move, rename, and delete files
- **Permission Handling**: Respect file system permissions
- **Path Resolution**: Handle relative and absolute paths
- **Symbolic Links**: Follow and manage symbolic links

### Security Features
- **Sandboxed Access**: Restricted to specified directories
- **Permission Checks**: Validates file system permissions
- **Path Validation**: Prevents directory traversal attacks
- **Safe Operations**: Atomic file operations where possible

### Advanced Features
- **File Watching**: Monitor files for changes
- **Batch Operations**: Perform operations on multiple files
- **Pattern Matching**: Use glob patterns for file selection
- **Metadata Access**: Read file stats, permissions, and timestamps
- **Binary Support**: Handle binary files and images

## Requirements

### System Requirements
- **Operating System**: Windows, macOS, or Linux
- **Node.js**: Version 16 or higher (for Node.js implementation)
- **Python**: Version 3.8 or higher (for Python implementation)
- **Disk Space**: Minimal (< 10MB)
- **Memory**: Low memory footprint

### Permissions
- Read/write access to specified directories
- Appropriate file system permissions
- Network access for MCP communication

## Security Considerations

### Best Practices
- **Limit Scope**: Only grant access to necessary directories
- **Regular Audits**: Review file access patterns regularly
- **Backup Important Data**: Always backup before bulk operations
- **Monitor Usage**: Keep track of file system operations

### Directory Restrictions
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "/home/user/safe-directory"
      ]
    }
  }
}
```

## Troubleshooting

### Common Issues

#### Permission Denied
**Problem**: Cannot access files or directories
**Solution**: 
- Check file system permissions
- Ensure Claude Desktop has necessary access rights
- Verify directory paths are correct

#### Path Not Found
**Problem**: Specified paths don't exist
**Solution**:
- Verify directory paths in configuration
- Use absolute paths when possible
- Check for typos in path specifications

#### Server Won't Start
**Problem**: MCP server fails to initialize
**Solution**:
- Verify Node.js/Python installation
- Check configuration syntax
- Ensure all dependencies are installed

#### Slow Performance
**Problem**: File operations are slow
**Solution**:
- Limit directory scope
- Avoid deep directory structures
- Use specific paths instead of broad access

### Configuration Validation
```bash
# Test the configuration
npx @modelcontextprotocol/server-filesystem --help

# Verify directory access
ls -la /path/to/configured/directory
```

## Advanced Configuration

### Environment Variables
```bash
export MCP_FILESYSTEM_ROOT="/custom/root/path"
export MCP_FILESYSTEM_READONLY="true"
```

### Custom Scripts
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "/path/to/custom/filesystem-wrapper.sh",
      "args": ["/allowed/directory"]
    }
  }
}
```

## Integration Examples

### With Git MCP
```
# Combined workflow
1. Use filesystem MCP to read project files
2. Use git MCP to check version history
3. Make changes with filesystem MCP
4. Commit changes with git MCP
```

### With Code Analysis
```
# Code review workflow
1. Read all source files
2. Analyze code structure
3. Generate improvement suggestions
4. Create updated files
```

## Links

- [Official MCP Repository](https://github.com/modelcontextprotocol/servers)
- [Filesystem MCP Documentation](https://modelcontextprotocol.io/servers/filesystem)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [Claude Desktop Configuration](https://claude.ai/docs/desktop)
- [Security Best Practices](https://modelcontextprotocol.io/security)

## Community Resources

- [MCP Community Discord](https://discord.gg/mcp)
- [Example Configurations](https://github.com/modelcontextprotocol/examples)
- [Troubleshooting Guide](https://modelcontextprotocol.io/troubleshooting)
- [Best Practices](https://modelcontextprotocol.io/best-practices)

