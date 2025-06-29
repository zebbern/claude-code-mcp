# Steipete's Claude Code MCP

## Overview
Steipete's Claude Code MCP is a powerful implementation that allows running Claude Code in one-shot mode with permissions bypassed automatically. This MCP server enables you to have "an agent in your agent" by providing Claude Code capabilities through the Model Context Protocol interface. It's particularly useful for integrating Claude Code's powerful software engineering capabilities into other AI workflows and applications.

## Installation

### Prerequisites
- Claude Code CLI installed and configured
- Node.js 18+ or Python 3.8+
- Claude Desktop application
- Understanding of MCP server configuration

### Install Steps

#### Option 1: NPM Installation
```bash
npm install -g @steipete/claude-code-mcp
```

#### Option 2: Direct from GitHub
```bash
git clone https://github.com/steipete/claude-code-mcp.git
cd claude-code-mcp
npm install
npm run build
```

#### Option 3: Using Claude Code MCP CLI
```bash
claude mcp add steipete/claude-code-mcp
```

#### Option 4: Docker Container
```bash
docker run -d --name steipete-claude-code-mcp \
  -v $(pwd):/workspace \
  -e ANTHROPIC_API_KEY=your-api-key \
  steipete/claude-code-mcp
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "claude-code": {
      "command": "npx",
      "args": [
        "@steipete/claude-code-mcp"
      ],
      "env": {
        "ANTHROPIC_API_KEY": "your-anthropic-api-key",
        "CLAUDE_CODE_PATH": "/path/to/claude-code",
        "WORKSPACE_PATH": "/path/to/workspace"
      }
    }
  }
}
```

### Advanced Configuration
```json
{
  "mcpServers": {
    "claude-code-advanced": {
      "command": "node",
      "args": [
        "/path/to/claude-code-mcp/dist/index.js",
        "--config", "/path/to/config.json"
      ],
      "env": {
        "ANTHROPIC_API_KEY": "your-anthropic-api-key",
        "CLAUDE_CODE_PATH": "/usr/local/bin/claude",
        "WORKSPACE_PATH": "/workspace",
        "AUTO_APPROVE": "true",
        "MAX_ITERATIONS": "10",
        "TIMEOUT": "300"
      }
    }
  }
}
```

### Configuration File (config.json)
```json
{
  "claudeCode": {
    "path": "/usr/local/bin/claude",
    "autoApprove": true,
    "maxIterations": 10,
    "timeout": 300,
    "workspacePath": "/workspace",
    "permissions": {
      "fileSystem": true,
      "network": false,
      "shell": true
    }
  },
  "mcp": {
    "serverName": "claude-code",
    "version": "1.0.0",
    "capabilities": {
      "tools": true,
      "resources": true,
      "prompts": false
    }
  },
  "security": {
    "sandboxMode": false,
    "allowedPaths": ["/workspace", "/tmp"],
    "blockedCommands": ["rm -rf", "sudo", "su"]
  }
}
```

## Usage Examples

### Basic Claude Code Execution
```
# Execute Claude Code commands through MCP
Execute a Claude Code command to analyze the current codebase and suggest improvements.

# One-shot code generation
Generate a complete Python script for data analysis using Claude Code's capabilities.

# Automated code review
Run Claude Code to review recent commits and provide feedback on code quality.

# Project scaffolding
Use Claude Code to create a new project structure with best practices.

# Bug fixing workflow
Analyze error logs and use Claude Code to identify and fix bugs automatically.
```

### Advanced Workflows
```
# Multi-step development workflow
1. Analyze requirements using Claude Code
2. Generate initial code structure
3. Implement core functionality
4. Add tests and documentation
5. Optimize and refactor code

# Continuous integration integration
Integrate with CI/CD pipelines to run Claude Code analysis on every commit.

# Code migration assistance
Use Claude Code to help migrate legacy code to modern frameworks.

# Documentation generation
Automatically generate comprehensive documentation for existing codebases.

# Performance optimization
Analyze code performance and implement optimizations using Claude Code.
```

### Integration Patterns
```
# With other MCP servers
Combine with filesystem MCP for enhanced file operations.
Integrate with Git MCP for version control workflows.
Use with database MCPs for data-driven development.

# In development environments
Integrate with VS Code through MCP extensions.
Use in Cursor for enhanced AI-powered development.
Combine with other AI coding assistants.

# For team workflows
Set up shared Claude Code instances for team collaboration.
Implement code review workflows with automated feedback.
Create standardized development processes.
```

## Features

### Core Capabilities
- **One-Shot Execution**: Run Claude Code commands without manual approval
- **Permission Bypass**: Automatically handle permission prompts
- **Workspace Management**: Manage multiple workspaces and projects
- **Error Handling**: Robust error handling and recovery mechanisms
- **Logging**: Comprehensive logging of all Claude Code operations

### Advanced Features
- **Batch Processing**: Execute multiple Claude Code commands in sequence
- **Template Support**: Use predefined templates for common tasks
- **Custom Workflows**: Define custom workflows for specific development patterns
- **Integration APIs**: RESTful APIs for external system integration
- **Monitoring**: Real-time monitoring of Claude Code execution

### Security Features
- **Sandbox Mode**: Optional sandboxed execution environment
- **Path Restrictions**: Limit file system access to specific directories
- **Command Filtering**: Block potentially dangerous commands
- **Audit Logging**: Complete audit trail of all operations
- **Permission Management**: Fine-grained permission control

### Performance Optimizations
- **Caching**: Cache Claude Code responses for faster execution
- **Parallel Execution**: Run multiple Claude Code instances in parallel
- **Resource Management**: Efficient resource usage and cleanup
- **Timeout Handling**: Configurable timeouts for long-running operations
- **Memory Optimization**: Optimized memory usage for large codebases

## Requirements

### System Requirements
- **Operating System**: macOS 10.15+, Linux, Windows 10+ (with WSL)
- **Node.js**: 18.0 or higher
- **Memory**: 4GB RAM minimum, 8GB+ recommended
- **Storage**: 2GB+ available space
- **Network**: Internet connection for Claude API access

### Claude Code Requirements
- Claude Code CLI installed and configured
- Valid Anthropic API key with sufficient credits
- Proper authentication setup
- Understanding of Claude Code capabilities and limitations

### Dependencies
```json
{
  "dependencies": {
    "@anthropic-ai/sdk": "^0.24.0",
    "@modelcontextprotocol/sdk": "^0.5.0",
    "commander": "^11.0.0",
    "dotenv": "^16.0.0",
    "winston": "^3.10.0"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "typescript": "^5.0.0",
    "jest": "^29.0.0",
    "eslint": "^8.0.0"
  }
}
```

## Security Considerations

### Best Practices
- **API Key Security**: Store API keys securely using environment variables
- **Workspace Isolation**: Use separate workspaces for different projects
- **Permission Management**: Carefully configure file system and command permissions
- **Audit Logging**: Enable comprehensive logging for security monitoring
- **Regular Updates**: Keep the MCP server updated to latest version

### Security Configuration
```json
{
  "security": {
    "apiKey": {
      "source": "environment",
      "validation": "required",
      "rotation": "90d"
    },
    "fileSystem": {
      "allowedPaths": ["/workspace", "/tmp"],
      "blockedPaths": ["/etc", "/usr", "/bin"],
      "permissions": "read-write"
    },
    "commands": {
      "allowList": ["git", "npm", "python", "node"],
      "blockList": ["rm -rf", "sudo", "su", "chmod 777"],
      "validation": "strict"
    },
    "network": {
      "allowOutbound": true,
      "allowInbound": false,
      "blockedDomains": ["malicious-site.com"]
    }
  }
}
```

### Compliance Features
```json
{
  "compliance": {
    "auditLogging": {
      "enabled": true,
      "level": "detailed",
      "retention": "90d",
      "encryption": "AES-256"
    },
    "dataProtection": {
      "encryptionAtRest": true,
      "encryptionInTransit": true,
      "dataMinimization": true,
      "rightToErasure": true
    },
    "accessControl": {
      "authentication": "required",
      "authorization": "role-based",
      "sessionTimeout": "1h",
      "multiFactorAuth": "optional"
    }
  }
}
```

## Troubleshooting

### Common Issues

#### Installation Problems
**Problem**: NPM installation fails
**Solution**:
```bash
# Clear npm cache
npm cache clean --force

# Install with verbose logging
npm install -g @steipete/claude-code-mcp --verbose

# Use alternative registry
npm install -g @steipete/claude-code-mcp --registry https://registry.npmjs.org/
```

#### Configuration Issues
**Problem**: MCP server not starting
**Solution**:
```bash
# Check Claude Code installation
claude --version

# Verify API key
echo $ANTHROPIC_API_KEY

# Test MCP server manually
npx @steipete/claude-code-mcp --test

# Check logs
tail -f ~/.claude/logs/mcp-server.log
```

#### Permission Problems
**Problem**: Claude Code commands failing due to permissions
**Solution**:
- Enable auto-approve mode in configuration
- Check workspace path permissions
- Verify API key has sufficient credits
- Review security settings and allowed paths

#### Performance Issues
**Problem**: Slow Claude Code execution
**Solution**:
```json
{
  "performance": {
    "caching": {
      "enabled": true,
      "ttl": 3600,
      "maxSize": "100MB"
    },
    "parallelExecution": {
      "enabled": true,
      "maxConcurrent": 3
    },
    "optimization": {
      "memoryLimit": "2GB",
      "timeoutMs": 30000,
      "retryAttempts": 3
    }
  }
}
```

### Diagnostic Commands
```bash
# Health check
npx @steipete/claude-code-mcp --health

# Configuration validation
npx @steipete/claude-code-mcp --validate-config

# Performance test
npx @steipete/claude-code-mcp --benchmark

# Debug mode
DEBUG=* npx @steipete/claude-code-mcp
```

## Advanced Configuration

### Custom Workflows
```json
{
  "workflows": {
    "codeReview": {
      "steps": [
        "analyze-changes",
        "check-style",
        "run-tests",
        "generate-report"
      ],
      "autoApprove": false,
      "notifications": true
    },
    "bugFix": {
      "steps": [
        "analyze-error",
        "identify-root-cause",
        "generate-fix",
        "test-fix",
        "apply-fix"
      ],
      "autoApprove": true,
      "rollbackOnFailure": true
    }
  }
}
```

### Integration Examples
```javascript
// Custom MCP client integration
const { MCPClient } = require('@modelcontextprotocol/sdk');

class ClaudeCodeIntegration {
  constructor(config) {
    this.client = new MCPClient(config);
    this.claudeCode = new ClaudeCodeMCP(config.claudeCode);
  }

  async executeWorkflow(workflow, params) {
    try {
      const result = await this.claudeCode.execute(workflow, params);
      return this.processResult(result);
    } catch (error) {
      return this.handleError(error);
    }
  }

  async processResult(result) {
    // Process Claude Code execution result
    return {
      success: true,
      output: result.output,
      files: result.modifiedFiles,
      metrics: result.performance
    };
  }
}
```

### Monitoring and Analytics
```json
{
  "monitoring": {
    "metrics": {
      "enabled": true,
      "endpoint": "http://localhost:9090/metrics",
      "interval": "30s"
    },
    "alerts": {
      "errorRate": {
        "threshold": 0.05,
        "action": "notify"
      },
      "responseTime": {
        "threshold": "30s",
        "action": "scale"
      }
    },
    "logging": {
      "level": "info",
      "format": "json",
      "destination": "file"
    }
  }
}
```

## API Reference

### Core Methods
```typescript
interface ClaudeCodeMCP {
  execute(command: string, options?: ExecuteOptions): Promise<ExecuteResult>;
  analyze(path: string, options?: AnalyzeOptions): Promise<AnalyzeResult>;
  generate(prompt: string, options?: GenerateOptions): Promise<GenerateResult>;
  review(files: string[], options?: ReviewOptions): Promise<ReviewResult>;
  optimize(target: string, options?: OptimizeOptions): Promise<OptimizeResult>;
}

interface ExecuteOptions {
  workspace?: string;
  timeout?: number;
  autoApprove?: boolean;
  dryRun?: boolean;
}

interface ExecuteResult {
  success: boolean;
  output: string;
  files: ModifiedFile[];
  metrics: PerformanceMetrics;
  errors?: Error[];
}
```

### Event Handlers
```typescript
interface EventHandlers {
  onStart?: (context: ExecutionContext) => void;
  onProgress?: (progress: ProgressUpdate) => void;
  onComplete?: (result: ExecuteResult) => void;
  onError?: (error: Error) => void;
  onFileChange?: (file: FileChange) => void;
}
```

## Links

- [GitHub Repository](https://github.com/steipete/claude-code-mcp)
- [NPM Package](https://www.npmjs.com/package/@steipete/claude-code-mcp)
- [Smithery Listing](https://smithery.ai/server/@steipete/claude-code-mcp)
- [Documentation](https://github.com/steipete/claude-code-mcp/blob/main/README.md)
- [Issues](https://github.com/steipete/claude-code-mcp/issues)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)

## Community Resources

- [Claude Code Discord](https://discord.gg/claude-code)
- [MCP Community](https://github.com/modelcontextprotocol/community)
- [Anthropic Developer Forum](https://community.anthropic.com/)
- [Claude Code Examples](https://github.com/anthropics/claude-code-examples)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [Best Practices Guide](https://docs.anthropic.com/en/docs/claude-code/best-practices)

