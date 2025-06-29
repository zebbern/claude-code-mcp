# Elasticsearch MCP

## Overview
The Elasticsearch MCP provides Claude with comprehensive search, analytics, and data management capabilities for Elasticsearch clusters. This MCP enables full-text search, log analysis, real-time analytics, and data visualization workflows, making it essential for observability, business intelligence, and data-driven applications.

## Installation

### Prerequisites
- Elasticsearch cluster running and accessible
- Elasticsearch credentials or API keys
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Network access to Elasticsearch cluster

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx elasticsearch-mcp-server
```

#### Option 2: From GitHub
```bash
git clone https://github.com/elasticsearch-mcp/elasticsearch-mcp-server.git
cd elasticsearch-mcp-server
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install elasticsearch-mcp-server
```

#### Option 4: Docker Container
```bash
docker run -d --name elasticsearch-mcp \
  -e ELASTICSEARCH_URL=http://elasticsearch:9200 \
  -e ELASTICSEARCH_USERNAME=elastic \
  -e ELASTICSEARCH_PASSWORD=password \
  elasticsearch-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "elasticsearch": {
      "command": "npx",
      "args": [
        "elasticsearch-mcp-server",
        "--url", "http://localhost:9200"
      ]
    }
  }
}
```

### With Authentication
```json
{
  "mcpServers": {
    "elasticsearch": {
      "command": "npx",
      "args": [
        "elasticsearch-mcp-server",
        "--url", "https://elasticsearch.example.com:9200",
        "--username", "elastic",
        "--password", "${ELASTICSEARCH_PASSWORD}",
        "--verify-ssl"
      ]
    }
  }
}
```

### With API Key Authentication
```json
{
  "mcpServers": {
    "elasticsearch": {
      "command": "npx",
      "args": [
        "elasticsearch-mcp-server",
        "--url", "https://elasticsearch.example.com:9200",
        "--api-key", "${ELASTICSEARCH_API_KEY}"
      ]
    }
  }
}
```

### Multiple Clusters
```json
{
  "mcpServers": {
    "elasticsearch-prod": {
      "command": "npx",
      "args": [
        "elasticsearch-mcp-server",
        "--url", "https://es-prod.example.com:9200",
        "--api-key", "${ES_PROD_API_KEY}"
      ]
    },
    "elasticsearch-logs": {
      "command": "npx",
      "args": [
        "elasticsearch-mcp-server",
        "--url", "https://es-logs.example.com:9200",
        "--api-key", "${ES_LOGS_API_KEY}"
      ]
    }
  }
}
```

## Usage Examples

### Search Operations
```
# Basic search
Search for documents containing "error" in the logs index.

# Advanced search
Find all HTTP 500 errors in the last 24 hours from the web-logs index.

# Aggregation queries
Show me the top 10 IP addresses by request count in the access logs.

# Full-text search
Search for documents containing "authentication failed" across all indices.

# Filtered search
Find all documents where status is "error" and timestamp is within the last hour.
```

### Index Management
```
# List indices
Show me all indices in the Elasticsearch cluster.

# Create index
Create a new index called "application-logs" with appropriate mappings.

# Delete index
Delete the old "deprecated-logs" index.

# Index statistics
Show me statistics for the "web-logs" index including document count and size.

# Index mappings
Display the field mappings for the "user-events" index.
```

### Document Operations
```
# Index documents
Add this JSON document to the "products" index.

# Get document
Retrieve the document with ID "12345" from the "users" index.

# Update document
Update the "status" field to "active" for document ID "67890" in the "orders" index.

# Delete document
Remove the document with ID "abc123" from the "temp-data" index.

# Bulk operations
Perform bulk indexing of these 1000 documents into the "events" index.
```

### Analytics & Aggregations
```
# Time-based analytics
Show me the hourly distribution of log events over the last 7 days.

# Statistical analysis
Calculate average, min, max response times for API endpoints.

# Geospatial analysis
Find all events within 50km of New York City coordinates.

# Terms aggregation
Show me the top 20 user agents from web access logs.

# Date histogram
Create a daily breakdown of error counts for the last month.
```

## Features

### Core Elasticsearch Operations
- **Search Queries**: Full-text search, term queries, and complex boolean queries
- **Index Management**: Create, delete, and configure indices and mappings
- **Document Operations**: CRUD operations on individual documents
- **Bulk Operations**: Efficient batch processing of multiple documents
- **Cluster Management**: Monitor cluster health and node status

### Advanced Search Features
- **Query DSL**: Support for Elasticsearch's full Query DSL
- **Aggregations**: Statistical, bucket, and pipeline aggregations
- **Highlighting**: Search result highlighting and snippets
- **Suggestions**: Auto-complete and spell correction
- **Percolator**: Reverse search and alerting queries

### Analytics Capabilities
- **Time Series Analysis**: Time-based data analysis and visualization
- **Geospatial Queries**: Location-based search and analysis
- **Machine Learning**: Anomaly detection and forecasting (X-Pack)
- **Graph Analytics**: Relationship and network analysis
- **Custom Scoring**: Advanced relevance scoring algorithms

### Data Management
- **Index Templates**: Automated index configuration
- **Index Lifecycle Management**: Automated data retention policies
- **Snapshots**: Backup and restore operations
- **Cross-Cluster Search**: Federated search across clusters
- **Data Streams**: Time-series data management

## Requirements

### System Requirements
- **Elasticsearch**: Version 7.0 or higher (8.0+ recommended)
- **Operating System**: Linux, macOS, or Windows
- **Memory**: 1GB+ available RAM
- **Network**: HTTP/HTTPS access to Elasticsearch cluster
- **Java**: OpenJDK 11+ (for Elasticsearch server)

### Elasticsearch Configuration
```yaml
# elasticsearch.yml
cluster.name: my-application
node.name: node-1
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: 0.0.0.0
http.port: 9200
discovery.seed_hosts: ["host1", "host2"]
cluster.initial_master_nodes: ["node-1", "node-2"]

# Security settings
xpack.security.enabled: true
xpack.security.transport.ssl.enabled: true
xpack.security.http.ssl.enabled: true
```

### Network Access
- HTTP/HTTPS access to Elasticsearch cluster (port 9200)
- Authentication credentials or API keys
- SSL/TLS certificates for secure connections
- Firewall rules for cluster communication

## Security Considerations

### Best Practices
- **Authentication**: Use strong authentication mechanisms
- **Authorization**: Implement role-based access control
- **Encryption**: Enable SSL/TLS for data in transit
- **API Keys**: Use API keys with minimal required permissions
- **Network Security**: Restrict network access to trusted sources

### Secure Configuration
```json
{
  "mcpServers": {
    "elasticsearch": {
      "command": "npx",
      "args": [
        "elasticsearch-mcp-server",
        "--url", "https://elasticsearch.example.com:9200",
        "--api-key", "${ELASTICSEARCH_API_KEY}",
        "--verify-ssl",
        "--timeout", "30s"
      ]
    }
  }
}
```

### Role-Based Access Control
```json
{
  "role_name": "mcp_user",
  "cluster": ["monitor"],
  "indices": [
    {
      "names": ["logs-*", "metrics-*"],
      "privileges": ["read", "view_index_metadata"]
    },
    {
      "names": ["application-*"],
      "privileges": ["read", "write", "create_index"]
    }
  ]
}
```

## Troubleshooting

### Common Issues

#### Connection Failed
**Problem**: Cannot connect to Elasticsearch cluster
**Solution**:
```bash
# Test Elasticsearch connectivity
curl -X GET "localhost:9200/"

# Check cluster health
curl -X GET "localhost:9200/_cluster/health"

# Verify authentication
curl -u elastic:password -X GET "localhost:9200/_security/_authenticate"
```

#### Authentication Failed
**Problem**: Invalid credentials or API key
**Solution**:
```bash
# Test API key
curl -H "Authorization: ApiKey $API_KEY" \
  -X GET "localhost:9200/_security/_authenticate"

# Generate new API key
curl -u elastic:password -X POST "localhost:9200/_security/api_key" \
  -H "Content-Type: application/json" \
  -d '{"name": "mcp-key", "expiration": "1d"}'
```

#### Index Not Found
**Problem**: Specified index does not exist
**Solution**:
```bash
# List all indices
curl -X GET "localhost:9200/_cat/indices?v"

# Check index existence
curl -X HEAD "localhost:9200/my-index"

# Create index if needed
curl -X PUT "localhost:9200/my-index"
```

#### Query Performance Issues
**Problem**: Slow query execution
**Solution**:
- Use filters instead of queries when possible
- Optimize mapping and field types
- Use appropriate shard and replica settings
- Monitor cluster performance metrics

### Diagnostic Commands
```bash
# Cluster information
curl -X GET "localhost:9200/_cluster/stats"

# Node information
curl -X GET "localhost:9200/_nodes/stats"

# Index statistics
curl -X GET "localhost:9200/_stats"

# Search performance
curl -X GET "localhost:9200/_search?explain=true"
```

## Advanced Configuration

### Index Templates
```json
{
  "index_patterns": ["logs-*"],
  "template": {
    "settings": {
      "number_of_shards": 1,
      "number_of_replicas": 1,
      "index.refresh_interval": "30s"
    },
    "mappings": {
      "properties": {
        "@timestamp": {
          "type": "date"
        },
        "level": {
          "type": "keyword"
        },
        "message": {
          "type": "text",
          "analyzer": "standard"
        },
        "host": {
          "type": "keyword"
        }
      }
    }
  }
}
```

### Index Lifecycle Management
```json
{
  "policy": {
    "phases": {
      "hot": {
        "actions": {
          "rollover": {
            "max_size": "50GB",
            "max_age": "30d"
          }
        }
      },
      "warm": {
        "min_age": "30d",
        "actions": {
          "allocate": {
            "number_of_replicas": 0
          }
        }
      },
      "cold": {
        "min_age": "90d",
        "actions": {
          "allocate": {
            "number_of_replicas": 0
          }
        }
      },
      "delete": {
        "min_age": "365d"
      }
    }
  }
}
```

### Custom Analyzers
```json
{
  "settings": {
    "analysis": {
      "analyzer": {
        "custom_analyzer": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "stop",
            "snowball"
          ]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "content": {
        "type": "text",
        "analyzer": "custom_analyzer"
      }
    }
  }
}
```

## Query Examples

### Basic Queries
```json
{
  "query": {
    "match": {
      "message": "error"
    }
  }
}

{
  "query": {
    "range": {
      "@timestamp": {
        "gte": "now-1h"
      }
    }
  }
}

{
  "query": {
    "bool": {
      "must": [
        {"term": {"status": "error"}},
        {"range": {"@timestamp": {"gte": "now-24h"}}}
      ]
    }
  }
}
```

### Aggregation Queries
```json
{
  "aggs": {
    "status_counts": {
      "terms": {
        "field": "status.keyword"
      }
    }
  }
}

{
  "aggs": {
    "hourly_counts": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "hour"
      }
    }
  }
}

{
  "aggs": {
    "avg_response_time": {
      "avg": {
        "field": "response_time"
      }
    }
  }
}
```

### Complex Analytics
```json
{
  "aggs": {
    "top_ips": {
      "terms": {
        "field": "client_ip.keyword",
        "size": 10
      },
      "aggs": {
        "avg_response_time": {
          "avg": {
            "field": "response_time"
          }
        },
        "error_rate": {
          "filter": {
            "range": {
              "status": {"gte": 400}
            }
          }
        }
      }
    }
  }
}
```

## Integration with Other MCPs

### With Prometheus MCP
```
# Observability workflow
1. Use prometheus MCP for metrics collection
2. Use elasticsearch MCP for log analysis
3. Correlate metrics and logs for troubleshooting
4. Create comprehensive monitoring dashboards
```

### With Grafana MCP
```
# Visualization workflow
1. Use elasticsearch MCP to query log data
2. Use grafana MCP to create log dashboards
3. Set up alerts based on log patterns
4. Share insights with development teams
```

### With Kubernetes MCP
```
# Container logging
1. Use kubernetes MCP to manage applications
2. Use elasticsearch MCP to analyze container logs
3. Monitor application performance and errors
4. Implement centralized logging strategy
```

## Workflow Examples

### Log Analysis
```
1. Ingest logs from multiple sources
2. Parse and structure log data
3. Create search queries for troubleshooting
4. Set up alerts for critical errors
5. Generate reports and dashboards
```

### Business Intelligence
```
1. Index business data and events
2. Create analytical queries and aggregations
3. Build real-time dashboards
4. Monitor KPIs and trends
5. Generate automated reports
```

### Security Monitoring
```
1. Collect security logs and events
2. Analyze patterns and anomalies
3. Create threat detection rules
4. Monitor compliance requirements
5. Generate security reports
```

## Links

- [Elasticsearch MCP Repository](https://github.com/elasticsearch-mcp/elasticsearch-mcp-server)
- [Elasticsearch Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/)
- [Elasticsearch Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html)
- [Elasticsearch APIs](https://www.elastic.co/guide/en/elasticsearch/reference/current/rest-apis.html)
- [Elastic Stack](https://www.elastic.co/elastic-stack/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Elastic Community](https://www.elastic.co/community)
- [Elasticsearch Discuss](https://discuss.elastic.co/)
- [MCP Discord](https://discord.gg/mcp)
- [Awesome Elasticsearch](https://github.com/dzharii/awesome-elasticsearch)
- [Elasticsearch Best Practices](https://www.elastic.co/guide/en/elasticsearch/reference/current/best-practices.html)

