# MongoDB MCP

## Overview
The MongoDB MCP provides Claude with comprehensive MongoDB database integration capabilities, enabling natural language document operations, aggregation pipelines, schema analysis, and NoSQL data management. This MCP is essential for modern applications using document-based databases and flexible data structures.

## Installation

### Prerequisites
- MongoDB server running and accessible (Atlas or self-hosted)
- MongoDB connection string and credentials
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Network access to MongoDB cluster

### Install Steps

#### Option 1: Official MongoDB MCP
```bash
npx @mongodb-js/mongodb-mcp-server
```

#### Option 2: Via Smithery
```bash
npx -y @smithery/cli install @mongodb-js/mongodb-mcp-server --client claude
```

#### Option 3: Community Implementation
```bash
git clone https://github.com/QuantGeekDev/mongo-mcp.git
cd mongo-mcp
npm install
npm run build
```

#### Option 4: Docker Container
```bash
docker run -d --name mongodb-mcp \
  -e MONGODB_URI="mongodb://localhost:27017/mydb" \
  mongodb-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "mongodb": {
      "command": "npx",
      "args": [
        "@mongodb-js/mongodb-mcp-server",
        "--connection-string", "mongodb://localhost:27017/mydb"
      ]
    }
  }
}
```

### MongoDB Atlas Configuration
```json
{
  "mcpServers": {
    "mongodb": {
      "command": "npx",
      "args": [
        "@mongodb-js/mongodb-mcp-server",
        "--connection-string", "mongodb+srv://username:password@cluster.mongodb.net/database"
      ]
    }
  }
}
```

### With Environment Variables
```json
{
  "mcpServers": {
    "mongodb": {
      "command": "npx",
      "args": ["@mongodb-js/mongodb-mcp-server"],
      "env": {
        "MONGODB_URI": "mongodb://localhost:27017/mydb",
        "MONGODB_DATABASE": "myapp",
        "MONGODB_OPTIONS": "retryWrites=true&w=majority"
      }
    }
  }
}
```

### Multiple Database Connections
```json
{
  "mcpServers": {
    "mongodb-prod": {
      "command": "npx",
      "args": ["@mongodb-js/mongodb-mcp-server"],
      "env": {
        "MONGODB_URI": "mongodb+srv://prod-user:${MONGODB_PROD_PASSWORD}@prod-cluster.mongodb.net/production"
      }
    },
    "mongodb-dev": {
      "command": "npx",
      "args": ["@mongodb-js/mongodb-mcp-server"],
      "env": {
        "MONGODB_URI": "mongodb://localhost:27017/development"
      }
    }
  }
}
```

## Usage Examples

### Basic Document Operations
```
# Find documents
Show me all users in the users collection.

# Insert documents
Add a new user with name "John Doe", email "john@example.com", and age 30.

# Update documents
Update the email address for user with _id "507f1f77bcf86cd799439011".

# Delete documents
Remove all inactive users from the users collection.

# Count documents
How many orders were placed in the last 30 days?
```

### Advanced Queries
```
# Complex filtering
Find all products with price between $50 and $200 and category "electronics".

# Array operations
Find all users who have "javascript" in their skills array.

# Nested document queries
Find all orders where the shipping address city is "New York".

# Text search
Search for products containing "wireless" in the name or description.

# Geospatial queries
Find all stores within 10 miles of coordinates [40.7128, -74.0060].
```

### Aggregation Pipelines
```
# Group and count
Group orders by customer and calculate total order value for each.

# Date aggregation
Show monthly sales totals for the last 12 months.

# Complex aggregation
Calculate average rating by product category with minimum 10 reviews.

# Lookup operations
Join orders with customer information and product details.

# Pipeline optimization
Create an optimized aggregation pipeline for sales reporting.
```

### Schema Analysis
```
# Collection structure
Analyze the structure of the products collection and show field types.

# Index analysis
Show all indexes on the users collection and their usage statistics.

# Data validation
Check for documents that don't match the expected schema in orders collection.

# Field analysis
Analyze the distribution of values in the "status" field across all orders.

# Collection statistics
Show storage statistics and document count for all collections.
```

## Features

### Core MongoDB Operations
- **CRUD Operations**: Create, Read, Update, Delete operations on documents
- **Query Operations**: Complex queries with filters, sorting, and pagination
- **Aggregation Framework**: Advanced data processing and analysis pipelines
- **Index Management**: Create, analyze, and optimize database indexes
- **Collection Management**: Create, modify, and manage collections

### Advanced Features
- **Text Search**: Full-text search capabilities across documents
- **Geospatial Queries**: Location-based queries and spatial operations
- **GridFS**: Large file storage and retrieval operations
- **Change Streams**: Real-time data change monitoring
- **Transactions**: Multi-document ACID transactions

### Data Analysis Capabilities
- **Aggregation Pipelines**: Complex data transformation and analysis
- **MapReduce**: Large-scale data processing operations
- **Statistical Functions**: Data distribution and statistical calculations
- **Time Series**: Time-based data analysis and trending
- **Graph Operations**: Relationship analysis and graph traversal

### Integration Features
- **MongoDB Atlas**: Cloud database integration
- **Replica Sets**: High availability and read scaling
- **Sharding**: Horizontal scaling across multiple servers
- **Authentication**: Various authentication mechanisms
- **SSL/TLS**: Secure connections and data encryption

## Requirements

### System Requirements
- **MongoDB**: Version 4.4 or higher (6.0+ recommended)
- **Operating System**: Linux, macOS, or Windows
- **Memory**: 1GB+ available RAM
- **Network**: TCP/IP connectivity to MongoDB server
- **Storage**: Varies by data size and indexes

### MongoDB Configuration
```javascript
// MongoDB connection options
const options = {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  maxPoolSize: 10,
  serverSelectionTimeoutMS: 5000,
  socketTimeoutMS: 45000,
  bufferMaxEntries: 0,
  retryWrites: true,
  w: 'majority'
};
```

### Atlas Configuration
```javascript
// MongoDB Atlas connection
const atlasUri = "mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<database>?retryWrites=true&w=majority";

// Connection with options
const atlasOptions = {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  ssl: true,
  sslValidate: true,
  authSource: 'admin'
};
```

## Security Considerations

### Best Practices
- **Authentication**: Use strong authentication mechanisms
- **Authorization**: Implement role-based access control
- **Encryption**: Use SSL/TLS for data in transit
- **Network Security**: Restrict database access to trusted networks
- **Regular Updates**: Keep MongoDB updated with security patches

### Secure Configuration
```json
{
  "mcpServers": {
    "mongodb": {
      "command": "npx",
      "args": ["@mongodb-js/mongodb-mcp-server"],
      "env": {
        "MONGODB_URI": "mongodb+srv://readonly:${MONGODB_PASSWORD}@cluster.mongodb.net/mydb?ssl=true&authSource=admin",
        "MONGODB_READ_ONLY": "true"
      }
    }
  }
}
```

### Access Control
```javascript
// Create database users with specific roles
db.createUser({
  user: "mcp_analyst",
  pwd: "secure_password",
  roles: [
    { role: "read", db: "analytics" },
    { role: "read", db: "reporting" }
  ]
});

db.createUser({
  user: "mcp_developer",
  pwd: "secure_password",
  roles: [
    { role: "readWrite", db: "development" },
    { role: "dbAdmin", db: "development" }
  ]
});
```

## Troubleshooting

### Common Issues

#### Connection Failed
**Problem**: Cannot connect to MongoDB server
**Solution**:
```bash
# Test MongoDB connectivity
mongosh "mongodb://localhost:27017/mydb"

# Check MongoDB service status
sudo systemctl status mongod

# Verify network connectivity
telnet hostname 27017
```

#### Authentication Failed
**Problem**: Invalid credentials or permissions
**Solution**:
```javascript
// Check user permissions
db.runCommand({usersInfo: "username"});

// Test authentication
db.auth("username", "password");

// Check database access
show dbs;
use mydb;
show collections;
```

#### Query Performance Issues
**Problem**: Slow query execution
**Solution**:
```javascript
// Enable profiler
db.setProfilingLevel(2);

// Analyze query performance
db.collection.find({field: "value"}).explain("executionStats");

// Check indexes
db.collection.getIndexes();

// Create appropriate indexes
db.collection.createIndex({field: 1});
```

#### Memory Issues
**Problem**: High memory usage
**Solution**:
```javascript
// Check server status
db.serverStatus().mem;

// Monitor connections
db.serverStatus().connections;

// Check collection statistics
db.collection.stats();

// Optimize queries and indexes
db.collection.find().limit(100);
```

### Diagnostic Commands
```javascript
// Server status
db.serverStatus();

// Database statistics
db.stats();

// Collection statistics
db.collection.stats();

// Current operations
db.currentOp();

// Replica set status
rs.status();
```

## Advanced Configuration

### Index Optimization
```javascript
// Compound indexes
db.products.createIndex({category: 1, price: -1});

// Text indexes
db.products.createIndex({
  name: "text",
  description: "text"
}, {
  weights: {name: 10, description: 5}
});

// Geospatial indexes
db.stores.createIndex({location: "2dsphere"});

// Partial indexes
db.users.createIndex(
  {email: 1},
  {partialFilterExpression: {active: true}}
);

// TTL indexes
db.sessions.createIndex(
  {createdAt: 1},
  {expireAfterSeconds: 3600}
);
```

### Aggregation Pipelines
```javascript
// Sales analysis pipeline
db.orders.aggregate([
  {
    $match: {
      orderDate: {
        $gte: new Date("2024-01-01"),
        $lt: new Date("2024-12-31")
      }
    }
  },
  {
    $group: {
      _id: {
        year: {$year: "$orderDate"},
        month: {$month: "$orderDate"}
      },
      totalSales: {$sum: "$totalAmount"},
      orderCount: {$sum: 1},
      avgOrderValue: {$avg: "$totalAmount"}
    }
  },
  {
    $sort: {"_id.year": 1, "_id.month": 1}
  }
]);

// Customer analytics pipeline
db.orders.aggregate([
  {
    $lookup: {
      from: "customers",
      localField: "customerId",
      foreignField: "_id",
      as: "customer"
    }
  },
  {
    $unwind: "$customer"
  },
  {
    $group: {
      _id: "$customer.segment",
      totalRevenue: {$sum: "$totalAmount"},
      customerCount: {$addToSet: "$customerId"},
      avgOrderValue: {$avg: "$totalAmount"}
    }
  },
  {
    $addFields: {
      customerCount: {$size: "$customerCount"}
    }
  }
]);
```

### Schema Validation
```javascript
// Create collection with schema validation
db.createCollection("products", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "price", "category"],
      properties: {
        name: {
          bsonType: "string",
          description: "Product name is required and must be a string"
        },
        price: {
          bsonType: "number",
          minimum: 0,
          description: "Price must be a positive number"
        },
        category: {
          bsonType: "string",
          enum: ["electronics", "clothing", "books", "home"],
          description: "Category must be one of the predefined values"
        },
        tags: {
          bsonType: "array",
          items: {
            bsonType: "string"
          },
          description: "Tags must be an array of strings"
        }
      }
    }
  }
});
```

## Query Examples

### Basic Queries
```javascript
// Find with conditions
db.users.find({age: {$gte: 18, $lt: 65}});

// Find with array conditions
db.users.find({skills: {$in: ["javascript", "python"]}});

// Find nested documents
db.orders.find({"shipping.address.city": "New York"});

// Find with regex
db.products.find({name: {$regex: /wireless/i}});

// Find with date range
db.orders.find({
  orderDate: {
    $gte: new Date("2024-01-01"),
    $lt: new Date("2024-12-31")
  }
});
```

### Advanced Aggregations
```javascript
// Time series analysis
db.sales.aggregate([
  {
    $group: {
      _id: {
        $dateToString: {
          format: "%Y-%m-%d",
          date: "$timestamp"
        }
      },
      dailySales: {$sum: "$amount"},
      transactionCount: {$sum: 1}
    }
  },
  {
    $sort: {_id: 1}
  }
]);

// Geospatial aggregation
db.stores.aggregate([
  {
    $geoNear: {
      near: {type: "Point", coordinates: [-74.0060, 40.7128]},
      distanceField: "distance",
      maxDistance: 10000,
      spherical: true
    }
  },
  {
    $group: {
      _id: "$chain",
      storeCount: {$sum: 1},
      avgDistance: {$avg: "$distance"}
    }
  }
]);

// Complex lookup with pipeline
db.orders.aggregate([
  {
    $lookup: {
      from: "products",
      let: {orderItems: "$items"},
      pipeline: [
        {
          $match: {
            $expr: {
              $in: ["$_id", "$$orderItems.productId"]
            }
          }
        },
        {
          $project: {name: 1, category: 1, price: 1}
        }
      ],
      as: "productDetails"
    }
  }
]);
```

## Integration with Other MCPs

### With Elasticsearch MCP
```
# Search and analytics workflow
1. Use mongodb MCP for operational data storage
2. Use elasticsearch MCP for full-text search
3. Sync data between MongoDB and Elasticsearch
4. Implement hybrid search capabilities
```

### With Redis MCP
```
# Caching strategy
1. Use mongodb MCP for persistent data storage
2. Use redis MCP for caching frequently accessed data
3. Implement cache-aside pattern
4. Monitor cache hit rates and performance
```

### With Grafana MCP
```
# Monitoring and visualization
1. Use mongodb MCP to query application metrics
2. Use grafana MCP to create monitoring dashboards
3. Set up alerts for database performance
4. Visualize business metrics and trends
```

## Workflow Examples

### Data Migration
```
1. Analyze source data structure
2. Design MongoDB document schema
3. Create migration scripts
4. Execute data transformation
5. Validate migrated data
6. Update application configurations
```

### Performance Optimization
```
1. Identify slow queries using profiler
2. Analyze query execution plans
3. Create appropriate indexes
4. Optimize aggregation pipelines
5. Monitor performance improvements
6. Document optimization strategies
```

### Real-time Analytics
```
1. Set up change streams for real-time data
2. Create aggregation pipelines for analytics
3. Implement data processing workflows
4. Build real-time dashboards
5. Set up alerting for anomalies
6. Monitor system performance
```

## Links

- [Official MongoDB MCP](https://github.com/mongodb-js/mongodb-mcp-server)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [MongoDB University](https://university.mongodb.com/)
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
- [Aggregation Framework](https://docs.mongodb.com/manual/aggregation/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [MongoDB Community](https://www.mongodb.com/community)
- [MongoDB Forums](https://developer.mongodb.com/community/forums/)
- [MCP Discord](https://discord.gg/mcp)
- [Stack Overflow MongoDB](https://stackoverflow.com/questions/tagged/mongodb)
- [MongoDB Best Practices](https://docs.mongodb.com/manual/administration/production-notes/)

