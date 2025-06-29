# Grafana MCP

## Overview
The Grafana MCP provides Claude with comprehensive data visualization and dashboard management capabilities, enabling the creation, modification, and analysis of monitoring dashboards, alerting rules, and data source integrations. This MCP is essential for observability workflows and data-driven decision making.

## Installation

### Prerequisites
- Grafana server running and accessible
- Grafana API key or authentication credentials
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Data sources configured in Grafana

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx grafana-mcp-server
```

#### Option 2: From GitHub
```bash
git clone https://github.com/grafana-mcp/grafana-mcp-server.git
cd grafana-mcp-server
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install grafana-mcp-server
```

#### Option 4: Docker Container
```bash
docker run -d --name grafana-mcp \
  -e GRAFANA_URL=http://grafana:3000 \
  -e GRAFANA_API_KEY=your-api-key \
  grafana-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "grafana": {
      "command": "npx",
      "args": [
        "grafana-mcp-server",
        "--url", "http://localhost:3000",
        "--api-key", "your-grafana-api-key"
      ]
    }
  }
}
```

### With Authentication
```json
{
  "mcpServers": {
    "grafana": {
      "command": "npx",
      "args": [
        "grafana-mcp-server",
        "--url", "https://grafana.example.com",
        "--username", "admin",
        "--password", "${GRAFANA_PASSWORD}",
        "--org-id", "1"
      ]
    }
  }
}
```

### Multiple Grafana Instances
```json
{
  "mcpServers": {
    "grafana-prod": {
      "command": "npx",
      "args": [
        "grafana-mcp-server",
        "--url", "https://grafana-prod.example.com",
        "--api-key", "${GRAFANA_PROD_KEY}"
      ]
    },
    "grafana-dev": {
      "command": "npx",
      "args": [
        "grafana-mcp-server",
        "--url", "http://localhost:3000",
        "--api-key", "${GRAFANA_DEV_KEY}"
      ]
    }
  }
}
```

### Environment Variables
```bash
export GRAFANA_URL=http://localhost:3000
export GRAFANA_API_KEY=your-api-key
export GRAFANA_ORG_ID=1
export GRAFANA_TIMEOUT=30s
```

## Usage Examples

### Dashboard Management
```
# List dashboards
Show me all dashboards in the current Grafana organization.

# Create dashboard
Create a new dashboard called "Application Performance" with CPU and memory panels.

# Update dashboard
Add a new panel showing HTTP request rate to the "Web Services" dashboard.

# Export dashboard
Export the "Infrastructure Overview" dashboard as JSON.

# Import dashboard
Import the dashboard from the provided JSON configuration.
```

### Panel Operations
```
# Create panels
Add a graph panel showing database connection count over time.

# Configure visualizations
Create a stat panel displaying the current number of active users.

# Set up alerts
Configure an alert on the "High CPU Usage" panel when CPU exceeds 80%.

# Panel queries
Show me the PromQL query used in the "Memory Usage" panel.

# Panel styling
Update the "Response Time" panel to use a red threshold at 500ms.
```

### Data Source Management
```
# List data sources
Show me all configured data sources in Grafana.

# Add data source
Add a new Prometheus data source pointing to http://prometheus:9090.

# Test data source
Test the connection to the "Production Prometheus" data source.

# Update data source
Update the URL for the "Development InfluxDB" data source.

# Data source queries
Test this PromQL query against the Prometheus data source.
```

### Alerting & Notifications
```
# Alert rules
Show me all alert rules and their current status.

# Create alerts
Create an alert rule for when disk usage exceeds 90%.

# Notification channels
List all configured notification channels.

# Alert history
Show me the alert history for the last 24 hours.

# Silence alerts
Temporarily silence alerts for the "maintenance" tag.
```

## Features

### Core Grafana Operations
- **Dashboard Management**: Create, update, delete, and organize dashboards
- **Panel Configuration**: Add, modify, and style visualization panels
- **Data Source Integration**: Connect to various data sources and databases
- **Query Building**: Construct and test queries for different data sources
- **Template Variables**: Create dynamic dashboards with variables

### Advanced Features
- **Alerting System**: Configure alerts, notification channels, and rules
- **User Management**: Manage users, teams, and permissions
- **Organization Management**: Handle multi-tenant configurations
- **Plugin Management**: Install and configure Grafana plugins
- **Annotation Management**: Add contextual annotations to dashboards

### Visualization Capabilities
- **Time Series**: Line graphs, area charts, and bar charts
- **Single Stat**: Gauge, stat, and bargauge panels
- **Tables**: Data tables with sorting and filtering
- **Heatmaps**: Density and correlation visualizations
- **Geospatial**: World map and geomap panels

### Integration Features
- **Prometheus**: Native Prometheus query support
- **InfluxDB**: Time series database integration
- **Elasticsearch**: Log and metric data visualization
- **MySQL/PostgreSQL**: Relational database connectivity
- **Cloud Services**: AWS CloudWatch, Azure Monitor, GCP

## Requirements

### System Requirements
- **Grafana**: Version 8.0 or higher (9.0+ recommended)
- **Operating System**: Linux, macOS, or Windows
- **Memory**: 512MB+ available RAM
- **Network**: HTTP/HTTPS access to Grafana server
- **Storage**: Minimal local storage for caching

### Grafana Configuration
```ini
# grafana.ini
[server]
http_port = 3000
domain = localhost
root_url = http://localhost:3000

[security]
admin_user = admin
admin_password = admin
secret_key = SW2YcwTIb9zpOOhoPsMm

[auth.anonymous]
enabled = true
org_name = Main Org.
org_role = Viewer

[api]
enable_cors = true
```

### Network Access
- HTTP/HTTPS access to Grafana API
- Authentication credentials (API key or username/password)
- Network access to configured data sources
- Firewall rules for Grafana port (default 3000)

## Security Considerations

### Best Practices
- **API Keys**: Use API keys with minimal required permissions
- **HTTPS**: Always use HTTPS in production environments
- **Authentication**: Implement strong authentication mechanisms
- **Authorization**: Use role-based access control (RBAC)
- **Data Source Security**: Secure connections to data sources

### Secure Configuration
```json
{
  "mcpServers": {
    "grafana": {
      "command": "npx",
      "args": [
        "grafana-mcp-server",
        "--url", "https://grafana.example.com",
        "--api-key", "${GRAFANA_API_KEY}",
        "--verify-ssl",
        "--org-id", "1"
      ]
    }
  }
}
```

### RBAC Configuration
```ini
# grafana.ini
[users]
allow_sign_up = false
allow_org_create = false
auto_assign_org = true
auto_assign_org_role = Viewer

[auth]
disable_login_form = false
disable_signout_menu = false

[auth.ldap]
enabled = true
config_file = /etc/grafana/ldap.toml
```

## Troubleshooting

### Common Issues

#### Connection Failed
**Problem**: Cannot connect to Grafana server
**Solution**:
```bash
# Test Grafana connectivity
curl -I http://localhost:3000

# Check Grafana API
curl -H "Authorization: Bearer $API_KEY" \
  http://localhost:3000/api/health

# Verify API key
curl -H "Authorization: Bearer $API_KEY" \
  http://localhost:3000/api/user
```

#### Authentication Failed
**Problem**: Invalid API key or credentials
**Solution**:
```bash
# Generate new API key in Grafana UI
# Configuration -> API Keys -> Add API key

# Test API key
curl -H "Authorization: Bearer $API_KEY" \
  http://localhost:3000/api/org

# Check user permissions
curl -H "Authorization: Bearer $API_KEY" \
  http://localhost:3000/api/user/orgs
```

#### Dashboard Not Found
**Problem**: Cannot access or modify dashboards
**Solution**:
- Verify dashboard UID or slug
- Check user permissions for dashboard
- Ensure dashboard exists in correct organization
- Validate folder permissions

#### Data Source Issues
**Problem**: Data source connection failures
**Solution**:
```bash
# Test data source connectivity
curl -H "Authorization: Bearer $API_KEY" \
  http://localhost:3000/api/datasources/proxy/1/api/v1/query?query=up

# Check data source configuration
curl -H "Authorization: Bearer $API_KEY" \
  http://localhost:3000/api/datasources
```

### Diagnostic Commands
```bash
# Grafana health check
curl http://localhost:3000/api/health

# API version
curl http://localhost:3000/api/frontend/settings

# Organization info
curl -H "Authorization: Bearer $API_KEY" \
  http://localhost:3000/api/org

# User info
curl -H "Authorization: Bearer $API_KEY" \
  http://localhost:3000/api/user
```

## Advanced Configuration

### Custom Dashboard Templates
```json
{
  "dashboard": {
    "id": null,
    "title": "Application Performance",
    "tags": ["application", "performance"],
    "timezone": "browser",
    "panels": [
      {
        "id": 1,
        "title": "CPU Usage",
        "type": "graph",
        "targets": [
          {
            "expr": "cpu_usage_percent",
            "legendFormat": "{{instance}}"
          }
        ],
        "yAxes": [
          {
            "min": 0,
            "max": 100,
            "unit": "percent"
          }
        ]
      }
    ],
    "time": {
      "from": "now-1h",
      "to": "now"
    },
    "refresh": "5s"
  }
}
```

### Alert Rule Configuration
```json
{
  "alert": {
    "name": "High CPU Usage",
    "message": "CPU usage is above 80%",
    "frequency": "10s",
    "conditions": [
      {
        "query": {
          "queryType": "",
          "refId": "A",
          "model": {
            "expr": "cpu_usage_percent > 80",
            "intervalMs": 1000,
            "maxDataPoints": 43200
          }
        },
        "reducer": {
          "type": "last",
          "params": []
        },
        "evaluator": {
          "params": [80],
          "type": "gt"
        }
      }
    ],
    "executionErrorState": "alerting",
    "noDataState": "no_data",
    "for": "5m"
  }
}
```

### Data Source Configuration
```json
{
  "name": "Prometheus",
  "type": "prometheus",
  "url": "http://prometheus:9090",
  "access": "proxy",
  "isDefault": true,
  "jsonData": {
    "httpMethod": "POST",
    "timeInterval": "15s"
  },
  "secureJsonData": {
    "httpHeaderValue1": "Bearer token123"
  }
}
```

## Dashboard Examples

### Infrastructure Monitoring
```json
{
  "dashboard": {
    "title": "Infrastructure Overview",
    "panels": [
      {
        "title": "System Load",
        "type": "graph",
        "targets": [
          {
            "expr": "node_load1",
            "legendFormat": "1m load - {{instance}}"
          }
        ]
      },
      {
        "title": "Memory Usage",
        "type": "singlestat",
        "targets": [
          {
            "expr": "(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100",
            "legendFormat": "Memory Usage %"
          }
        ]
      },
      {
        "title": "Disk I/O",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(node_disk_read_bytes_total[5m])",
            "legendFormat": "Read - {{device}}"
          },
          {
            "expr": "rate(node_disk_written_bytes_total[5m])",
            "legendFormat": "Write - {{device}}"
          }
        ]
      }
    ]
  }
}
```

### Application Performance
```json
{
  "dashboard": {
    "title": "Application Performance",
    "panels": [
      {
        "title": "Request Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "sum(rate(http_requests_total[5m])) by (service)",
            "legendFormat": "{{service}}"
          }
        ]
      },
      {
        "title": "Response Time",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, service))",
            "legendFormat": "95th percentile - {{service}}"
          }
        ]
      },
      {
        "title": "Error Rate",
        "type": "singlestat",
        "targets": [
          {
            "expr": "sum(rate(http_requests_total{status=~\"5..\"}[5m])) / sum(rate(http_requests_total[5m])) * 100",
            "legendFormat": "Error Rate %"
          }
        ]
      }
    ]
  }
}
```

### Business Metrics
```json
{
  "dashboard": {
    "title": "Business KPIs",
    "panels": [
      {
        "title": "Active Users",
        "type": "stat",
        "targets": [
          {
            "expr": "active_users_total",
            "legendFormat": "Active Users"
          }
        ]
      },
      {
        "title": "Revenue",
        "type": "graph",
        "targets": [
          {
            "expr": "sum(revenue_total) by (product)",
            "legendFormat": "{{product}}"
          }
        ]
      },
      {
        "title": "Conversion Rate",
        "type": "gauge",
        "targets": [
          {
            "expr": "conversions_total / visits_total * 100",
            "legendFormat": "Conversion Rate %"
          }
        ]
      }
    ]
  }
}
```

## Integration with Other MCPs

### With Prometheus MCP
```
# Monitoring workflow
1. Use prometheus MCP to query metrics
2. Use grafana MCP to create visualizations
3. Set up alerts and notifications
4. Share dashboards with teams
```

### With Kubernetes MCP
```
# Container monitoring
1. Use kubernetes MCP to deploy applications
2. Use grafana MCP to monitor container metrics
3. Create dashboards for cluster health
4. Alert on pod and node issues
```

### With Jenkins MCP
```
# CI/CD monitoring
1. Use jenkins MCP to manage builds
2. Use grafana MCP to visualize build metrics
3. Track deployment success rates
4. Monitor pipeline performance
```

## Workflow Examples

### Dashboard Creation
```
1. Define monitoring requirements
2. Identify relevant data sources
3. Create dashboard structure
4. Add and configure panels
5. Set up alerts and notifications
6. Share with stakeholders
```

### Alert Management
```
1. Identify critical metrics to monitor
2. Define alert thresholds and conditions
3. Configure notification channels
4. Test alert rules and notifications
5. Document alert response procedures
6. Review and tune alert sensitivity
```

### Performance Analysis
```
1. Collect baseline performance metrics
2. Create performance dashboards
3. Monitor trends and anomalies
4. Investigate performance issues
5. Optimize based on insights
6. Document findings and improvements
```

## Links

- [Grafana MCP Repository](https://github.com/grafana-mcp/grafana-mcp-server)
- [Grafana Documentation](https://grafana.com/docs/)
- [Grafana API Documentation](https://grafana.com/docs/grafana/latest/http_api/)
- [Grafana Dashboards](https://grafana.com/grafana/dashboards/)
- [Grafana Plugins](https://grafana.com/grafana/plugins/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Grafana Community](https://community.grafana.com/)
- [Grafana Slack](https://grafana.slack.com/)
- [MCP Discord](https://discord.gg/mcp)
- [Awesome Grafana](https://github.com/grafana/awesome-grafana)
- [Grafana Best Practices](https://grafana.com/docs/grafana/latest/best-practices/)

