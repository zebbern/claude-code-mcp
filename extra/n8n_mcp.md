# n8n MCP

## Overview
The n8n MCP provides Claude with comprehensive workflow automation capabilities, enabling the creation, management, and execution of complex automation workflows. This MCP bridges Claude with n8n's powerful workflow automation platform, allowing for sophisticated integration between AI and business process automation.

## Installation

### Prerequisites
- n8n instance running and accessible
- n8n API credentials or webhook access
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Network access to n8n instance

### Install Steps

#### Option 1: Official n8n MCP Node
```bash
npm install n8n-nodes-mcp
```

#### Option 2: Via n8n Community
```bash
n8n install n8n-nodes-mcp
```

#### Option 3: From GitHub
```bash
git clone https://github.com/nerding-io/n8n-nodes-mcp.git
cd n8n-nodes-mcp
npm install
npm run build
```

#### Option 4: Custom MCP Server
```bash
git clone https://github.com/salacoste/mcp-n8n-workflow-builder.git
cd mcp-n8n-workflow-builder
npm install
npm run build
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "n8n": {
      "command": "npx",
      "args": [
        "n8n-mcp-server",
        "--n8n-url", "http://localhost:5678",
        "--api-key", "your-n8n-api-key"
      ]
    }
  }
}
```

### With n8n Cloud
```json
{
  "mcpServers": {
    "n8n": {
      "command": "npx",
      "args": [
        "n8n-mcp-server",
        "--n8n-url", "https://your-instance.app.n8n.cloud",
        "--api-key", "${N8N_API_KEY}"
      ]
    }
  }
}
```

### Self-hosted n8n Configuration
```json
{
  "mcpServers": {
    "n8n": {
      "command": "npx",
      "args": [
        "n8n-mcp-server",
        "--n8n-url", "https://n8n.yourdomain.com",
        "--username", "admin",
        "--password", "${N8N_PASSWORD}"
      ]
    }
  }
}
```

### Environment Variables
```bash
export N8N_URL=http://localhost:5678
export N8N_API_KEY=your-api-key
export N8N_WEBHOOK_URL=https://your-webhook-url.com
export N8N_ENCRYPTION_KEY=your-encryption-key
```

## Usage Examples

### Workflow Management
```
# List workflows
Show me all active workflows in my n8n instance.

# Create workflow
Create a new workflow that monitors my email and creates tasks in Notion.

# Execute workflow
Run the "Data Backup" workflow manually.

# Update workflow
Modify the "Lead Processing" workflow to include Slack notifications.

# Delete workflow
Remove the outdated "Old Integration" workflow.
```

### Workflow Creation
```
# Email automation
Create a workflow that processes incoming emails and categorizes them automatically.

# Data synchronization
Build a workflow that syncs customer data between CRM and marketing tools.

# Social media automation
Create a workflow that posts content across multiple social media platforms.

# File processing
Build a workflow that processes uploaded files and extracts metadata.

# API integration
Create a workflow that connects multiple APIs for data transformation.
```

### Advanced Automation
```
# Conditional workflows
Create a workflow with conditional logic based on data values.

# Scheduled workflows
Set up a workflow that runs daily to generate reports.

# Webhook workflows
Create a webhook-triggered workflow for real-time data processing.

# Error handling
Implement error handling and retry logic in existing workflows.

# Multi-step workflows
Build complex workflows with multiple decision points and branches.
```

### Monitoring & Analytics
```
# Workflow performance
Show me execution statistics for all workflows this month.

# Error analysis
Analyze failed workflow executions and identify common issues.

# Usage metrics
Generate a report on workflow usage and performance trends.

# Resource monitoring
Monitor resource usage and optimization opportunities.

# Audit logs
Review workflow execution logs for compliance and debugging.
```

## Features

### Core n8n Operations
- **Workflow Management**: Create, read, update, delete workflows
- **Execution Control**: Start, stop, pause, and monitor workflow executions
- **Node Configuration**: Configure and manage workflow nodes
- **Credential Management**: Handle API keys and authentication
- **Webhook Management**: Create and manage webhook endpoints

### Advanced Features
- **Conditional Logic**: Implement complex decision trees
- **Error Handling**: Robust error handling and retry mechanisms
- **Scheduling**: Time-based and event-driven workflow triggers
- **Data Transformation**: Advanced data manipulation and formatting
- **API Integration**: Connect with hundreds of services and APIs

### Automation Capabilities
- **Email Processing**: Automated email handling and responses
- **Data Synchronization**: Keep data in sync across platforms
- **File Processing**: Automated file handling and transformation
- **Social Media**: Automated posting and engagement
- **Business Process**: Streamline business operations and workflows

### Integration Features
- **400+ Integrations**: Connect with popular services and APIs
- **Custom Nodes**: Create custom integrations and functionality
- **Webhook Support**: Real-time data processing and triggers
- **Database Connectivity**: Connect to various database systems
- **Cloud Services**: Integration with major cloud platforms

## Requirements

### System Requirements
- **n8n**: Version 0.200.0 or higher (latest recommended)
- **Operating System**: Linux, macOS, or Windows
- **Node.js**: Version 16 or higher
- **Memory**: 2GB+ available RAM
- **Storage**: Varies by workflow complexity and data volume

### n8n Configuration
```javascript
// n8n environment configuration
const n8nConfig = {
  N8N_HOST: '0.0.0.0',
  N8N_PORT: 5678,
  N8N_PROTOCOL: 'https',
  N8N_ENCRYPTION_KEY: 'your-encryption-key',
  WEBHOOK_URL: 'https://your-domain.com',
  N8N_METRICS: true,
  N8N_LOG_LEVEL: 'info'
};
```

### Database Setup
```sql
-- PostgreSQL setup for n8n
CREATE DATABASE n8n;
CREATE USER n8n_user WITH PASSWORD 'secure_password';
GRANT ALL PRIVILEGES ON DATABASE n8n TO n8n_user;

-- Environment variables
export DB_TYPE=postgresdb
export DB_POSTGRESDB_HOST=localhost
export DB_POSTGRESDB_PORT=5432
export DB_POSTGRESDB_DATABASE=n8n
export DB_POSTGRESDB_USER=n8n_user
export DB_POSTGRESDB_PASSWORD=secure_password
```

## Security Considerations

### Best Practices
- **API Security**: Use strong API keys and rotate them regularly
- **Network Security**: Restrict access to n8n instance
- **Credential Management**: Store credentials securely
- **Webhook Security**: Validate webhook signatures
- **Access Control**: Implement proper user permissions

### Secure Configuration
```json
{
  "mcpServers": {
    "n8n": {
      "command": "npx",
      "args": [
        "n8n-mcp-server",
        "--n8n-url", "https://secure-n8n.example.com",
        "--api-key", "${N8N_API_KEY}",
        "--verify-ssl",
        "--timeout", "30s"
      ]
    }
  }
}
```

### n8n Security Settings
```javascript
// Security configuration
const securityConfig = {
  N8N_BASIC_AUTH_ACTIVE: true,
  N8N_BASIC_AUTH_USER: 'admin',
  N8N_BASIC_AUTH_PASSWORD: 'secure_password',
  N8N_JWT_AUTH_ACTIVE: true,
  N8N_JWT_AUTH_HEADER: 'authorization',
  N8N_SECURE_COOKIE: true,
  N8N_DISABLE_UI: false
};
```

## Troubleshooting

### Common Issues

#### Connection Failed
**Problem**: Cannot connect to n8n instance
**Solution**:
```bash
# Test n8n connectivity
curl -I http://localhost:5678

# Check n8n service status
docker ps | grep n8n
# or
pm2 status n8n

# Verify API endpoint
curl -H "X-N8N-API-KEY: $API_KEY" \
  http://localhost:5678/api/v1/workflows
```

#### Authentication Failed
**Problem**: Invalid API key or credentials
**Solution**:
- Generate new API key in n8n settings
- Verify API key permissions
- Check basic auth credentials
- Ensure proper headers are set

#### Workflow Execution Errors
**Problem**: Workflows failing to execute
**Solution**:
```bash
# Check workflow logs
curl -H "X-N8N-API-KEY: $API_KEY" \
  http://localhost:5678/api/v1/executions

# Validate workflow configuration
# Check node credentials and connections
# Verify webhook URLs and triggers
```

#### Performance Issues
**Problem**: Slow workflow execution
**Solution**:
- Optimize workflow logic and reduce complexity
- Check database performance
- Monitor system resources
- Implement caching where appropriate

### Diagnostic Commands
```bash
# n8n health check
curl http://localhost:5678/healthz

# List workflows
curl -H "X-N8N-API-KEY: $API_KEY" \
  http://localhost:5678/api/v1/workflows

# Check executions
curl -H "X-N8N-API-KEY: $API_KEY" \
  http://localhost:5678/api/v1/executions

# System information
curl -H "X-N8N-API-KEY: $API_KEY" \
  http://localhost:5678/api/v1/system/info
```

## Advanced Configuration

### Custom Node Development
```javascript
// Custom node example
import { INodeType, INodeTypeDescription } from 'n8n-workflow';

export class CustomMCPNode implements INodeType {
  description: INodeTypeDescription = {
    displayName: 'Custom MCP Node',
    name: 'customMcpNode',
    group: ['transform'],
    version: 1,
    description: 'Custom node for MCP integration',
    defaults: {
      name: 'Custom MCP Node',
    },
    inputs: ['main'],
    outputs: ['main'],
    properties: [
      {
        displayName: 'Operation',
        name: 'operation',
        type: 'options',
        options: [
          {
            name: 'Process Data',
            value: 'processData',
          },
        ],
        default: 'processData',
      },
    ],
  };

  async execute(this: IExecuteFunctions): Promise<INodeExecutionData[][]> {
    // Implementation logic
    return [[]];
  }
}
```

### Workflow Templates
```json
{
  "name": "Email to Task Automation",
  "nodes": [
    {
      "parameters": {
        "pollTimes": {
          "item": [
            {
              "mode": "everyMinute"
            }
          ]
        }
      },
      "name": "Email Trigger",
      "type": "n8n-nodes-base.emailReadImap",
      "position": [250, 300]
    },
    {
      "parameters": {
        "conditions": {
          "string": [
            {
              "value1": "={{$json[\"subject\"]}}",
              "operation": "contains",
              "value2": "URGENT"
            }
          ]
        }
      },
      "name": "Check Priority",
      "type": "n8n-nodes-base.if",
      "position": [450, 300]
    },
    {
      "parameters": {
        "resource": "page",
        "operation": "create",
        "pageId": "notion-database-id",
        "title": "={{$json[\"subject\"]}}",
        "properties": {
          "Priority": "High",
          "Status": "To Do"
        }
      },
      "name": "Create Notion Task",
      "type": "n8n-nodes-base.notion",
      "position": [650, 200]
    }
  ],
  "connections": {
    "Email Trigger": {
      "main": [
        [
          {
            "node": "Check Priority",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Check Priority": {
      "main": [
        [
          {
            "node": "Create Notion Task",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

### Webhook Configuration
```javascript
// Webhook workflow configuration
const webhookWorkflow = {
  name: "MCP Webhook Handler",
  active: true,
  nodes: [
    {
      name: "Webhook",
      type: "n8n-nodes-base.webhook",
      parameters: {
        httpMethod: "POST",
        path: "mcp-handler",
        responseMode: "responseNode"
      },
      position: [250, 300]
    },
    {
      name: "Process Data",
      type: "n8n-nodes-base.function",
      parameters: {
        functionCode: `
          // Process incoming MCP data
          const data = items[0].json;
          
          // Transform data
          const processed = {
            id: data.id,
            timestamp: new Date().toISOString(),
            processed: true,
            original: data
          };
          
          return [{ json: processed }];
        `
      },
      position: [450, 300]
    },
    {
      name: "Webhook Response",
      type: "n8n-nodes-base.respondToWebhook",
      parameters: {
        respondWith: "json",
        responseBody: `{
          "status": "success",
          "message": "Data processed successfully"
        }`
      },
      position: [650, 300]
    }
  ]
};
```

## Workflow Examples

### Data Processing Pipeline
```json
{
  "name": "Data Processing Pipeline",
  "description": "Process CSV files and sync to database",
  "workflow": {
    "trigger": "file_upload",
    "steps": [
      {
        "name": "Parse CSV",
        "type": "csv_parser",
        "config": {
          "delimiter": ",",
          "headers": true
        }
      },
      {
        "name": "Validate Data",
        "type": "data_validator",
        "config": {
          "rules": [
            {"field": "email", "type": "email"},
            {"field": "age", "type": "number", "min": 0}
          ]
        }
      },
      {
        "name": "Transform Data",
        "type": "data_transformer",
        "config": {
          "mappings": {
            "full_name": "{{first_name}} {{last_name}}",
            "created_at": "{{$now}}"
          }
        }
      },
      {
        "name": "Save to Database",
        "type": "database_insert",
        "config": {
          "table": "customers",
          "conflict": "update"
        }
      }
    ]
  }
}
```

### Social Media Automation
```json
{
  "name": "Social Media Cross-Posting",
  "description": "Post content across multiple platforms",
  "workflow": {
    "trigger": "webhook",
    "steps": [
      {
        "name": "Content Validation",
        "type": "content_validator",
        "config": {
          "max_length": 280,
          "required_fields": ["text", "image"]
        }
      },
      {
        "name": "Image Processing",
        "type": "image_processor",
        "config": {
          "resize": {"width": 1200, "height": 630},
          "format": "jpg",
          "quality": 85
        }
      },
      {
        "name": "Post to Twitter",
        "type": "twitter_post",
        "config": {
          "text": "{{content.text}}",
          "media": "{{processed_image}}"
        }
      },
      {
        "name": "Post to LinkedIn",
        "type": "linkedin_post",
        "config": {
          "text": "{{content.text}}",
          "media": "{{processed_image}}"
        }
      },
      {
        "name": "Log Results",
        "type": "logger",
        "config": {
          "level": "info",
          "message": "Posted to {{platforms.length}} platforms"
        }
      }
    ]
  }
}
```

### Business Process Automation
```json
{
  "name": "Invoice Processing",
  "description": "Automated invoice processing and approval",
  "workflow": {
    "trigger": "email_attachment",
    "steps": [
      {
        "name": "Extract Invoice Data",
        "type": "ocr_processor",
        "config": {
          "fields": ["amount", "vendor", "date", "invoice_number"]
        }
      },
      {
        "name": "Validate Amount",
        "type": "conditional",
        "config": {
          "condition": "{{amount}} > 1000",
          "true_path": "require_approval",
          "false_path": "auto_approve"
        }
      },
      {
        "name": "Send for Approval",
        "type": "slack_message",
        "config": {
          "channel": "#finance",
          "message": "Invoice {{invoice_number}} requires approval: ${{amount}}"
        }
      },
      {
        "name": "Update Accounting System",
        "type": "api_call",
        "config": {
          "url": "https://accounting.example.com/api/invoices",
          "method": "POST",
          "data": "{{extracted_data}}"
        }
      }
    ]
  }
}
```

## Integration with Other MCPs

### With Notion MCP
```
# Knowledge management workflow
1. Use n8n MCP to automate data collection
2. Use notion MCP to organize information
3. Create automated documentation workflows
4. Sync project updates across platforms
```

### With Slack MCP
```
# Team communication automation
1. Use n8n MCP to monitor systems
2. Use slack MCP to send notifications
3. Automate incident response workflows
4. Create team productivity dashboards
```

### With Database MCPs
```
# Data synchronization workflow
1. Use n8n MCP to orchestrate data flows
2. Use database MCPs for data operations
3. Implement real-time data synchronization
4. Create automated backup and recovery
```

## Performance Optimization

### Workflow Optimization
```javascript
// Optimization strategies
const optimizationTips = {
  "batch_processing": "Process multiple items together",
  "caching": "Cache frequently accessed data",
  "parallel_execution": "Run independent tasks in parallel",
  "error_handling": "Implement proper error handling",
  "resource_management": "Monitor and limit resource usage"
};
```

### Monitoring and Metrics
```javascript
// Monitoring configuration
const monitoringConfig = {
  metrics: {
    execution_time: true,
    success_rate: true,
    error_rate: true,
    resource_usage: true
  },
  alerts: {
    execution_failure: {
      threshold: 5,
      window: "5m"
    },
    high_latency: {
      threshold: "30s",
      window: "1m"
    }
  }
};
```

## Links

- [n8n MCP Nodes Repository](https://github.com/nerding-io/n8n-nodes-mcp)
- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community](https://community.n8n.io/)
- [n8n Workflow Templates](https://n8n.io/workflows/)
- [n8n API Documentation](https://docs.n8n.io/api/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [n8n Community Forum](https://community.n8n.io/)
- [n8n Discord](https://discord.gg/n8n)
- [MCP Discord](https://discord.gg/mcp)
- [n8n YouTube Channel](https://www.youtube.com/c/n8n-io)
- [Awesome n8n](https://github.com/n8n-io/awesome-n8n)

