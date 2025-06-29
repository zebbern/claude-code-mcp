# Claude-Flow AI Agent MCP

## Overview
Claude-Flow is an advanced AI agent orchestration platform that integrates seamlessly with Claude Code to create powerful multi-agent workflows. This MCP enables you to build sophisticated AI agent teams that can collaborate with Claude Code to handle complex software development tasks, automate workflows, and create intelligent development pipelines.

## What is Claude-Flow?
Claude-Flow is a cutting-edge platform that allows you to:
- **Orchestrate Multiple AI Agents**: Create teams of specialized AI agents that work together
- **Integrate with Claude Code**: Seamlessly connect with Claude Code for enhanced development capabilities
- **Automate Complex Workflows**: Build sophisticated automation pipelines
- **Manage Agent Coordination**: Handle complex inter-agent communication and task delegation
- **Scale Development Operations**: Scale your development processes with intelligent automation

## Installation

### Prerequisites
- Claude Code CLI installed and configured
- Node.js 18+ or Python 3.9+
- Claude Desktop application
- Valid Anthropic API key
- Docker (optional, for containerized deployment)
- Understanding of AI agent concepts

### Step 1: Install Claude-Flow
```bash
# Option 1: NPM Installation
npm install -g claude-flow-mcp

# Option 2: Python Installation
pip install claude-flow-mcp

# Option 3: Direct from GitHub
git clone https://github.com/claude-flow/claude-flow-mcp.git
cd claude-flow-mcp
npm install
npm run build

# Option 4: Docker Installation
docker pull claude-flow/mcp-server:latest
```

### Step 2: Install Dependencies
```bash
# Install required dependencies
npm install @anthropic-ai/sdk @modelcontextprotocol/sdk
pip install anthropic mcp-sdk

# Install optional dependencies for enhanced features
npm install redis ioredis bull
pip install redis celery
```

### Step 3: Configure Environment
```bash
# Create environment file
cat > .env << EOF
ANTHROPIC_API_KEY=your-anthropic-api-key
CLAUDE_CODE_PATH=/usr/local/bin/claude
CLAUDE_FLOW_PORT=3001
REDIS_URL=redis://localhost:6379
WORKSPACE_ROOT=/workspace
LOG_LEVEL=info
MAX_AGENTS=10
AGENT_TIMEOUT=300000
EOF

# Set environment variables
export ANTHROPIC_API_KEY=your-anthropic-api-key
export CLAUDE_CODE_PATH=/usr/local/bin/claude
export CLAUDE_FLOW_PORT=3001
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "claude-flow": {
      "command": "npx",
      "args": [
        "claude-flow-mcp",
        "--port", "3001",
        "--workspace", "/workspace"
      ],
      "env": {
        "ANTHROPIC_API_KEY": "your-anthropic-api-key",
        "CLAUDE_CODE_PATH": "/usr/local/bin/claude",
        "REDIS_URL": "redis://localhost:6379",
        "MAX_AGENTS": "10",
        "AGENT_TIMEOUT": "300000"
      }
    }
  }
}
```

### Advanced Configuration File (claude-flow-config.json)
```json
{
  "server": {
    "name": "claude-flow-mcp",
    "version": "2.0.0",
    "port": 3001,
    "host": "0.0.0.0",
    "cors": {
      "enabled": true,
      "origins": ["*"]
    }
  },
  "claudeCode": {
    "executable": "/usr/local/bin/claude",
    "workspaceRoot": "/workspace",
    "defaultModel": "claude-3-5-sonnet-20241022",
    "maxTokens": 8192,
    "temperature": 0.1,
    "integration": {
      "enabled": true,
      "autoStart": true,
      "sharedContext": true
    }
  },
  "agents": {
    "maxConcurrent": 10,
    "defaultTimeout": 300000,
    "retryAttempts": 3,
    "coordination": {
      "enabled": true,
      "strategy": "hierarchical",
      "communicationProtocol": "message-passing"
    },
    "specializations": [
      "code-reviewer",
      "test-generator",
      "documentation-writer",
      "bug-fixer",
      "performance-optimizer",
      "security-auditor"
    ]
  },
  "workflows": {
    "enabled": true,
    "storage": "redis",
    "persistence": true,
    "scheduling": {
      "enabled": true,
      "engine": "bull"
    }
  },
  "security": {
    "authentication": {
      "enabled": true,
      "method": "api-key"
    },
    "authorization": {
      "enabled": true,
      "rbac": true
    },
    "sandboxing": {
      "enabled": true,
      "containerized": false
    }
  }
}
```

### Agent Configuration Templates
```json
{
  "agentTemplates": {
    "codeReviewer": {
      "name": "Code Reviewer Agent",
      "description": "Specialized in code review and quality analysis",
      "capabilities": [
        "code-analysis",
        "style-checking",
        "security-scanning",
        "performance-analysis"
      ],
      "claudeCodeIntegration": {
        "enabled": true,
        "sharedWorkspace": true,
        "commandAccess": ["analyze", "review", "suggest"]
      },
      "configuration": {
        "model": "claude-3-5-sonnet-20241022",
        "temperature": 0.1,
        "maxTokens": 4096,
        "systemPrompt": "You are a senior code reviewer..."
      }
    },
    "testGenerator": {
      "name": "Test Generator Agent",
      "description": "Specialized in generating comprehensive test suites",
      "capabilities": [
        "unit-test-generation",
        "integration-test-creation",
        "e2e-test-design",
        "test-data-generation"
      ],
      "claudeCodeIntegration": {
        "enabled": true,
        "sharedWorkspace": true,
        "commandAccess": ["generate", "test", "validate"]
      },
      "configuration": {
        "model": "claude-3-5-sonnet-20241022",
        "temperature": 0.2,
        "maxTokens": 6144,
        "systemPrompt": "You are a test automation expert..."
      }
    }
  }
}
```

## Commands and Usage

### Basic Commands
```bash
# Start Claude-Flow MCP Server
claude-flow start --config claude-flow-config.json

# Start with Claude Code integration
claude-flow start --claude-code --workspace /workspace

# Start with specific agents
claude-flow start --agents code-reviewer,test-generator,documentation-writer

# Start in development mode
claude-flow dev --watch --debug

# Check server status
claude-flow status

# List available agents
claude-flow agents list

# Create new agent
claude-flow agents create --template code-reviewer --name my-reviewer

# Deploy agent workflow
claude-flow workflows deploy --file workflow.json

# Monitor agent performance
claude-flow monitor --real-time
```

### Advanced Commands
```bash
# Cluster management
claude-flow cluster start --nodes 3
claude-flow cluster scale --agents 20
claude-flow cluster status

# Workflow management
claude-flow workflows create --name "full-stack-dev" --template advanced
claude-flow workflows start --name "full-stack-dev" --input project.json
claude-flow workflows pause --id workflow-123
claude-flow workflows resume --id workflow-123
claude-flow workflows stop --id workflow-123

# Agent coordination
claude-flow coordination setup --strategy hierarchical
claude-flow coordination assign --agent code-reviewer --task review-pr-123
claude-flow coordination status --verbose

# Integration commands
claude-flow integrate claude-code --workspace /workspace --shared-context
claude-flow integrate git --repo https://github.com/user/repo.git
claude-flow integrate ci-cd --platform github-actions

# Monitoring and debugging
claude-flow logs --agent code-reviewer --tail 100
claude-flow debug --agent test-generator --verbose
claude-flow metrics --export prometheus
claude-flow health-check --comprehensive
```

### Claude Code Integration Commands
```bash
# Initialize Claude Code integration
claude-flow claude-code init --workspace /workspace

# Execute Claude Code through agent
claude-flow claude-code execute --command "analyze codebase" --agent code-reviewer

# Share context between Claude Code and agents
claude-flow claude-code share-context --agents all

# Coordinate Claude Code with agent workflow
claude-flow claude-code coordinate --workflow full-stack-dev

# Monitor Claude Code integration
claude-flow claude-code monitor --real-time
```

## Usage Examples

### Basic Agent Workflow
```javascript
// Create a simple code review workflow
const workflow = {
  name: "code-review-workflow",
  description: "Automated code review with Claude Code integration",
  steps: [
    {
      agent: "code-reviewer",
      task: "analyze-code",
      claudeCodeIntegration: true,
      input: {
        files: ["src/**/*.js", "src/**/*.ts"],
        criteria: ["style", "security", "performance"]
      }
    },
    {
      agent: "test-generator",
      task: "generate-tests",
      dependsOn: ["analyze-code"],
      input: {
        coverage: 90,
        types: ["unit", "integration"]
      }
    },
    {
      agent: "documentation-writer",
      task: "update-docs",
      dependsOn: ["analyze-code"],
      input: {
        format: "markdown",
        includeExamples: true
      }
    }
  ]
};

// Deploy and execute workflow
await claudeFlow.workflows.deploy(workflow);
await claudeFlow.workflows.execute("code-review-workflow", {
  repository: "/workspace/my-project",
  branch: "feature/new-feature"
});
```

### Advanced Multi-Agent Coordination
```javascript
// Complex development workflow with Claude Code
const advancedWorkflow = {
  name: "full-stack-development",
  description: "Complete full-stack development with AI agents and Claude Code",
  agents: {
    architect: {
      type: "system-architect",
      claudeCodeIntegration: true,
      responsibilities: ["system-design", "architecture-planning"]
    },
    backendDev: {
      type: "backend-developer",
      claudeCodeIntegration: true,
      responsibilities: ["api-development", "database-design"]
    },
    frontendDev: {
      type: "frontend-developer",
      claudeCodeIntegration: true,
      responsibilities: ["ui-development", "component-creation"]
    },
    tester: {
      type: "test-engineer",
      claudeCodeIntegration: true,
      responsibilities: ["test-automation", "quality-assurance"]
    },
    devops: {
      type: "devops-engineer",
      claudeCodeIntegration: true,
      responsibilities: ["deployment", "monitoring"]
    }
  },
  coordination: {
    strategy: "hierarchical",
    lead: "architect",
    communication: "event-driven",
    synchronization: "checkpoint-based"
  },
  phases: [
    {
      name: "planning",
      agents: ["architect"],
      claudeCodeTasks: ["analyze-requirements", "design-architecture"],
      deliverables: ["system-design", "technical-specs"]
    },
    {
      name: "development",
      agents: ["backendDev", "frontendDev"],
      parallel: true,
      claudeCodeTasks: ["implement-backend", "create-frontend"],
      deliverables: ["api-endpoints", "ui-components"]
    },
    {
      name: "testing",
      agents: ["tester"],
      claudeCodeTasks: ["generate-tests", "run-automation"],
      deliverables: ["test-suite", "quality-report"]
    },
    {
      name: "deployment",
      agents: ["devops"],
      claudeCodeTasks: ["setup-ci-cd", "deploy-application"],
      deliverables: ["deployment-pipeline", "monitoring-setup"]
    }
  ]
};
```

### Real-time Agent Monitoring
```javascript
// Monitor agent performance and Claude Code integration
const monitoring = {
  agents: {
    performance: {
      metrics: ["response-time", "success-rate", "resource-usage"],
      alerts: {
        slowResponse: { threshold: "30s", action: "notify" },
        highFailure: { threshold: "5%", action: "restart" }
      }
    },
    claudeCodeIntegration: {
      metrics: ["api-calls", "token-usage", "error-rate"],
      optimization: {
        caching: true,
        batching: true,
        rateLimiting: true
      }
    }
  },
  workflows: {
    tracking: {
      enabled: true,
      granularity: "step-level",
      persistence: "database"
    },
    analytics: {
      enabled: true,
      dashboards: ["performance", "costs", "quality"],
      reporting: "daily"
    }
  }
};
```

## Editing and Customization

### Creating Custom Agents
```javascript
// Custom agent template
class CustomClaudeCodeAgent {
  constructor(config) {
    this.name = config.name;
    this.capabilities = config.capabilities;
    this.claudeCodeIntegration = config.claudeCodeIntegration;
  }

  async initialize() {
    // Initialize Claude Code connection
    this.claudeCode = new ClaudeCodeClient({
      apiKey: process.env.ANTHROPIC_API_KEY,
      workspace: this.claudeCodeIntegration.workspace
    });

    // Setup agent-specific configurations
    await this.setupCapabilities();
    await this.registerWithOrchestrator();
  }

  async executeTask(task) {
    try {
      // Pre-process task
      const processedTask = await this.preprocessTask(task);
      
      // Execute with Claude Code if needed
      let result;
      if (task.requiresClaudeCode) {
        result = await this.executeWithClaudeCode(processedTask);
      } else {
        result = await this.executeStandalone(processedTask);
      }

      // Post-process result
      return await this.postprocessResult(result);
    } catch (error) {
      return this.handleError(error);
    }
  }

  async executeWithClaudeCode(task) {
    // Coordinate with Claude Code
    const claudeCodeResult = await this.claudeCode.execute({
      command: task.claudeCodeCommand,
      parameters: task.parameters,
      workspace: task.workspace
    });

    // Process Claude Code result
    return this.processClaudeCodeResult(claudeCodeResult);
  }
}
```

### Workflow Customization
```json
{
  "customWorkflows": {
    "aiPairProgramming": {
      "name": "AI Pair Programming",
      "description": "Collaborative programming with AI agents and Claude Code",
      "configuration": {
        "realTime": true,
        "interactive": true,
        "claudeCodeIntegration": "deep"
      },
      "agents": [
        {
          "role": "senior-developer",
          "claudeCodeAccess": "full",
          "responsibilities": ["architecture", "complex-logic"]
        },
        {
          "role": "code-reviewer",
          "claudeCodeAccess": "read-write",
          "responsibilities": ["quality-check", "optimization"]
        },
        {
          "role": "test-specialist",
          "claudeCodeAccess": "read-write",
          "responsibilities": ["test-generation", "validation"]
        }
      ],
      "interaction": {
        "mode": "collaborative",
        "turnTaking": "intelligent",
        "conflictResolution": "consensus"
      }
    }
  }
}
```

### Configuration Editing
```bash
# Edit agent configurations
claude-flow config edit --agent code-reviewer
claude-flow config edit --workflow full-stack-dev
claude-flow config edit --integration claude-code

# Validate configurations
claude-flow config validate --all
claude-flow config validate --agent code-reviewer

# Backup and restore configurations
claude-flow config backup --output backup.json
claude-flow config restore --input backup.json

# Template management
claude-flow templates create --name custom-agent --base code-reviewer
claude-flow templates edit --name custom-agent
claude-flow templates deploy --name custom-agent
```

## Advanced Features

### Claude Code Deep Integration
```javascript
// Deep integration configuration
const deepIntegration = {
  claudeCode: {
    sharedContext: {
      enabled: true,
      synchronization: "real-time",
      contextWindow: 32000,
      persistence: "session-based"
    },
    commandSharing: {
      enabled: true,
      agentAccess: {
        "code-reviewer": ["analyze", "review", "suggest"],
        "test-generator": ["generate", "test", "validate"],
        "documentation-writer": ["document", "explain", "format"]
      }
    },
    workspaceSharing: {
      enabled: true,
      isolation: "namespace-based",
      permissions: "role-based"
    },
    resultAggregation: {
      enabled: true,
      strategy: "intelligent-merge",
      conflictResolution: "claude-code-priority"
    }
  }
};
```

### Scalability and Performance
```json
{
  "scalability": {
    "horizontal": {
      "enabled": true,
      "maxNodes": 10,
      "autoScaling": {
        "enabled": true,
        "metrics": ["cpu", "memory", "queue-length"],
        "thresholds": {
          "scaleUp": { "cpu": 80, "memory": 85, "queueLength": 100 },
          "scaleDown": { "cpu": 30, "memory": 40, "queueLength": 10 }
        }
      }
    },
    "vertical": {
      "enabled": true,
      "resourceLimits": {
        "memory": "8GB",
        "cpu": "4 cores",
        "storage": "100GB"
      }
    },
    "loadBalancing": {
      "enabled": true,
      "strategy": "round-robin",
      "healthChecks": true
    }
  },
  "performance": {
    "caching": {
      "enabled": true,
      "strategy": "multi-level",
      "ttl": 3600,
      "maxSize": "1GB"
    },
    "optimization": {
      "claudeCodeCalls": {
        "batching": true,
        "deduplication": true,
        "compression": true
      },
      "agentCommunication": {
        "protocol": "grpc",
        "compression": "gzip",
        "keepAlive": true
      }
    }
  }
}
```

## Troubleshooting

### Common Issues and Solutions

#### Installation Issues
```bash
# Issue: NPM installation fails
# Solution:
npm cache clean --force
npm install -g claude-flow-mcp --verbose

# Issue: Python dependencies conflict
# Solution:
python -m venv claude-flow-env
source claude-flow-env/bin/activate
pip install claude-flow-mcp

# Issue: Docker container won't start
# Solution:
docker logs claude-flow-mcp
docker run -it --entrypoint /bin/bash claude-flow/mcp-server:latest
```

#### Configuration Issues
```bash
# Issue: Claude Code integration not working
# Solution:
claude-flow claude-code test-connection
claude-flow config validate --integration claude-code

# Issue: Agents not starting
# Solution:
claude-flow agents diagnose --all
claude-flow logs --agent-startup --verbose

# Issue: Workflow execution fails
# Solution:
claude-flow workflows validate --name workflow-name
claude-flow workflows debug --id workflow-id
```

#### Performance Issues
```bash
# Issue: Slow agent response
# Solution:
claude-flow monitor --performance --real-time
claude-flow optimize --agents --parallel-execution

# Issue: High memory usage
# Solution:
claude-flow config edit --memory-limits
claude-flow garbage-collect --force

# Issue: Claude Code API rate limiting
# Solution:
claude-flow config edit --rate-limiting
claude-flow cache optimize --claude-code-calls
```

### Diagnostic Commands
```bash
# Comprehensive health check
claude-flow health-check --comprehensive --output health-report.json

# Performance analysis
claude-flow analyze performance --duration 1h --export metrics.json

# Integration testing
claude-flow test integration --claude-code --agents --workflows

# Debug mode
DEBUG=claude-flow:* claude-flow start --debug

# Log analysis
claude-flow logs analyze --pattern error --last 24h
```

## API Reference

### Core API Endpoints
```typescript
interface ClaudeFlowAPI {
  // Agent management
  POST /agents: CreateAgentRequest;
  GET /agents: ListAgentsResponse;
  GET /agents/{id}: GetAgentResponse;
  PUT /agents/{id}: UpdateAgentRequest;
  DELETE /agents/{id}: DeleteAgentResponse;

  // Workflow management
  POST /workflows: CreateWorkflowRequest;
  GET /workflows: ListWorkflowsResponse;
  POST /workflows/{id}/execute: ExecuteWorkflowRequest;
  GET /workflows/{id}/status: WorkflowStatusResponse;

  // Claude Code integration
  POST /claude-code/execute: ClaudeCodeExecuteRequest;
  GET /claude-code/status: ClaudeCodeStatusResponse;
  POST /claude-code/share-context: ShareContextRequest;

  // Monitoring
  GET /metrics: MetricsResponse;
  GET /health: HealthResponse;
  GET /logs: LogsResponse;
}
```

### WebSocket Events
```typescript
interface WebSocketEvents {
  // Agent events
  'agent-started': AgentStartedEvent;
  'agent-stopped': AgentStoppedEvent;
  'agent-error': AgentErrorEvent;
  'agent-task-completed': TaskCompletedEvent;

  // Workflow events
  'workflow-started': WorkflowStartedEvent;
  'workflow-step-completed': StepCompletedEvent;
  'workflow-completed': WorkflowCompletedEvent;
  'workflow-failed': WorkflowFailedEvent;

  // Claude Code events
  'claude-code-command-executed': CommandExecutedEvent;
  'claude-code-context-shared': ContextSharedEvent;
  'claude-code-integration-status': IntegrationStatusEvent;
}
```

## Security Considerations

### Authentication and Authorization
```json
{
  "security": {
    "authentication": {
      "methods": ["api-key", "oauth2", "jwt"],
      "apiKey": {
        "header": "X-API-Key",
        "validation": "strict",
        "rotation": "90d"
      },
      "oauth2": {
        "provider": "anthropic",
        "scopes": ["claude-code", "agents", "workflows"]
      }
    },
    "authorization": {
      "rbac": {
        "enabled": true,
        "roles": ["admin", "developer", "viewer"],
        "permissions": {
          "admin": ["*"],
          "developer": ["agents:*", "workflows:*", "claude-code:execute"],
          "viewer": ["agents:read", "workflows:read", "metrics:read"]
        }
      }
    },
    "dataProtection": {
      "encryption": {
        "atRest": "AES-256",
        "inTransit": "TLS-1.3"
      },
      "dataMinimization": true,
      "retention": "90d"
    }
  }
}
```

## Links and Resources

- [GitHub Repository](https://github.com/claude-flow/claude-flow-mcp)
- [Documentation](https://docs.claude-flow.ai/)
- [API Reference](https://api.claude-flow.ai/docs)
- [Community Discord](https://discord.gg/claude-flow)
- [Examples Repository](https://github.com/claude-flow/examples)
- [Claude Code Integration Guide](https://docs.claude-flow.ai/claude-code)
- [Agent Development Guide](https://docs.claude-flow.ai/agents)
- [Workflow Templates](https://templates.claude-flow.ai/)

## Community and Support

- [Discord Community](https://discord.gg/claude-flow)
- [GitHub Discussions](https://github.com/claude-flow/claude-flow-mcp/discussions)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/claude-flow)
- [Reddit Community](https://reddit.com/r/ClaudeFlow)
- [YouTube Channel](https://youtube.com/c/ClaudeFlow)
- [Blog](https://blog.claude-flow.ai/)
- [Newsletter](https://newsletter.claude-flow.ai/)
- [Support Portal](https://support.claude-flow.ai/)

