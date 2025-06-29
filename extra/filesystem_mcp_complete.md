# Filesystem MCP - Complete Guide

## Overview
The Filesystem MCP is one of the most essential Model Context Protocol implementations for Claude Code. It provides comprehensive file system operations, enabling Claude Code to read, write, create, delete, and manage files and directories with full control. This MCP transforms Claude Code into a powerful file management tool that can handle complex file operations, directory traversal, and file content manipulation.

## What Does Filesystem MCP Do?
- **File Operations**: Read, write, create, delete, copy, move files
- **Directory Management**: Create, delete, list, traverse directories
- **File Search**: Search for files by name, content, or patterns
- **Permission Management**: Handle file permissions and ownership
- **Symbolic Links**: Create and manage symbolic links
- **File Monitoring**: Watch for file changes and modifications
- **Batch Operations**: Perform bulk file operations efficiently
- **Content Analysis**: Analyze file content, encoding, and metadata

## Installation

### Prerequisites
- Claude Code CLI installed and configured
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Valid Anthropic API key
- Appropriate file system permissions

### Step 1: Install Filesystem MCP Server

#### Option 1: NPM Installation (Recommended)
```bash
# Install the official MCP filesystem server
npm install -g @modelcontextprotocol/server-filesystem

# Verify installation
npx @modelcontextprotocol/server-filesystem --version

# Test the server
npx @modelcontextprotocol/server-filesystem --help
```

#### Option 2: Python Installation
```bash
# Install Python version
pip install mcp-server-filesystem

# Verify installation
mcp-server-filesystem --version

# Test the server
mcp-server-filesystem --help
```

#### Option 3: Direct from GitHub
```bash
# Clone the repository
git clone https://github.com/modelcontextprotocol/servers.git
cd servers/src/filesystem

# Install dependencies
npm install

# Build the server
npm run build

# Test the server
npm start -- --help
```

#### Option 4: Docker Installation
```bash
# Pull the Docker image
docker pull mcpservers/filesystem:latest

# Run the container
docker run -d --name filesystem-mcp \
  -v /workspace:/workspace \
  -p 3000:3000 \
  mcpservers/filesystem:latest

# Verify container is running
docker ps | grep filesystem-mcp
```

### Step 2: Configure Claude Desktop

#### Basic Configuration
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "/workspace"
      ],
      "env": {
        "NODE_ENV": "production"
      }
    }
  }
}
```

#### Advanced Configuration
```json
{
  "mcpServers": {
    "filesystem-advanced": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "/workspace",
        "--allow-write",
        "--allow-delete",
        "--max-file-size", "100MB",
        "--watch-changes"
      ],
      "env": {
        "NODE_ENV": "production",
        "LOG_LEVEL": "info",
        "MAX_CONCURRENT_OPERATIONS": "10",
        "ENABLE_SYMLINKS": "true",
        "ENABLE_HIDDEN_FILES": "false"
      }
    }
  }
}
```

#### Multiple Workspace Configuration
```json
{
  "mcpServers": {
    "filesystem-workspace1": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "/workspace/project1"
      ]
    },
    "filesystem-workspace2": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "/workspace/project2"
      ]
    },
    "filesystem-home": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-filesystem",
        "/home/user",
        "--read-only"
      ]
    }
  }
}
```

### Step 3: Verify Installation
```bash
# Check if Claude Desktop recognizes the MCP
# Open Claude Desktop and look for filesystem tools

# Test file operations
echo "Test file content" > /workspace/test.txt

# In Claude Desktop, ask:
# "Can you read the contents of test.txt?"
# "List all files in the current directory"
# "Create a new file called hello.txt with 'Hello World'"
```

## Commands and Usage

### Basic File Operations

#### Reading Files
```bash
# Claude Code commands you can use:
"Read the contents of package.json"
"Show me the first 10 lines of README.md"
"Display the content of src/main.js"
"Read all .env files in the project"

# Direct MCP tool calls:
read_file: {
  "path": "/workspace/package.json"
}

read_file: {
  "path": "/workspace/README.md",
  "start_line": 1,
  "end_line": 10
}
```

#### Writing Files
```bash
# Claude Code commands:
"Create a new file called config.json with the following content: {...}"
"Write a Python script that prints 'Hello World' to hello.py"
"Update the README.md file to include installation instructions"
"Append the current timestamp to log.txt"

# Direct MCP tool calls:
write_file: {
  "path": "/workspace/config.json",
  "content": "{\n  \"name\": \"my-project\",\n  \"version\": \"1.0.0\"\n}"
}

append_file: {
  "path": "/workspace/log.txt",
  "content": "\n2024-01-01 12:00:00 - Application started"
}
```

#### File Management
```bash
# Claude Code commands:
"Delete the temporary files in the temp/ directory"
"Copy all .js files from src/ to backup/"
"Move the old-config.json file to archive/"
"Rename setup.py to install.py"

# Direct MCP tool calls:
delete_file: {
  "path": "/workspace/temp/temp-file.txt"
}

copy_file: {
  "source": "/workspace/src/main.js",
  "destination": "/workspace/backup/main.js"
}

move_file: {
  "source": "/workspace/old-config.json",
  "destination": "/workspace/archive/old-config.json"
}
```

### Directory Operations

#### Listing Directories
```bash
# Claude Code commands:
"List all files and directories in the current workspace"
"Show me the directory structure of the src/ folder"
"Find all Python files in the project"
"List hidden files in the home directory"

# Direct MCP tool calls:
list_directory: {
  "path": "/workspace"
}

list_directory: {
  "path": "/workspace/src",
  "recursive": true,
  "include_hidden": false,
  "filter": "*.py"
}
```

#### Creating Directories
```bash
# Claude Code commands:
"Create a new directory called 'tests' in the project root"
"Make a nested directory structure: src/components/ui"
"Create directories for logs, temp, and cache"

# Direct MCP tool calls:
create_directory: {
  "path": "/workspace/tests"
}

create_directory: {
  "path": "/workspace/src/components/ui",
  "recursive": true
}
```

### Advanced File Operations

#### File Search and Pattern Matching
```bash
# Claude Code commands:
"Find all files containing the word 'TODO' in their content"
"Search for all JavaScript files that import React"
"Find configuration files (*.conf, *.config, *.json) in the project"
"Locate all files modified in the last 24 hours"

# Direct MCP tool calls:
search_files: {
  "pattern": "TODO",
  "path": "/workspace",
  "content_search": true,
  "recursive": true
}

find_files: {
  "pattern": "*.{js,ts,jsx,tsx}",
  "path": "/workspace/src",
  "content_filter": "import.*React"
}
```

#### File Information and Metadata
```bash
# Claude Code commands:
"Get detailed information about package.json"
"Show file permissions for all files in the config/ directory"
"Check the size and modification date of large files"
"Analyze the encoding of text files"

# Direct MCP tool calls:
get_file_info: {
  "path": "/workspace/package.json"
}

get_directory_stats: {
  "path": "/workspace/config",
  "include_permissions": true,
  "include_metadata": true
}
```

#### Batch Operations
```bash
# Claude Code commands:
"Rename all .txt files to .md files in the docs/ directory"
"Copy all image files from assets/ to public/images/"
"Delete all .log files older than 7 days"
"Change permissions of all shell scripts to executable"

# Direct MCP tool calls:
batch_rename: {
  "path": "/workspace/docs",
  "pattern": "*.txt",
  "replacement": "*.md"
}

batch_copy: {
  "source_pattern": "/workspace/assets/*.{jpg,png,gif}",
  "destination": "/workspace/public/images/"
}
```

## Usage Examples

### Project Setup and Management
```bash
# Example 1: Initialize a new project structure
"Create a new project structure with the following directories:
- src/
  - components/
  - utils/
  - styles/
- tests/
  - unit/
  - integration/
- docs/
- config/
- scripts/"

# Example 2: Setup configuration files
"Create the following configuration files:
1. package.json with basic Node.js project setup
2. .gitignore with common Node.js ignores
3. README.md with project description
4. .env.example with sample environment variables"

# Example 3: Code organization
"Organize the source code by:
1. Moving all utility functions to src/utils/
2. Creating separate directories for each component
3. Adding index.js files for clean imports
4. Setting up a consistent file naming convention"
```

### Development Workflow Integration
```bash
# Example 1: Pre-commit checks
"Before committing, please:
1. Check for any TODO comments in the codebase
2. Verify all test files have corresponding source files
3. Ensure all JavaScript files have proper JSDoc comments
4. List any files that might need attention"

# Example 2: Code review preparation
"Prepare for code review by:
1. Listing all modified files in the last commit
2. Checking for any hardcoded values that should be configurable
3. Verifying consistent code formatting
4. Generating a summary of changes made"

# Example 3: Deployment preparation
"Prepare for deployment by:
1. Creating a build directory structure
2. Copying production files to the build directory
3. Removing development-only files
4. Generating a deployment manifest"
```

### File Content Analysis
```bash
# Example 1: Code analysis
"Analyze the codebase and provide:
1. A count of lines of code by file type
2. List of all external dependencies
3. Identification of potential security issues
4. Suggestions for code organization improvements"

# Example 2: Documentation audit
"Review the documentation and:
1. Check if all public functions have documentation
2. Verify all README files are up to date
3. Identify missing documentation
4. Suggest improvements to existing docs"

# Example 3: Configuration validation
"Validate the project configuration by:
1. Checking all config files for syntax errors
2. Verifying environment variables are properly documented
3. Ensuring consistent configuration across environments
4. Identifying any missing or redundant settings"
```

## Editing and Customization

### Custom File Operations
```javascript
// Create custom file operation scripts
const customFileOps = {
  // Bulk file processing
  processMarkdownFiles: async (directory) => {
    const files = await listDirectory(directory, { filter: '*.md' });
    for (const file of files) {
      const content = await readFile(file.path);
      const processedContent = processMarkdown(content);
      await writeFile(file.path, processedContent);
    }
  },

  // Template-based file creation
  createFromTemplate: async (templatePath, targetPath, variables) => {
    const template = await readFile(templatePath);
    const content = replaceVariables(template, variables);
    await writeFile(targetPath, content);
  },

  // Intelligent file organization
  organizeByType: async (sourceDir, targetDir) => {
    const files = await listDirectory(sourceDir, { recursive: true });
    const organized = groupFilesByType(files);
    
    for (const [type, fileList] of Object.entries(organized)) {
      const typeDir = `${targetDir}/${type}`;
      await createDirectory(typeDir);
      
      for (const file of fileList) {
        await moveFile(file.path, `${typeDir}/${file.name}`);
      }
    }
  }
};
```

### Configuration Customization
```json
{
  "filesystem": {
    "security": {
      "allowedPaths": ["/workspace", "/tmp", "/home/user/projects"],
      "blockedPaths": ["/etc", "/usr", "/bin", "/sbin"],
      "allowedExtensions": [".txt", ".md", ".js", ".ts", ".json", ".yaml"],
      "blockedExtensions": [".exe", ".bat", ".sh"],
      "maxFileSize": "100MB",
      "maxDirectoryDepth": 10
    },
    "performance": {
      "caching": {
        "enabled": true,
        "ttl": 300,
        "maxEntries": 1000
      },
      "concurrency": {
        "maxConcurrentOps": 10,
        "queueSize": 100
      },
      "optimization": {
        "enableCompression": true,
        "enableStreaming": true,
        "chunkSize": "64KB"
      }
    },
    "features": {
      "watchFiles": true,
      "enableSymlinks": true,
      "enableHiddenFiles": false,
      "enableBackups": true,
      "enableVersioning": false
    }
  }
}
```

### Advanced Scripting
```bash
#!/bin/bash
# Custom filesystem MCP management script

# Function to backup workspace
backup_workspace() {
    local workspace=$1
    local backup_dir="/backups/$(date +%Y%m%d_%H%M%S)"
    
    echo "Creating backup of $workspace to $backup_dir"
    mkdir -p "$backup_dir"
    cp -r "$workspace"/* "$backup_dir/"
    
    echo "Backup completed: $backup_dir"
}

# Function to clean temporary files
clean_temp_files() {
    local workspace=$1
    
    echo "Cleaning temporary files in $workspace"
    find "$workspace" -name "*.tmp" -delete
    find "$workspace" -name "*.log" -mtime +7 -delete
    find "$workspace" -name ".DS_Store" -delete
    
    echo "Cleanup completed"
}

# Function to validate file structure
validate_structure() {
    local workspace=$1
    local required_dirs=("src" "tests" "docs" "config")
    
    echo "Validating project structure in $workspace"
    for dir in "${required_dirs[@]}"; do
        if [ ! -d "$workspace/$dir" ]; then
            echo "Warning: Missing required directory: $dir"
        else
            echo "✓ Found: $dir"
        fi
    done
}

# Main execution
case "$1" in
    backup)
        backup_workspace "$2"
        ;;
    clean)
        clean_temp_files "$2"
        ;;
    validate)
        validate_structure "$2"
        ;;
    *)
        echo "Usage: $0 {backup|clean|validate} <workspace_path>"
        exit 1
        ;;
esac
```

## Advanced Features

### File Watching and Monitoring
```javascript
// Setup file watching
const fileWatcher = {
  watchDirectory: async (path, options = {}) => {
    const watcher = new FileWatcher(path, {
      recursive: options.recursive || true,
      ignoreHidden: options.ignoreHidden || true,
      debounce: options.debounce || 100
    });

    watcher.on('change', (event) => {
      console.log(`File ${event.type}: ${event.path}`);
      handleFileChange(event);
    });

    watcher.on('error', (error) => {
      console.error('File watcher error:', error);
    });

    return watcher;
  },

  handleFileChange: (event) => {
    switch (event.type) {
      case 'created':
        onFileCreated(event.path);
        break;
      case 'modified':
        onFileModified(event.path);
        break;
      case 'deleted':
        onFileDeleted(event.path);
        break;
    }
  }
};
```

### Intelligent File Analysis
```javascript
// Advanced file analysis capabilities
const fileAnalyzer = {
  analyzeCodebase: async (rootPath) => {
    const analysis = {
      totalFiles: 0,
      totalLines: 0,
      fileTypes: {},
      dependencies: new Set(),
      complexity: {},
      issues: []
    };

    const files = await listDirectory(rootPath, { recursive: true });
    
    for (const file of files) {
      if (isCodeFile(file.path)) {
        const content = await readFile(file.path);
        const fileAnalysis = analyzeFile(content, file.path);
        
        analysis.totalFiles++;
        analysis.totalLines += fileAnalysis.lines;
        analysis.fileTypes[file.extension] = (analysis.fileTypes[file.extension] || 0) + 1;
        
        fileAnalysis.dependencies.forEach(dep => analysis.dependencies.add(dep));
        analysis.complexity[file.path] = fileAnalysis.complexity;
        analysis.issues.push(...fileAnalysis.issues);
      }
    }

    return analysis;
  },

  generateReport: (analysis) => {
    return {
      summary: {
        totalFiles: analysis.totalFiles,
        totalLines: analysis.totalLines,
        averageComplexity: calculateAverageComplexity(analysis.complexity)
      },
      breakdown: {
        fileTypes: analysis.fileTypes,
        dependencies: Array.from(analysis.dependencies),
        topComplexFiles: getTopComplexFiles(analysis.complexity, 10)
      },
      recommendations: generateRecommendations(analysis)
    };
  }
};
```

### Backup and Versioning
```javascript
// Backup and versioning system
const backupSystem = {
  createBackup: async (sourcePath, backupPath) => {
    const timestamp = new Date().toISOString().replace(/[:.]/g, '-');
    const backupDir = `${backupPath}/backup-${timestamp}`;
    
    await createDirectory(backupDir);
    await copyDirectory(sourcePath, backupDir);
    
    const manifest = {
      timestamp,
      sourcePath,
      backupPath: backupDir,
      files: await getFileList(backupDir)
    };
    
    await writeFile(`${backupDir}/manifest.json`, JSON.stringify(manifest, null, 2));
    return manifest;
  },

  restoreBackup: async (backupPath, targetPath) => {
    const manifest = JSON.parse(await readFile(`${backupPath}/manifest.json`));
    
    // Verify backup integrity
    const isValid = await verifyBackup(backupPath, manifest);
    if (!isValid) {
      throw new Error('Backup integrity check failed');
    }
    
    // Restore files
    await copyDirectory(backupPath, targetPath, { exclude: ['manifest.json'] });
    
    return {
      restored: true,
      timestamp: manifest.timestamp,
      fileCount: manifest.files.length
    };
  },

  listBackups: async (backupPath) => {
    const backups = [];
    const dirs = await listDirectory(backupPath);
    
    for (const dir of dirs) {
      if (dir.name.startsWith('backup-')) {
        const manifestPath = `${dir.path}/manifest.json`;
        if (await fileExists(manifestPath)) {
          const manifest = JSON.parse(await readFile(manifestPath));
          backups.push({
            name: dir.name,
            timestamp: manifest.timestamp,
            path: dir.path,
            fileCount: manifest.files.length
          });
        }
      }
    }
    
    return backups.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
  }
};
```

## Troubleshooting

### Common Issues and Solutions

#### Installation Problems
```bash
# Issue: NPM installation fails with permission errors
# Solution:
sudo npm install -g @modelcontextprotocol/server-filesystem
# Or use nvm to manage Node.js versions without sudo

# Issue: Python installation conflicts
# Solution:
python -m venv mcp-env
source mcp-env/bin/activate
pip install mcp-server-filesystem

# Issue: Command not found after installation
# Solution:
which npx
echo $PATH
npm list -g @modelcontextprotocol/server-filesystem
```

#### Configuration Issues
```bash
# Issue: Claude Desktop doesn't recognize the MCP server
# Solution:
# 1. Check configuration file syntax
cat ~/.claude/claude_desktop_config.json | jq .

# 2. Verify file paths
ls -la /workspace

# 3. Test server manually
npx @modelcontextprotocol/server-filesystem /workspace --test

# 4. Check Claude Desktop logs
tail -f ~/.claude/logs/claude-desktop.log
```

#### Permission Problems
```bash
# Issue: Access denied errors
# Solution:
# 1. Check directory permissions
ls -la /workspace
chmod 755 /workspace

# 2. Verify user ownership
chown -R $USER:$USER /workspace

# 3. Check SELinux/AppArmor restrictions
getenforce  # For SELinux
aa-status   # For AppArmor

# 4. Test with read-only mode first
npx @modelcontextprotocol/server-filesystem /workspace --read-only
```

#### Performance Issues
```bash
# Issue: Slow file operations
# Solution:
# 1. Enable caching
export ENABLE_CACHE=true
export CACHE_TTL=300

# 2. Limit concurrent operations
export MAX_CONCURRENT_OPS=5

# 3. Use file system optimization
mount -o noatime /workspace

# 4. Monitor system resources
htop
iotop
df -h
```

### Diagnostic Commands
```bash
# System diagnostics
filesystem-mcp diagnose --workspace /workspace --verbose

# Performance testing
filesystem-mcp benchmark --operations 1000 --concurrent 5

# Configuration validation
filesystem-mcp validate-config --config ~/.claude/claude_desktop_config.json

# Health check
filesystem-mcp health-check --comprehensive

# Debug mode
DEBUG=filesystem-mcp:* npx @modelcontextprotocol/server-filesystem /workspace
```

### Log Analysis
```bash
# View MCP server logs
tail -f ~/.claude/logs/mcp-filesystem.log

# Analyze error patterns
grep -i error ~/.claude/logs/mcp-filesystem.log | tail -20

# Monitor file operations
grep -i "file operation" ~/.claude/logs/mcp-filesystem.log

# Performance metrics
grep -i "performance" ~/.claude/logs/mcp-filesystem.log | tail -10
```

## Security Considerations

### Access Control
```json
{
  "security": {
    "pathRestrictions": {
      "allowedPaths": [
        "/workspace",
        "/home/user/projects",
        "/tmp/mcp-workspace"
      ],
      "blockedPaths": [
        "/etc",
        "/usr",
        "/bin",
        "/sbin",
        "/root",
        "/home/user/.ssh"
      ],
      "pathValidation": "strict"
    },
    "fileRestrictions": {
      "allowedExtensions": [
        ".txt", ".md", ".json", ".yaml", ".yml",
        ".js", ".ts", ".jsx", ".tsx", ".py", ".java",
        ".html", ".css", ".scss", ".less"
      ],
      "blockedExtensions": [
        ".exe", ".bat", ".sh", ".ps1", ".cmd",
        ".dll", ".so", ".dylib"
      ],
      "maxFileSize": "100MB",
      "scanForMalware": true
    },
    "operationRestrictions": {
      "allowRead": true,
      "allowWrite": true,
      "allowDelete": false,
      "allowExecute": false,
      "allowSymlinks": false,
      "requireConfirmation": ["delete", "move", "chmod"]
    }
  }
}
```

### Audit Logging
```json
{
  "audit": {
    "enabled": true,
    "logLevel": "detailed",
    "logFile": "/var/log/mcp-filesystem-audit.log",
    "logRotation": {
      "enabled": true,
      "maxSize": "100MB",
      "maxFiles": 10
    },
    "events": {
      "fileRead": true,
      "fileWrite": true,
      "fileDelete": true,
      "directoryCreate": true,
      "permissionChange": true,
      "accessDenied": true
    },
    "alerting": {
      "enabled": true,
      "channels": ["email", "webhook"],
      "rules": [
        {
          "event": "accessDenied",
          "threshold": 5,
          "timeWindow": "5m",
          "action": "alert"
        },
        {
          "event": "fileDelete",
          "pattern": "*.important",
          "action": "alert"
        }
      ]
    }
  }
}
```

## Performance Optimization

### Caching Strategies
```javascript
// Multi-level caching system
const cachingSystem = {
  memoryCache: new Map(),
  diskCache: new DiskCache('/tmp/mcp-cache'),
  
  get: async (key) => {
    // Check memory cache first
    if (this.memoryCache.has(key)) {
      return this.memoryCache.get(key);
    }
    
    // Check disk cache
    const diskResult = await this.diskCache.get(key);
    if (diskResult) {
      // Promote to memory cache
      this.memoryCache.set(key, diskResult);
      return diskResult;
    }
    
    return null;
  },
  
  set: async (key, value, ttl = 300) => {
    // Store in memory cache
    this.memoryCache.set(key, value);
    
    // Store in disk cache for persistence
    await this.diskCache.set(key, value, ttl);
    
    // Implement LRU eviction for memory cache
    if (this.memoryCache.size > 1000) {
      const firstKey = this.memoryCache.keys().next().value;
      this.memoryCache.delete(firstKey);
    }
  }
};
```

### Batch Operations
```javascript
// Efficient batch processing
const batchProcessor = {
  processBatch: async (operations, batchSize = 10) => {
    const results = [];
    
    for (let i = 0; i < operations.length; i += batchSize) {
      const batch = operations.slice(i, i + batchSize);
      const batchResults = await Promise.all(
        batch.map(op => this.processOperation(op))
      );
      results.push(...batchResults);
      
      // Add small delay to prevent overwhelming the system
      if (i + batchSize < operations.length) {
        await new Promise(resolve => setTimeout(resolve, 10));
      }
    }
    
    return results;
  },
  
  processOperation: async (operation) => {
    try {
      switch (operation.type) {
        case 'read':
          return await readFile(operation.path);
        case 'write':
          return await writeFile(operation.path, operation.content);
        case 'delete':
          return await deleteFile(operation.path);
        default:
          throw new Error(`Unknown operation type: ${operation.type}`);
      }
    } catch (error) {
      return { error: error.message, operation };
    }
  }
};
```

## API Reference

### Core Functions
```typescript
interface FilesystemMCP {
  // File operations
  readFile(path: string, options?: ReadOptions): Promise<string>;
  writeFile(path: string, content: string, options?: WriteOptions): Promise<void>;
  appendFile(path: string, content: string, options?: WriteOptions): Promise<void>;
  deleteFile(path: string): Promise<void>;
  copyFile(source: string, destination: string): Promise<void>;
  moveFile(source: string, destination: string): Promise<void>;
  
  // Directory operations
  listDirectory(path: string, options?: ListOptions): Promise<FileInfo[]>;
  createDirectory(path: string, options?: CreateDirOptions): Promise<void>;
  deleteDirectory(path: string, recursive?: boolean): Promise<void>;
  
  // File information
  getFileInfo(path: string): Promise<FileInfo>;
  fileExists(path: string): Promise<boolean>;
  getFileStats(path: string): Promise<FileStats>;
  
  // Search operations
  searchFiles(pattern: string, path: string, options?: SearchOptions): Promise<FileInfo[]>;
  findFiles(pattern: string, path: string, options?: FindOptions): Promise<string[]>;
  
  // Advanced operations
  watchFile(path: string, callback: WatchCallback): Promise<FileWatcher>;
  createSymlink(target: string, path: string): Promise<void>;
  readSymlink(path: string): Promise<string>;
}

interface FileInfo {
  name: string;
  path: string;
  size: number;
  type: 'file' | 'directory' | 'symlink';
  permissions: string;
  owner: string;
  group: string;
  created: Date;
  modified: Date;
  accessed: Date;
}

interface ReadOptions {
  encoding?: string;
  startLine?: number;
  endLine?: number;
  maxSize?: number;
}

interface WriteOptions {
  encoding?: string;
  mode?: string;
  createDirectories?: boolean;
  backup?: boolean;
}

interface ListOptions {
  recursive?: boolean;
  includeHidden?: boolean;
  filter?: string;
  sortBy?: 'name' | 'size' | 'modified';
  sortOrder?: 'asc' | 'desc';
}
```

## Links and Resources

- [Official MCP Filesystem Server](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Node.js File System API](https://nodejs.org/api/fs.html)
- [Python pathlib Documentation](https://docs.python.org/3/library/pathlib.html)
- [File System Security Best Practices](https://owasp.org/www-community/vulnerabilities/Path_Traversal)

## Community and Support

- [MCP Community Discord](https://discord.gg/mcp)
- [GitHub Issues](https://github.com/modelcontextprotocol/servers/issues)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/model-context-protocol)
- [Reddit Community](https://reddit.com/r/ModelContextProtocol)
- [Documentation Wiki](https://github.com/modelcontextprotocol/servers/wiki)

