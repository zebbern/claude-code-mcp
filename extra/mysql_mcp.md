# MySQL MCP

## Overview
The MySQL MCP provides Claude with comprehensive MySQL database integration capabilities, enabling natural language database interactions, SQL query execution, schema management, and data analysis. This MCP is essential for database-driven applications and data management workflows.

## Installation

### Prerequisites
- MySQL server running and accessible
- MySQL client libraries installed
- Database credentials and permissions
- Node.js 16+ or Python 3.8+
- Claude Desktop application

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx @meanands/mysql-mcp
```

#### Option 2: Via Smithery
```bash
npx -y @smithery/cli install @meanands/mysql-mcp --client claude
```

#### Option 3: From GitHub
```bash
git clone https://github.com/benborla/mcp-server-mysql.git
cd mcp-server-mysql
npm install
npm run build
```

#### Option 4: Python Implementation
```bash
pip install mysql-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": [
        "@meanands/mysql-mcp",
        "--host", "localhost",
        "--port", "3306",
        "--user", "username",
        "--password", "password",
        "--database", "mydb"
      ]
    }
  }
}
```

### With Environment Variables
```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": ["@meanands/mysql-mcp"],
      "env": {
        "MYSQL_HOST": "localhost",
        "MYSQL_PORT": "3306",
        "MYSQL_USER": "username",
        "MYSQL_PASSWORD": "password",
        "MYSQL_DATABASE": "mydb"
      }
    }
  }
}
```

### Multiple Database Connections
```json
{
  "mcpServers": {
    "mysql-prod": {
      "command": "npx",
      "args": [
        "@meanands/mysql-mcp",
        "--host", "prod-db.example.com",
        "--database", "production"
      ],
      "env": {
        "MYSQL_USER": "prod_user",
        "MYSQL_PASSWORD": "${MYSQL_PROD_PASSWORD}"
      }
    },
    "mysql-dev": {
      "command": "npx",
      "args": [
        "@meanands/mysql-mcp",
        "--host", "localhost",
        "--database", "development"
      ],
      "env": {
        "MYSQL_USER": "dev_user",
        "MYSQL_PASSWORD": "${MYSQL_DEV_PASSWORD}"
      }
    }
  }
}
```

### SSL Configuration
```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": [
        "@meanands/mysql-mcp",
        "--host", "secure-db.example.com",
        "--ssl-ca", "/path/to/ca.pem",
        "--ssl-cert", "/path/to/client-cert.pem",
        "--ssl-key", "/path/to/client-key.pem"
      ]
    }
  }
}
```

## Usage Examples

### Basic Database Operations
```
# Query data
Show me all users from the users table.

# Insert data
Add a new user with name "John Doe" and email "john@example.com" to the users table.

# Update records
Update the email address for user ID 123 to "newemail@example.com".

# Delete records
Remove all inactive users from the users table.

# Count records
How many orders were placed in the last 30 days?
```

### Advanced Queries
```
# Join operations
Show me all orders with customer information for orders placed this month.

# Aggregation queries
Calculate the total revenue by product category for the last quarter.

# Subqueries
Find all customers who have placed orders worth more than $1000.

# Window functions
Show the running total of sales for each month this year.

# Complex filtering
Find all products that are low in stock and have been ordered in the last week.
```

### Schema Management
```
# Table structure
Show me the structure of the products table.

# Create tables
Create a new table called "reviews" with columns for id, product_id, rating, and comment.

# Modify tables
Add a new column "created_at" to the users table.

# Index management
Create an index on the email column of the users table.

# Foreign keys
Add a foreign key constraint linking orders.customer_id to customers.id.
```

### Data Analysis
```
# Statistical analysis
Calculate average, min, max order values by customer segment.

# Trend analysis
Show me the monthly sales trend for the last 12 months.

# Performance analysis
Identify the top 10 best-selling products this quarter.

# Customer analysis
Find customers who haven't placed an order in the last 6 months.

# Inventory analysis
Show products that are running low in stock based on recent sales velocity.
```

## Features

### Core MySQL Operations
- **CRUD Operations**: Create, Read, Update, Delete operations on tables
- **Query Execution**: Execute complex SQL queries with natural language
- **Transaction Management**: Handle database transactions and rollbacks
- **Schema Operations**: Create, modify, and manage database schemas
- **Index Management**: Create and optimize database indexes

### Advanced Features
- **Stored Procedures**: Execute and manage stored procedures
- **Views Management**: Create and manage database views
- **Triggers**: Handle database triggers and events
- **User Management**: Manage database users and permissions
- **Backup Operations**: Database backup and restore operations

### Data Analysis Capabilities
- **Aggregation Functions**: SUM, COUNT, AVG, MIN, MAX operations
- **Window Functions**: Advanced analytical functions
- **Statistical Analysis**: Data distribution and statistical calculations
- **Trend Analysis**: Time-series data analysis
- **Performance Metrics**: Query performance and optimization insights

### Integration Features
- **Multiple Connections**: Connect to multiple MySQL instances
- **SSL Support**: Secure connections with SSL/TLS
- **Connection Pooling**: Efficient connection management
- **Error Handling**: Comprehensive error handling and recovery
- **Logging**: Detailed query logging and audit trails

## Requirements

### System Requirements
- **MySQL Server**: Version 5.7 or higher (8.0+ recommended)
- **Operating System**: Linux, macOS, or Windows
- **Memory**: 512MB+ available RAM
- **Network**: TCP/IP connectivity to MySQL server
- **Storage**: Minimal local storage for caching

### MySQL Configuration
```sql
-- Create dedicated user for MCP
CREATE USER 'mcp_user'@'%' IDENTIFIED BY 'secure_password';

-- Grant appropriate permissions
GRANT SELECT, INSERT, UPDATE, DELETE ON mydb.* TO 'mcp_user'@'%';
GRANT CREATE, ALTER, DROP ON mydb.* TO 'mcp_user'@'%';
GRANT EXECUTE ON mydb.* TO 'mcp_user'@'%';

-- For read-only access
GRANT SELECT ON mydb.* TO 'mcp_readonly'@'%';

FLUSH PRIVILEGES;
```

### Network Configuration
```ini
# my.cnf configuration
[mysqld]
bind-address = 0.0.0.0
port = 3306
max_connections = 200
innodb_buffer_pool_size = 1G

# SSL configuration
ssl-ca = /path/to/ca.pem
ssl-cert = /path/to/server-cert.pem
ssl-key = /path/to/server-key.pem
```

## Security Considerations

### Best Practices
- **Least Privilege**: Grant minimal required permissions
- **SSL/TLS**: Use encrypted connections for remote databases
- **Strong Passwords**: Use complex passwords for database users
- **Network Security**: Restrict database access to trusted networks
- **Regular Updates**: Keep MySQL server updated with security patches

### Secure Configuration
```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": [
        "@meanands/mysql-mcp",
        "--host", "secure-db.example.com",
        "--ssl-mode", "REQUIRED",
        "--read-only", "true"
      ],
      "env": {
        "MYSQL_USER": "readonly_user",
        "MYSQL_PASSWORD": "${MYSQL_READONLY_PASSWORD}"
      }
    }
  }
}
```

### Access Control
```sql
-- Create role-based access
CREATE ROLE 'mcp_analyst';
GRANT SELECT ON analytics.* TO 'mcp_analyst';

CREATE ROLE 'mcp_developer';
GRANT SELECT, INSERT, UPDATE, DELETE ON development.* TO 'mcp_developer';

-- Assign roles to users
GRANT 'mcp_analyst' TO 'analyst_user'@'%';
GRANT 'mcp_developer' TO 'dev_user'@'%';
```

## Troubleshooting

### Common Issues

#### Connection Failed
**Problem**: Cannot connect to MySQL server
**Solution**:
```bash
# Test MySQL connectivity
mysql -h hostname -u username -p

# Check MySQL service status
sudo systemctl status mysql

# Verify network connectivity
telnet hostname 3306
```

#### Authentication Failed
**Problem**: Invalid credentials or permissions
**Solution**:
```sql
-- Check user permissions
SHOW GRANTS FOR 'username'@'hostname';

-- Reset password
ALTER USER 'username'@'hostname' IDENTIFIED BY 'new_password';

-- Check user existence
SELECT User, Host FROM mysql.user WHERE User = 'username';
```

#### Query Performance Issues
**Problem**: Slow query execution
**Solution**:
```sql
-- Enable slow query log
SET GLOBAL slow_query_log = 'ON';
SET GLOBAL long_query_time = 2;

-- Analyze query performance
EXPLAIN SELECT * FROM large_table WHERE condition;

-- Check indexes
SHOW INDEX FROM table_name;

-- Optimize table
OPTIMIZE TABLE table_name;
```

#### Connection Pool Exhaustion
**Problem**: Too many connections
**Solution**:
```sql
-- Check current connections
SHOW PROCESSLIST;

-- Check connection limits
SHOW VARIABLES LIKE 'max_connections';

-- Kill long-running queries
KILL CONNECTION_ID;
```

### Diagnostic Commands
```sql
-- Server status
SHOW STATUS;

-- Server variables
SHOW VARIABLES;

-- Process list
SHOW PROCESSLIST;

-- Database sizes
SELECT 
  table_schema AS 'Database',
  ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS 'Size (MB)'
FROM information_schema.tables
GROUP BY table_schema;
```

## Advanced Configuration

### Connection Pooling
```javascript
const poolConfig = {
  connectionLimit: 10,
  host: 'localhost',
  user: 'mcp_user',
  password: 'password',
  database: 'mydb',
  acquireTimeout: 60000,
  timeout: 60000,
  reconnect: true
};
```

### Query Optimization
```sql
-- Create indexes for better performance
CREATE INDEX idx_user_email ON users(email);
CREATE INDEX idx_order_date ON orders(order_date);
CREATE INDEX idx_product_category ON products(category_id);

-- Composite indexes
CREATE INDEX idx_order_customer_date ON orders(customer_id, order_date);

-- Full-text search indexes
CREATE FULLTEXT INDEX idx_product_search ON products(name, description);
```

### Stored Procedures
```sql
-- Example stored procedure for order processing
DELIMITER //
CREATE PROCEDURE ProcessOrder(
  IN customer_id INT,
  IN product_id INT,
  IN quantity INT,
  OUT order_id INT
)
BEGIN
  DECLARE EXIT HANDLER FOR SQLEXCEPTION
  BEGIN
    ROLLBACK;
    RESIGNAL;
  END;
  
  START TRANSACTION;
  
  INSERT INTO orders (customer_id, order_date, status)
  VALUES (customer_id, NOW(), 'pending');
  
  SET order_id = LAST_INSERT_ID();
  
  INSERT INTO order_items (order_id, product_id, quantity)
  VALUES (order_id, product_id, quantity);
  
  UPDATE products 
  SET stock_quantity = stock_quantity - quantity
  WHERE id = product_id;
  
  COMMIT;
END //
DELIMITER ;
```

## Query Examples

### Basic Queries
```sql
-- Select with conditions
SELECT * FROM users WHERE created_at > '2024-01-01';

-- Join operations
SELECT u.name, o.total_amount
FROM users u
JOIN orders o ON u.id = o.customer_id
WHERE o.order_date >= CURDATE() - INTERVAL 30 DAY;

-- Aggregation
SELECT 
  category,
  COUNT(*) as product_count,
  AVG(price) as avg_price
FROM products
GROUP BY category
ORDER BY avg_price DESC;
```

### Advanced Analytics
```sql
-- Window functions
SELECT 
  customer_id,
  order_date,
  total_amount,
  SUM(total_amount) OVER (
    PARTITION BY customer_id 
    ORDER BY order_date
  ) as running_total
FROM orders;

-- Common Table Expressions
WITH monthly_sales AS (
  SELECT 
    DATE_FORMAT(order_date, '%Y-%m') as month,
    SUM(total_amount) as sales
  FROM orders
  GROUP BY DATE_FORMAT(order_date, '%Y-%m')
)
SELECT 
  month,
  sales,
  LAG(sales) OVER (ORDER BY month) as prev_month_sales,
  sales - LAG(sales) OVER (ORDER BY month) as growth
FROM monthly_sales;

-- Recursive queries
WITH RECURSIVE category_hierarchy AS (
  SELECT id, name, parent_id, 0 as level
  FROM categories
  WHERE parent_id IS NULL
  
  UNION ALL
  
  SELECT c.id, c.name, c.parent_id, ch.level + 1
  FROM categories c
  JOIN category_hierarchy ch ON c.parent_id = ch.id
)
SELECT * FROM category_hierarchy ORDER BY level, name;
```

## Integration with Other MCPs

### With Grafana MCP
```
# Database monitoring workflow
1. Use mysql MCP to query performance metrics
2. Use grafana MCP to create monitoring dashboards
3. Set up alerts for database health
4. Visualize query performance trends
```

### With Git MCP
```
# Database schema versioning
1. Use git MCP to manage schema migrations
2. Use mysql MCP to apply database changes
3. Track schema evolution over time
4. Coordinate database and code deployments
```

### With Docker MCP
```
# Containerized database workflow
1. Use docker MCP to manage MySQL containers
2. Use mysql MCP to interact with containerized databases
3. Set up development and testing environments
4. Implement database backup strategies
```

## Workflow Examples

### Data Migration
```
1. Analyze source data structure
2. Design target schema
3. Create migration scripts
4. Execute data transformation
5. Validate migrated data
6. Update application configurations
```

### Performance Optimization
```
1. Identify slow queries
2. Analyze query execution plans
3. Create appropriate indexes
4. Optimize table structures
5. Monitor performance improvements
6. Document optimization strategies
```

### Business Intelligence
```
1. Design analytical queries
2. Create data aggregation views
3. Build reporting procedures
4. Schedule automated reports
5. Set up data quality checks
6. Maintain data documentation
```

## Links

- [MySQL MCP Repository](https://github.com/benborla/mcp-server-mysql)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [MySQL Performance Tuning](https://dev.mysql.com/doc/refman/8.0/en/optimization.html)
- [MySQL Security Guide](https://dev.mysql.com/doc/refman/8.0/en/security.html)
- [SQL Best Practices](https://dev.mysql.com/doc/refman/8.0/en/sql-syntax.html)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [MySQL Community](https://www.mysql.com/community/)
- [MySQL Forums](https://forums.mysql.com/)
- [MCP Discord](https://discord.gg/mcp)
- [Stack Overflow MySQL](https://stackoverflow.com/questions/tagged/mysql)
- [MySQL Best Practices](https://dev.mysql.com/doc/refman/8.0/en/best-practices.html)

