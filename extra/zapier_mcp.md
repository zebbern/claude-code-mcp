# Zapier MCP

## Overview
The Zapier MCP provides Claude with comprehensive Zapier automation platform integration, enabling the creation, management, and execution of Zaps (automated workflows) that connect thousands of apps and services. This MCP is essential for no-code automation and business process optimization.

## Installation

### Prerequisites
- Zapier account with API access
- Zapier API key or OAuth credentials
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Access to Zapier apps and integrations

### Install Steps

#### Option 1: NPX Installation
```bash
npx zapier-mcp-server
```

#### Option 2: From GitHub
```bash
git clone https://github.com/zapier-mcp/zapier-mcp-server.git
cd zapier-mcp-server
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install zapier-mcp-server
```

#### Option 4: Docker Container
```bash
docker run -d --name zapier-mcp \
  -e ZAPIER_API_KEY=your-api-key \
  zapier-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "zapier": {
      "command": "npx",
      "args": [
        "zapier-mcp-server",
        "--api-key", "your-zapier-api-key"
      ]
    }
  }
}
```

### With Environment Variables
```json
{
  "mcpServers": {
    "zapier": {
      "command": "npx",
      "args": ["zapier-mcp-server"],
      "env": {
        "ZAPIER_API_KEY": "your-zapier-api-key",
        "ZAPIER_WEBHOOK_URL": "https://hooks.zapier.com/hooks/catch/your-hook"
      }
    }
  }
}
```

### OAuth Configuration
```json
{
  "mcpServers": {
    "zapier": {
      "command": "npx",
      "args": [
        "zapier-mcp-server",
        "--oauth-client-id", "${ZAPIER_CLIENT_ID}",
        "--oauth-client-secret", "${ZAPIER_CLIENT_SECRET}",
        "--oauth-redirect-uri", "http://localhost:3000/callback"
      ]
    }
  }
}
```

## Usage Examples

### Zap Management
```
# List Zaps
Show me all my active Zaps and their status.

# Create Zap
Create a new Zap that sends Slack notifications when I receive important emails.

# Update Zap
Modify the "Lead Processing" Zap to include additional data fields.

# Enable/Disable Zaps
Turn off the "Social Media Posting" Zap temporarily.

# Delete Zap
Remove the outdated "Old CRM Integration" Zap.
```

### Workflow Creation
```
# Email to CRM automation
Create a Zap that adds new email contacts to my CRM automatically.

# Social media automation
Set up a Zap that posts new blog articles to all my social media accounts.

# Data synchronization
Create a Zap that syncs customer data between my e-commerce store and email marketing tool.

# File processing
Build a Zap that processes uploaded files and organizes them in cloud storage.

# Lead management
Create a Zap that qualifies leads and assigns them to sales team members.
```

### Advanced Automation
```
# Multi-step workflows
Create a complex Zap with multiple conditions and actions.

# Webhook integrations
Set up webhook-triggered Zaps for real-time data processing.

# Scheduled automation
Create time-based Zaps that run on specific schedules.

# Conditional logic
Implement Zaps with filters and conditional branching.

# Error handling
Set up error notifications and retry logic for failed Zaps.
```

### Analytics & Monitoring
```
# Zap performance
Show me execution statistics for all Zaps this month.

# Error analysis
Analyze failed Zap runs and identify common issues.

# Usage metrics
Generate a report on Zap usage and automation ROI.

# Task consumption
Monitor task usage and optimize for efficiency.

# Success rates
Track success rates across different Zap types.
```

## Features

### Core Zapier Operations
- **Zap Management**: Create, read, update, delete, and manage Zaps
- **Trigger Configuration**: Set up various triggers and webhooks
- **Action Configuration**: Configure actions and data transformations
- **App Integration**: Connect with 5000+ supported applications
- **Workflow Execution**: Monitor and control Zap executions

### Advanced Features
- **Multi-Step Zaps**: Complex workflows with multiple actions
- **Conditional Logic**: Filters and paths for decision-making
- **Data Formatting**: Transform and format data between apps
- **Error Handling**: Robust error handling and retry mechanisms
- **Webhook Support**: Real-time triggers and custom integrations

### Automation Capabilities
- **Email Automation**: Automated email processing and responses
- **CRM Integration**: Customer relationship management workflows
- **Social Media**: Automated posting and engagement
- **E-commerce**: Order processing and inventory management
- **Marketing**: Lead generation and nurturing workflows

### Integration Features
- **5000+ Apps**: Connect with virtually any web service
- **Custom Webhooks**: Create custom integrations
- **API Connections**: Direct API integrations
- **Database Sync**: Keep databases synchronized
- **File Processing**: Automated file handling and storage

## Requirements

### System Requirements
- **Operating System**: Linux, macOS, or Windows
- **Node.js**: Version 16 or higher
- **Memory**: 512MB+ available RAM
- **Network**: Internet access for Zapier API
- **Storage**: Minimal local storage for caching

### Zapier Account Requirements
- Active Zapier account (Free, Starter, or Professional)
- API access enabled
- Appropriate app permissions
- Task allocation based on plan

### API Limits
```javascript
// Zapier API rate limits
const rateLimits = {
  free: {
    tasksPerMonth: 100,
    zapsLimit: 5,
    updateFrequency: "15 minutes"
  },
  starter: {
    tasksPerMonth: 750,
    zapsLimit: 20,
    updateFrequency: "15 minutes"
  },
  professional: {
    tasksPerMonth: 2000,
    zapsLimit: 100,
    updateFrequency: "2 minutes"
  }
};
```

## Security Considerations

### Best Practices
- **API Security**: Store API keys securely
- **App Permissions**: Grant minimal required permissions
- **Webhook Security**: Validate webhook signatures
- **Data Privacy**: Handle sensitive data appropriately
- **Access Control**: Limit Zap access to authorized users

### Secure Configuration
```json
{
  "mcpServers": {
    "zapier": {
      "command": "npx",
      "args": ["zapier-mcp-server"],
      "env": {
        "ZAPIER_API_KEY": "${ZAPIER_API_KEY}",
        "ZAPIER_VERIFY_SSL": "true",
        "ZAPIER_TIMEOUT": "30s"
      }
    }
  }
}
```

### Data Protection
```javascript
// Data handling configuration
const dataProtection = {
  encryption: true,
  dataRetention: "30 days",
  sensitiveFields: ["email", "phone", "ssn"],
  anonymization: true,
  auditLogging: true
};
```

## Troubleshooting

### Common Issues

#### Authentication Failed
**Problem**: Invalid API key or expired credentials
**Solution**:
- Verify API key in Zapier account settings
- Check API key permissions and scope
- Regenerate API key if necessary
- Ensure proper OAuth flow completion

#### Zap Execution Errors
**Problem**: Zaps failing to execute properly
**Solution**:
```bash
# Check Zap status
curl -H "Authorization: Bearer $ZAPIER_API_KEY" \
  https://api.zapier.com/v1/zaps

# Review error logs
curl -H "Authorization: Bearer $ZAPIER_API_KEY" \
  https://api.zapier.com/v1/zap-runs?status=error

# Test Zap manually
curl -X POST -H "Authorization: Bearer $ZAPIER_API_KEY" \
  https://api.zapier.com/v1/zaps/{zap_id}/test
```

#### Rate Limit Exceeded
**Problem**: Too many API requests
**Solution**:
- Implement request throttling
- Optimize Zap frequency
- Upgrade Zapier plan if needed
- Use batch operations when possible

#### App Connection Issues
**Problem**: Connected apps losing authentication
**Solution**:
- Reconnect apps in Zapier dashboard
- Check app-specific permissions
- Verify OAuth tokens are valid
- Update app credentials if changed

### Diagnostic Commands
```bash
# Test Zapier API connectivity
curl -H "Authorization: Bearer $ZAPIER_API_KEY" \
  https://api.zapier.com/v1/me

# List available apps
curl -H "Authorization: Bearer $ZAPIER_API_KEY" \
  https://api.zapier.com/v1/apps

# Check Zap history
curl -H "Authorization: Bearer $ZAPIER_API_KEY" \
  https://api.zapier.com/v1/zap-runs
```

## Advanced Configuration

### Custom Webhook Setup
```javascript
// Webhook configuration
const webhookConfig = {
  url: "https://hooks.zapier.com/hooks/catch/12345/abcdef/",
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "X-Zapier-Signature": "webhook-signature"
  },
  payload: {
    trigger: "custom_event",
    data: "{{input_data}}",
    timestamp: "{{current_timestamp}}"
  }
};
```

### Zap Templates
```json
{
  "name": "Email to CRM Lead",
  "description": "Add email contacts to CRM as leads",
  "trigger": {
    "app": "gmail",
    "event": "new_email",
    "filters": [
      {
        "field": "subject",
        "operator": "contains",
        "value": "inquiry"
      }
    ]
  },
  "actions": [
    {
      "app": "salesforce",
      "action": "create_lead",
      "fields": {
        "first_name": "{{trigger.from_name}}",
        "email": "{{trigger.from_email}}",
        "company": "{{trigger.subject}}",
        "lead_source": "Email Inquiry"
      }
    },
    {
      "app": "slack",
      "action": "send_message",
      "fields": {
        "channel": "#sales",
        "message": "New lead: {{trigger.from_name}} ({{trigger.from_email}})"
      }
    }
  ]
}
```

### Multi-Step Workflow
```json
{
  "name": "E-commerce Order Processing",
  "description": "Complete order fulfillment workflow",
  "steps": [
    {
      "trigger": {
        "app": "shopify",
        "event": "new_order"
      }
    },
    {
      "action": {
        "app": "inventory_system",
        "action": "check_stock",
        "fields": {
          "product_id": "{{trigger.line_items.product_id}}",
          "quantity": "{{trigger.line_items.quantity}}"
        }
      }
    },
    {
      "filter": {
        "field": "stock_available",
        "operator": "greater_than",
        "value": 0
      }
    },
    {
      "action": {
        "app": "fulfillment_service",
        "action": "create_shipment",
        "fields": {
          "order_id": "{{trigger.id}}",
          "shipping_address": "{{trigger.shipping_address}}"
        }
      }
    },
    {
      "action": {
        "app": "email_service",
        "action": "send_email",
        "fields": {
          "to": "{{trigger.customer.email}}",
          "subject": "Order Confirmation #{{trigger.order_number}}",
          "template": "order_confirmation"
        }
      }
    }
  ]
}
```

## API Examples

### Basic Operations
```javascript
// Create a new Zap
const newZap = await zapier.zaps.create({
  title: "Gmail to Slack Notifications",
  trigger: {
    app: "gmail",
    event: "new_email"
  },
  actions: [
    {
      app: "slack",
      action: "send_channel_message",
      params: {
        channel: "#general",
        message: "New email: {{trigger.subject}}"
      }
    }
  ]
});

// List all Zaps
const zaps = await zapier.zaps.list({
  status: "active",
  limit: 50
});

// Update Zap
await zapier.zaps.update(zapId, {
  title: "Updated Zap Title",
  status: "paused"
});

// Delete Zap
await zapier.zaps.delete(zapId);
```

### Advanced Workflows
```javascript
// Multi-step Zap with conditions
const complexZap = await zapier.zaps.create({
  title: "Lead Qualification Workflow",
  trigger: {
    app: "typeform",
    event: "new_entry"
  },
  actions: [
    {
      app: "filter",
      action: "only_continue_if",
      params: {
        condition: "{{trigger.score}} > 80"
      }
    },
    {
      app: "salesforce",
      action: "create_lead",
      params: {
        first_name: "{{trigger.first_name}}",
        last_name: "{{trigger.last_name}}",
        email: "{{trigger.email}}",
        lead_score: "{{trigger.score}}"
      }
    },
    {
      app: "slack",
      action: "send_direct_message",
      params: {
        user: "@sales-manager",
        message: "High-quality lead: {{trigger.first_name}} {{trigger.last_name}}"
      }
    }
  ]
});
```

### Webhook Integration
```javascript
// Set up webhook trigger
const webhookZap = await zapier.zaps.create({
  title: "Custom Webhook Handler",
  trigger: {
    app: "webhook",
    event: "catch_hook",
    params: {
      url: "https://hooks.zapier.com/hooks/catch/12345/abcdef/"
    }
  },
  actions: [
    {
      app: "airtable",
      action: "create_record",
      params: {
        base: "app123456",
        table: "Leads",
        fields: {
          "Name": "{{trigger.name}}",
          "Email": "{{trigger.email}}",
          "Source": "{{trigger.source}}"
        }
      }
    }
  ]
});

// Trigger webhook
const response = await fetch("https://hooks.zapier.com/hooks/catch/12345/abcdef/", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "John Doe",
    email: "john@example.com",
    source: "website"
  })
});
```

## Integration with Other MCPs

### With Notion MCP
```
# Productivity automation
1. Use zapier MCP to automate data collection
2. Use notion MCP to organize information
3. Create automated project management workflows
4. Sync tasks and notes across platforms
```

### With Slack MCP
```
# Team communication automation
1. Use zapier MCP to monitor external systems
2. Use slack MCP for team notifications
3. Automate incident response workflows
4. Create team productivity dashboards
```

### With CRM MCPs
```
# Sales automation workflow
1. Use zapier MCP to capture leads from multiple sources
2. Use CRM MCPs for lead management
3. Automate lead scoring and assignment
4. Create comprehensive sales funnels
```

## Workflow Examples

### Lead Generation
```
1. Capture leads from website forms, social media, and ads
2. Qualify leads based on predefined criteria
3. Route qualified leads to appropriate sales reps
4. Send welcome emails and nurture sequences
5. Track lead progression through sales funnel
6. Generate reports on lead quality and conversion
```

### Customer Support
```
1. Monitor support channels for new tickets
2. Categorize and prioritize tickets automatically
3. Route tickets to appropriate support agents
4. Send acknowledgment emails to customers
5. Escalate urgent issues to management
6. Track resolution times and satisfaction scores
```

### E-commerce Automation
```
1. Process new orders and payment confirmations
2. Update inventory levels across platforms
3. Generate shipping labels and tracking numbers
4. Send order confirmations and shipping notifications
5. Handle returns and refund processing
6. Sync customer data across all systems
```

## Performance Optimization

### Efficiency Tips
```javascript
// Optimization strategies
const optimizationTips = {
  "batch_processing": "Group similar actions together",
  "filter_early": "Use filters to reduce unnecessary actions",
  "minimize_steps": "Combine actions when possible",
  "cache_data": "Store frequently used data",
  "monitor_usage": "Track task consumption and optimize"
};
```

### Monitoring Configuration
```javascript
// Monitoring setup
const monitoringConfig = {
  alerts: {
    zap_failures: {
      threshold: 5,
      window: "1 hour",
      notification: "email"
    },
    high_task_usage: {
      threshold: "80%",
      window: "daily",
      notification: "slack"
    }
  },
  metrics: {
    success_rate: true,
    execution_time: true,
    task_consumption: true,
    error_frequency: true
  }
};
```

## Links

- [Zapier API Documentation](https://zapier.com/developer/documentation/v2/rest-hooks/)
- [Zapier Platform](https://zapier.com/developer/)
- [Zapier App Directory](https://zapier.com/apps)
- [Zapier Help Center](https://help.zapier.com/)
- [Zapier Community](https://community.zapier.com/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Zapier Community Forum](https://community.zapier.com/)
- [Zapier Developer Discord](https://discord.gg/zapier-developers)
- [MCP Discord](https://discord.gg/mcp)
- [Zapier YouTube Channel](https://www.youtube.com/c/Zapier)
- [Automation Best Practices](https://zapier.com/blog/automation-best-practices/)

