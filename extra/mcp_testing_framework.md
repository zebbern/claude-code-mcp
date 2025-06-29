# MCP Testing Framework

## Overview
The MCP Testing Framework provides comprehensive testing tools for Model Context Protocol implementations. This framework enables developers to create, run, and validate tests for custom MCPs, ensuring reliability, performance, and compatibility with Claude Code.

## Key Features

### 🧪 Comprehensive Testing Suite
- **Unit Testing**: Test individual MCP functions and methods
- **Integration Testing**: Validate MCP interactions with Claude Code
- **Performance Testing**: Measure response times and resource usage
- **Compatibility Testing**: Ensure MCP works across different environments

### 🔍 Advanced Validation
- **Schema Validation**: Verify MCP protocol compliance
- **Error Handling**: Test error scenarios and edge cases
- **Security Testing**: Validate authentication and authorization
- **Load Testing**: Test MCP under high concurrent usage

## Installation

### Method 1: Claude Code CLI
```bash
# Add MCP Testing Framework
claude mcp add mcp-testing-framework

# Verify installation
claude mcp list | grep testing-framework
```

### Method 2: NPM Installation
```bash
# Install globally
npm install -g @mcp/testing-framework

# Install locally for project
npm install --save-dev @mcp/testing-framework
```

### Method 3: Manual Configuration
```json
{
  "mcpServers": {
    "mcp-testing-framework": {
      "command": "npx",
      "args": ["@mcp/testing-framework"],
      "env": {
        "TEST_MODE": "true",
        "LOG_LEVEL": "debug",
        "TEST_TIMEOUT": "30000"
      }
    }
  }
}
```

## Usage Examples

### Basic MCP Testing
```bash
# Initialize test suite for MCP
mcp-test init --mcp-name "my-custom-mcp"

# Run all tests
mcp-test run

# Run specific test suite
mcp-test run --suite "unit-tests"

# Run tests with coverage
mcp-test run --coverage
```

### Advanced Testing Commands
```bash
# Test MCP performance
mcp-test performance --mcp "filesystem-mcp" --duration 60s

# Validate MCP schema compliance
mcp-test validate --schema --mcp "my-mcp"

# Test MCP security
mcp-test security --mcp "database-mcp" --scan-all

# Load testing
mcp-test load --mcp "api-mcp" --concurrent 100 --requests 1000
```

## Test Configuration

### Basic Test Configuration
```yaml
# mcp-test.config.yaml
test_config:
  name: "my-mcp-tests"
  version: "1.0.0"
  timeout: 30000
  retries: 3
  
  mcps:
    - name: "filesystem-mcp"
      path: "./src/filesystem-mcp"
      config: "./config/filesystem.json"
    
    - name: "database-mcp"
      path: "./src/database-mcp"
      config: "./config/database.json"

  test_suites:
    - name: "unit-tests"
      pattern: "**/*.unit.test.js"
      timeout: 5000
    
    - name: "integration-tests"
      pattern: "**/*.integration.test.js"
      timeout: 15000
    
    - name: "performance-tests"
      pattern: "**/*.perf.test.js"
      timeout: 60000

  coverage:
    enabled: true
    threshold: 80
    exclude: ["node_modules/**", "tests/**"]
```

### Advanced Test Configuration
```yaml
advanced_config:
  environments:
    development:
      claude_code_version: "latest"
      node_version: "18"
      test_data: "./test-data/dev"
    
    staging:
      claude_code_version: "stable"
      node_version: "18"
      test_data: "./test-data/staging"
    
    production:
      claude_code_version: "stable"
      node_version: "18"
      test_data: "./test-data/prod"

  performance:
    baseline_file: "./baselines/performance.json"
    thresholds:
      response_time: 1000  # ms
      memory_usage: 100    # MB
      cpu_usage: 50        # %

  security:
    scan_dependencies: true
    check_vulnerabilities: true
    validate_permissions: true
    test_authentication: true
```

## Writing Tests

### Unit Test Example
```javascript
// tests/filesystem-mcp.unit.test.js
const { MCPTestFramework } = require('@mcp/testing-framework');
const FilesystemMCP = require('../src/filesystem-mcp');

describe('Filesystem MCP Unit Tests', () => {
  let testFramework;
  let filesystemMCP;

  beforeEach(async () => {
    testFramework = new MCPTestFramework();
    filesystemMCP = new FilesystemMCP();
    await testFramework.setup();
  });

  afterEach(async () => {
    await testFramework.cleanup();
  });

  test('should read file successfully', async () => {
    // Arrange
    const testFile = await testFramework.createTestFile('test.txt', 'Hello World');
    
    // Act
    const result = await filesystemMCP.readFile(testFile);
    
    // Assert
    expect(result.success).toBe(true);
    expect(result.content).toBe('Hello World');
  });

  test('should handle file not found error', async () => {
    // Act & Assert
    await expect(filesystemMCP.readFile('nonexistent.txt'))
      .rejects.toThrow('File not found');
  });

  test('should validate file permissions', async () => {
    // Arrange
    const restrictedFile = await testFramework.createRestrictedFile('restricted.txt');
    
    // Act & Assert
    await expect(filesystemMCP.readFile(restrictedFile))
      .rejects.toThrow('Permission denied');
  });
});
```

### Integration Test Example
```javascript
// tests/filesystem-mcp.integration.test.js
const { MCPTestFramework, ClaudeCodeMock } = require('@mcp/testing-framework');

describe('Filesystem MCP Integration Tests', () => {
  let testFramework;
  let claudeCodeMock;

  beforeEach(async () => {
    testFramework = new MCPTestFramework();
    claudeCodeMock = new ClaudeCodeMock();
    await testFramework.setupIntegration(claudeCodeMock);
  });

  test('should integrate with Claude Code filesystem operations', async () => {
    // Arrange
    const workspace = await testFramework.createTestWorkspace();
    await claudeCodeMock.setWorkspace(workspace);

    // Act
    const response = await claudeCodeMock.sendMessage(
      'Read the contents of package.json'
    );

    // Assert
    expect(response.success).toBe(true);
    expect(response.data).toContain('package.json contents');
    expect(claudeCodeMock.getLastMCPCall()).toEqual({
      mcp: 'filesystem',
      method: 'read_file',
      args: { path: 'package.json' }
    });
  });

  test('should handle Claude Code error scenarios', async () => {
    // Arrange
    await claudeCodeMock.simulateError('PERMISSION_DENIED');

    // Act
    const response = await claudeCodeMock.sendMessage(
      'Read the contents of /etc/passwd'
    );

    // Assert
    expect(response.success).toBe(false);
    expect(response.error).toContain('Permission denied');
  });
});
```

### Performance Test Example
```javascript
// tests/filesystem-mcp.perf.test.js
const { MCPTestFramework, PerformanceProfiler } = require('@mcp/testing-framework');

describe('Filesystem MCP Performance Tests', () => {
  let testFramework;
  let profiler;

  beforeEach(async () => {
    testFramework = new MCPTestFramework();
    profiler = new PerformanceProfiler();
    await testFramework.setup();
  });

  test('should read large files within performance threshold', async () => {
    // Arrange
    const largeFile = await testFramework.createLargeFile('large.txt', '10MB');
    
    // Act
    const startTime = Date.now();
    await profiler.start();
    
    const result = await filesystemMCP.readFile(largeFile);
    
    const endTime = Date.now();
    const metrics = await profiler.stop();

    // Assert
    expect(endTime - startTime).toBeLessThan(5000); // 5 seconds
    expect(metrics.memoryUsage).toBeLessThan(50 * 1024 * 1024); // 50MB
    expect(result.success).toBe(true);
  });

  test('should handle concurrent file operations efficiently', async () => {
    // Arrange
    const files = await testFramework.createMultipleFiles(100);
    
    // Act
    const startTime = Date.now();
    const promises = files.map(file => filesystemMCP.readFile(file));
    const results = await Promise.all(promises);
    const endTime = Date.now();

    // Assert
    expect(endTime - startTime).toBeLessThan(10000); // 10 seconds
    expect(results.every(r => r.success)).toBe(true);
  });
});
```

## Test Utilities

### Mock Utilities
```javascript
// Mock Claude Code environment
const claudeCodeMock = new ClaudeCodeMock({
  workspace: '/test/workspace',
  permissions: ['read', 'write'],
  environment: 'test'
});

// Mock MCP responses
const mcpMock = new MCPMock({
  responses: {
    'read_file': { success: true, content: 'mocked content' },
    'write_file': { success: true, bytes_written: 100 }
  }
});

// Mock external services
const serviceMock = new ServiceMock({
  baseUrl: 'https://api.example.com',
  responses: {
    '/users': { users: [{ id: 1, name: 'Test User' }] }
  }
});
```

### Test Data Management
```javascript
// Create test data
const testData = await testFramework.createTestData({
  files: [
    { name: 'test1.txt', content: 'Hello World' },
    { name: 'test2.json', content: '{"key": "value"}' }
  ],
  directories: ['temp', 'output'],
  permissions: {
    'test1.txt': 'read-only',
    'temp': 'read-write'
  }
});

// Cleanup test data
await testFramework.cleanupTestData(testData);
```

### Assertion Helpers
```javascript
// MCP-specific assertions
expect(response).toBeValidMCPResponse();
expect(response).toHaveMCPError('PERMISSION_DENIED');
expect(response).toMatchMCPSchema(expectedSchema);

// Performance assertions
expect(metrics).toMeetPerformanceThreshold({
  responseTime: 1000,
  memoryUsage: 100 * 1024 * 1024,
  cpuUsage: 50
});

// Security assertions
expect(mcp).toHaveSecureConfiguration();
expect(mcp).toValidateInputProperly();
expect(mcp).toHandleAuthenticationCorrectly();
```

## Continuous Integration

### GitHub Actions Integration
```yaml
# .github/workflows/mcp-tests.yml
name: MCP Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [16, 18, 20]
        claude-code-version: [stable, latest]
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      
      - name: Install Claude Code
        run: |
          npm install -g @anthropic/claude-code@${{ matrix.claude-code-version }}
      
      - name: Install dependencies
        run: npm ci
      
      - name: Install MCP Testing Framework
        run: npm install -g @mcp/testing-framework
      
      - name: Run MCP tests
        run: |
          mcp-test run --coverage --reporter junit
        env:
          NODE_ENV: test
          CLAUDE_CODE_VERSION: ${{ matrix.claude-code-version }}
      
      - name: Upload test results
        uses: actions/upload-artifact@v3
        if: always()
        with:
          name: test-results-${{ matrix.node-version }}-${{ matrix.claude-code-version }}
          path: |
            test-results.xml
            coverage/
      
      - name: Upload coverage to Codecov
        uses: codecov/codecov-action@v3
        with:
          file: ./coverage/lcov.info
```

### Jenkins Pipeline
```groovy
// Jenkinsfile
pipeline {
    agent any
    
    parameters {
        choice(
            name: 'CLAUDE_CODE_VERSION',
            choices: ['stable', 'latest', 'beta'],
            description: 'Claude Code version to test against'
        )
    }
    
    stages {
        stage('Setup') {
            steps {
                sh 'npm install -g @anthropic/claude-code@${CLAUDE_CODE_VERSION}'
                sh 'npm ci'
                sh 'npm install -g @mcp/testing-framework'
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh 'mcp-test run --suite unit-tests --reporter junit'
            }
            post {
                always {
                    junit 'test-results/unit-tests.xml'
                }
            }
        }
        
        stage('Integration Tests') {
            steps {
                sh 'mcp-test run --suite integration-tests --reporter junit'
            }
            post {
                always {
                    junit 'test-results/integration-tests.xml'
                }
            }
        }
        
        stage('Performance Tests') {
            steps {
                sh 'mcp-test run --suite performance-tests --reporter junit'
            }
            post {
                always {
                    publishHTML([
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'performance-reports',
                        reportFiles: 'index.html',
                        reportName: 'Performance Report'
                    ])
                }
            }
        }
        
        stage('Security Tests') {
            steps {
                sh 'mcp-test security --all --reporter junit'
            }
            post {
                always {
                    junit 'test-results/security-tests.xml'
                }
            }
        }
    }
    
    post {
        always {
            publishTestResults testResultsPattern: 'test-results/*.xml'
            publishCoverage adapters: [
                coberturaAdapter('coverage/cobertura-coverage.xml')
            ]
        }
    }
}
```

## Best Practices

### Test Organization
1. **Separate Test Types**: Keep unit, integration, and performance tests in separate files
2. **Descriptive Names**: Use clear, descriptive test names that explain what is being tested
3. **Test Data Management**: Use proper setup and teardown for test data
4. **Mock External Dependencies**: Mock external services and APIs for reliable testing
5. **Test Coverage**: Aim for high test coverage but focus on critical paths

### Performance Testing
1. **Baseline Measurements**: Establish performance baselines for comparison
2. **Realistic Load**: Use realistic data sizes and concurrent user scenarios
3. **Resource Monitoring**: Monitor CPU, memory, and network usage during tests
4. **Regression Detection**: Automatically detect performance regressions
5. **Environment Consistency**: Use consistent test environments for reliable results

### Security Testing
1. **Input Validation**: Test all input validation and sanitization
2. **Authentication**: Verify authentication and authorization mechanisms
3. **Permission Checks**: Test file and resource permission enforcement
4. **Error Handling**: Ensure sensitive information isn't leaked in error messages
5. **Dependency Scanning**: Regularly scan dependencies for vulnerabilities

## Troubleshooting

### Common Issues

**Issue: Tests Failing Due to Environment Differences**
```bash
# Check Claude Code version compatibility
claude --version
mcp-test check-compatibility --claude-version $(claude --version)

# Use environment-specific configuration
mcp-test run --env development
```

**Issue: Performance Tests Inconsistent**
```bash
# Run performance tests multiple times
mcp-test performance --iterations 5 --statistical-analysis

# Check system resources
mcp-test system-check --performance-mode
```

**Issue: Mock Services Not Working**
```bash
# Debug mock configuration
mcp-test debug --mocks --verbose

# Validate mock responses
mcp-test validate-mocks --schema-check
```

## API Reference

### Test Framework API
```typescript
interface MCPTestFramework {
  setup(config?: TestConfig): Promise<void>;
  cleanup(): Promise<void>;
  createTestFile(name: string, content: string): Promise<string>;
  createTestWorkspace(): Promise<string>;
  runTest(testPath: string): Promise<TestResult>;
  generateReport(format: 'html' | 'json' | 'junit'): Promise<string>;
}

interface TestResult {
  success: boolean;
  duration: number;
  coverage: CoverageReport;
  errors: TestError[];
  performance: PerformanceMetrics;
}
```

## Community & Support

### Resources
- [MCP Testing Framework Documentation](https://docs.mcp.dev/testing)
- [Testing Best Practices Guide](https://docs.mcp.dev/testing/best-practices)
- [Community Forum](https://community.mcp.dev/testing)
- [GitHub Repository](https://github.com/mcp/testing-framework)

### Contributing
- [Contribution Guidelines](https://github.com/mcp/testing-framework/blob/main/CONTRIBUTING.md)
- [Test Template Repository](https://github.com/mcp/test-templates)
- [Feature Requests](https://github.com/mcp/testing-framework/discussions)

---

*MCP Testing Framework ensures your custom MCPs are reliable, performant, and secure through comprehensive automated testing.*

