# Prometheus MCP

## Overview
The Prometheus MCP provides Claude with comprehensive monitoring and observability capabilities, enabling metrics collection, alerting, and time-series data analysis. This MCP is essential for application performance monitoring, infrastructure observability, and DevOps workflows.

## Installation

### Prerequisites
- Prometheus server running and accessible
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Network access to Prometheus API
- Basic understanding of PromQL

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx mcp-server-prometheus
```

#### Option 2: From GitHub
```bash
git clone https://github.com/prometheus-mcp/mcp-server-prometheus.git
cd mcp-server-prometheus
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install prometheus-mcp-server
```

#### Option 4: Docker Container
```bash
docker run -d --name prometheus-mcp \
  -e PROMETHEUS_URL=http://prometheus:9090 \
  prometheus-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "prometheus": {
      "command": "npx",
      "args": [
        "mcp-server-prometheus",
        "--url", "http://localhost:9090"
      ]
    }
  }
}
```

### With Authentication
```json
{
  "mcpServers": {
    "prometheus": {
      "command": "npx",
      "args": [
        "mcp-server-prometheus",
        "--url", "https://prometheus.example.com",
        "--auth-token", "your-auth-token"
      ]
    }
  }
}
```

### Multiple Prometheus Instances
```json
{
  "mcpServers": {
    "prometheus-prod": {
      "command": "npx",
      "args": [
        "mcp-server-prometheus",
        "--url", "https://prometheus-prod.example.com"
      ]
    },
    "prometheus-dev": {
      "command": "npx",
      "args": [
        "mcp-server-prometheus",
        "--url", "http://localhost:9090"
      ]
    }
  }
}
```

### Environment Variables
```bash
export PROMETHEUS_URL=http://localhost:9090
export PROMETHEUS_AUTH_TOKEN=your-token
export PROMETHEUS_TIMEOUT=30s
```

## Usage Examples

### Basic Metrics Queries
```
# Current CPU usage
Show me the current CPU usage across all instances.

# Memory utilization
What's the memory utilization for the "web-server" service?

# Request rate
Display the HTTP request rate for the last hour.

# Error rate
Show me the error rate for API endpoints over the last 24 hours.

# Disk usage
Check disk usage across all monitored hosts.
```

### Advanced PromQL Queries
```
# Top 10 highest CPU consumers
Show me the top 10 processes with highest CPU usage.

# 95th percentile response time
What's the 95th percentile response time for our API?

# Rate of increase
Calculate the rate of increase for database connections.

# Aggregation by label
Group memory usage by application and environment.

# Prediction queries
Predict when disk space will be exhausted based on current trends.
```

### Alerting and Monitoring
```
# Active alerts
Show me all currently firing alerts.

# Alert history
Display alert history for the last week.

# Threshold monitoring
Monitor when CPU usage exceeds 80% for more than 5 minutes.

# Custom alerts
Create an alert for when response time exceeds 500ms.

# Alert correlation
Find correlations between different alert types.
```

### Performance Analysis
```
# Service performance
Analyze the performance of the "user-service" over the last day.

# Capacity planning
Help me understand resource usage trends for capacity planning.

# Anomaly detection
Identify unusual patterns in application metrics.

# Comparison analysis
Compare current performance with last week's metrics.
```

## Features

### Core Prometheus Operations
- **Metric Queries**: Execute PromQL queries against Prometheus
- **Time Range Queries**: Query metrics over specific time ranges
- **Instant Queries**: Get current metric values
- **Label Queries**: Discover available labels and values
- **Metadata Access**: Retrieve metric metadata and help

### Advanced Query Features
- **Aggregation Functions**: sum, avg, max, min, count, etc.
- **Rate Calculations**: Calculate rates and derivatives
- **Histogram Analysis**: Analyze histogram and summary metrics
- **Vector Operations**: Perform operations on metric vectors
- **Time Series Math**: Mathematical operations on time series

### Alerting Integration
- **Alert Rules**: Query and manage alert rules
- **Alert Status**: Check current alert states
- **Alert History**: Access historical alert data
- **Silences**: Manage alert silences
- **Notification Integration**: Connect with alerting systems

### Visualization Support
- **Graph Data**: Prepare data for visualization
- **Dashboard Queries**: Support for dashboard creation
- **Export Formats**: Multiple data export formats
- **Real-time Updates**: Live metric streaming
- **Custom Dashboards**: Create custom monitoring views

## Requirements

### System Requirements
- **Prometheus Server**: Version 2.0 or higher
- **Operating System**: Linux, macOS, or Windows
- **Memory**: 512MB+ available RAM
- **Network**: HTTP/HTTPS access to Prometheus
- **Storage**: Minimal local storage for caching

### Prometheus Configuration
```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  - "alert_rules.yml"

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
  
  - job_name: 'node-exporter'
    static_configs:
      - targets: ['localhost:9100']
```

### Network Access
- HTTP/HTTPS access to Prometheus API
- Authentication credentials if required
- Firewall rules for Prometheus port (default 9090)
- SSL/TLS certificates for secure connections

## Security Considerations

### Best Practices
- **Authentication**: Use strong authentication mechanisms
- **Authorization**: Implement proper access controls
- **Encryption**: Use HTTPS for data transmission
- **Network Security**: Restrict network access to Prometheus
- **Data Privacy**: Be mindful of sensitive metrics

### Secure Configuration
```json
{
  "mcpServers": {
    "prometheus": {
      "command": "npx",
      "args": [
        "mcp-server-prometheus",
        "--url", "https://prometheus.example.com",
        "--tls-verify",
        "--auth-token", "${PROMETHEUS_TOKEN}"
      ]
    }
  }
}
```

### Access Control
```yaml
# Prometheus configuration with basic auth
global:
  external_labels:
    monitor: 'production'

web:
  basic_auth_users:
    admin: '$2b$12$hNf2lSsxfm0.i4a.1kVpSOVyBCfIB51VRjgBUyv6kdnyTlgWj81Ay'
```

## Troubleshooting

### Common Issues

#### Connection Failed
**Problem**: Cannot connect to Prometheus server
**Solution**:
```bash
# Test Prometheus connectivity
curl http://localhost:9090/api/v1/status/config

# Check Prometheus status
curl http://localhost:9090/api/v1/status/buildinfo

# Verify network access
telnet prometheus-server 9090
```

#### Query Timeout
**Problem**: PromQL queries timing out
**Solution**:
- Reduce query time range
- Optimize PromQL queries
- Increase timeout settings
- Check Prometheus performance

#### Authentication Failed
**Problem**: Authentication errors
**Solution**:
```bash
# Test authentication
curl -H "Authorization: Bearer $TOKEN" \
  http://prometheus:9090/api/v1/query?query=up

# Verify token validity
# Check token permissions
```

#### No Data Returned
**Problem**: Queries return empty results
**Solution**:
- Verify metric names: `curl http://prometheus:9090/api/v1/label/__name__/values`
- Check time ranges
- Validate PromQL syntax
- Ensure data is being scraped

### Diagnostic Commands
```bash
# Prometheus status
curl http://localhost:9090/api/v1/status/config
curl http://localhost:9090/api/v1/status/flags

# Available metrics
curl http://localhost:9090/api/v1/label/__name__/values

# Query validation
curl -G http://localhost:9090/api/v1/query \
  --data-urlencode 'query=up'
```

## Advanced Configuration

### Custom Metrics Collection
```yaml
# Custom scrape configuration
scrape_configs:
  - job_name: 'custom-app'
    static_configs:
      - targets: ['app1:8080', 'app2:8080']
    metrics_path: '/metrics'
    scrape_interval: 30s
    scrape_timeout: 10s
```

### Alert Rules
```yaml
# alert_rules.yml
groups:
  - name: example
    rules:
    - alert: HighCPUUsage
      expr: cpu_usage_percent > 80
      for: 5m
      labels:
        severity: warning
      annotations:
        summary: "High CPU usage detected"
        description: "CPU usage is above 80% for more than 5 minutes"
```

### Recording Rules
```yaml
# recording_rules.yml
groups:
  - name: performance
    interval: 30s
    rules:
    - record: job:http_requests:rate5m
      expr: sum(rate(http_requests_total[5m])) by (job)
    
    - record: job:http_request_duration:p95
      expr: histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (job, le))
```

## PromQL Examples

### Basic Queries
```promql
# Current CPU usage
cpu_usage_percent

# Memory usage by instance
memory_usage_bytes{instance="web-server-1"}

# HTTP request rate
rate(http_requests_total[5m])

# Error rate percentage
rate(http_requests_total{status=~"5.."}[5m]) / rate(http_requests_total[5m]) * 100
```

### Advanced Queries
```promql
# Top 10 CPU consumers
topk(10, cpu_usage_percent)

# 95th percentile response time
histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))

# Disk space prediction
predict_linear(disk_free_bytes[1h], 4 * 3600) < 0

# Service availability
avg_over_time(up{job="web-service"}[24h]) * 100
```

### Aggregation Queries
```promql
# Total requests per service
sum(rate(http_requests_total[5m])) by (service)

# Average response time by endpoint
avg(http_request_duration_seconds) by (endpoint)

# Maximum memory usage across instances
max(memory_usage_bytes) by (application)
```

## Integration with Other MCPs

### With Kubernetes MCP
```
# Container monitoring workflow
1. Use kubernetes MCP to deploy applications
2. Use prometheus MCP to monitor metrics
3. Set up alerts for pod health
4. Scale based on metrics
```

### With Grafana Integration
```
# Visualization workflow
1. Query metrics with prometheus MCP
2. Create dashboard configurations
3. Set up automated reporting
4. Share insights with teams
```

## Monitoring Examples

### Application Performance Monitoring
```promql
# Application metrics
- Request rate: rate(http_requests_total[5m])
- Error rate: rate(http_requests_total{status=~"5.."}[5m])
- Response time: histogram_quantile(0.95, http_request_duration_seconds_bucket)
- Throughput: sum(rate(http_requests_total[5m]))
```

### Infrastructure Monitoring
```promql
# System metrics
- CPU usage: 100 - (avg(irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
- Memory usage: (1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100
- Disk usage: (1 - (node_filesystem_avail_bytes / node_filesystem_size_bytes)) * 100
- Network I/O: rate(node_network_receive_bytes_total[5m])
```

### Business Metrics
```promql
# Business KPIs
- User registrations: increase(user_registrations_total[1d])
- Revenue: sum(order_value_total)
- Conversion rate: user_conversions_total / user_visits_total * 100
- Active users: count(user_last_seen_timestamp > (time() - 3600))
```

## Links

- [Prometheus MCP Repository](https://github.com/prometheus-mcp/mcp-server-prometheus)
- [Prometheus Documentation](https://prometheus.io/docs/)
- [PromQL Documentation](https://prometheus.io/docs/prometheus/latest/querying/)
- [Prometheus API Reference](https://prometheus.io/docs/prometheus/latest/querying/api/)
- [Alerting Rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)
- [Recording Rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Prometheus Community](https://prometheus.io/community/)
- [Prometheus Mailing List](https://groups.google.com/forum/#!forum/prometheus-users)
- [MCP Discord](https://discord.gg/mcp)
- [Awesome Prometheus](https://github.com/roaldnefs/awesome-prometheus)
- [Prometheus Best Practices](https://prometheus.io/docs/practices/)

