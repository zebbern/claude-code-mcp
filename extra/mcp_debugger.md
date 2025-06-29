# MCP Debugger

## Overview
The MCP Debugger provides comprehensive debugging capabilities for Model Context Protocol implementations. It offers real-time debugging, request/response inspection, performance monitoring, and error analysis to help developers troubleshoot and optimize their MCPs.

## Key Features

### 🔍 Real-Time Debugging
- **Request Inspection**: Monitor all MCP requests and responses in real-time
- **Breakpoint Support**: Set breakpoints in MCP handlers for step-by-step debugging
- **Variable Inspection**: Examine variables and state during execution
- **Call Stack Analysis**: Trace execution flow through MCP handlers

### 📊 Performance Monitoring
- **Response Time Tracking**: Monitor MCP response times and identify bottlenecks
- **Memory Usage Analysis**: Track memory consumption and detect leaks
- **CPU Profiling**: Analyze CPU usage patterns and optimize performance
- **Resource Monitoring**: Monitor file handles, network connections, and other resources

## Installation

```bash
# Install MCP Debugger
npm install -g @mcp/debugger

# Add to Claude Code configuration
claude mcp add mcp-debugger --debug-mode

# Start debugging session
mcp-debug start --mcp my-custom-mcp
```

## Usage Examples

### Basic Debugging
```bash
# Start debugger for specific MCP
mcp-debug start --mcp filesystem-mcp --port 9229

# Attach to running MCP
mcp-debug attach --pid 12345

# Debug with breakpoints
mcp-debug start --mcp my-mcp --breakpoints "src/handlers/*.ts"

# Debug with logging
mcp-debug start --mcp my-mcp --log-level debug --log-file debug.log
```

### Advanced Debugging
```bash
# Performance profiling
mcp-debug profile --mcp my-mcp --duration 60s --output profile.json

# Memory analysis
mcp-debug memory --mcp my-mcp --heap-snapshot --gc-analysis

# Network debugging
mcp-debug network --mcp api-mcp --trace-requests --capture-headers

# Error analysis
mcp-debug errors --mcp my-mcp --stack-traces --error-patterns
```

## Configuration

```json
{
  "debugger": {
    "enabled": true,
    "port": 9229,
    "host": "localhost",
    "logLevel": "debug",
    "breakOnStart": false,
    "breakOnError": true,
    "captureStackTraces": true,
    "maxLogSize": "100MB",
    "retainLogs": "7d"
  },
  
  "monitoring": {
    "performance": true,
    "memory": true,
    "network": true,
    "resources": true,
    "sampling": {
      "interval": 1000,
      "maxSamples": 10000
    }
  },
  
  "breakpoints": {
    "patterns": ["src/handlers/*.ts", "src/utils/*.ts"],
    "conditions": ["error", "slow_response", "high_memory"],
    "actions": ["log", "capture_state", "notify"]
  }
}
```

## Debugging Interface

### Web-Based Debugger
```bash
# Start web debugger
mcp-debug web --port 8080

# Access at http://localhost:8080
# Features:
# - Real-time request/response viewer
# - Interactive breakpoint management
# - Performance charts and metrics
# - Error log analysis
# - Code navigation and inspection
```

### CLI Debugging
```bash
# Interactive CLI debugger
mcp-debug cli --mcp my-mcp

# Commands available in CLI:
# - break <file:line>     Set breakpoint
# - continue              Continue execution
# - step                  Step to next line
# - inspect <variable>    Inspect variable
# - stack                 Show call stack
# - performance           Show performance metrics
# - quit                  Exit debugger
```

## Breakpoint Management

### Setting Breakpoints
```typescript
// Programmatic breakpoints
import { MCPDebugger } from '@mcp/debugger';

export class MyHandler {
  async handle(request: MCPRequest): Promise<MCPResponse> {
    // Set conditional breakpoint
    MCPDebugger.breakpoint('handler_entry', {
      condition: request.method === 'critical_operation',
      captureState: true,
      logLevel: 'debug'
    });

    // Performance breakpoint
    MCPDebugger.performanceBreakpoint('slow_operation', {
      threshold: 1000, // ms
      action: 'capture_profile'
    });

    // Memory breakpoint
    MCPDebugger.memoryBreakpoint('memory_check', {
      threshold: 100 * 1024 * 1024, // 100MB
      action: 'heap_snapshot'
    });

    return this.processRequest(request);
  }
}
```

### Conditional Breakpoints
```bash
# Set breakpoint with condition
mcp-debug break src/handler.ts:25 --condition "request.method === 'read_file'"

# Set breakpoint on error
mcp-debug break --on-error --pattern "Permission denied"

# Set breakpoint on performance threshold
mcp-debug break --on-slow --threshold 1000ms
```

## Performance Analysis

### Response Time Analysis
```bash
# Analyze response times
mcp-debug analyze response-times --mcp my-mcp --period 1h

# Output:
# Method: read_file
#   Average: 45ms
#   P95: 120ms
#   P99: 250ms
#   Max: 500ms
#   Slowest requests: [...]

# Method: write_file
#   Average: 78ms
#   P95: 180ms
#   P99: 350ms
#   Max: 800ms
```

### Memory Analysis
```bash
# Memory usage analysis
mcp-debug analyze memory --mcp my-mcp --heap-snapshot

# Output:
# Memory Usage:
#   Heap Used: 45.2 MB
#   Heap Total: 67.8 MB
#   External: 12.3 MB
#   RSS: 89.4 MB
#
# Top Memory Consumers:
#   1. String objects: 15.2 MB
#   2. Array objects: 8.7 MB
#   3. Function objects: 6.1 MB
```

### CPU Profiling
```bash
# CPU profiling
mcp-debug profile cpu --mcp my-mcp --duration 30s

# Output:
# CPU Profile (30s):
#   Total CPU Time: 2.4s
#   Self Time: 1.8s
#   
# Hot Functions:
#   1. processRequest: 45% (1.08s)
#   2. validateInput: 23% (0.55s)
#   3. formatResponse: 18% (0.43s)
```

## Error Analysis

### Error Tracking
```typescript
// Enhanced error handling with debugging
import { MCPDebugger, ErrorAnalyzer } from '@mcp/debugger';

export class ErrorHandler {
  async handle(request: MCPRequest): Promise<MCPResponse> {
    try {
      return await this.processRequest(request);
    } catch (error) {
      // Capture error context
      const errorContext = MCPDebugger.captureErrorContext({
        request,
        stackTrace: error.stack,
        timestamp: new Date(),
        memoryUsage: process.memoryUsage(),
        systemInfo: process.versions
      });

      // Analyze error pattern
      const analysis = await ErrorAnalyzer.analyze(error, errorContext);
      
      // Log with enhanced context
      MCPDebugger.logError('Request failed', {
        error: error.message,
        context: errorContext,
        analysis,
        suggestions: analysis.suggestions
      });

      return {
        success: false,
        error: error.message,
        debugId: errorContext.id
      };
    }
  }
}
```

### Error Pattern Detection
```bash
# Analyze error patterns
mcp-debug analyze errors --mcp my-mcp --period 24h

# Output:
# Error Analysis (24h):
#   Total Errors: 127
#   Error Rate: 2.3%
#   
# Top Error Types:
#   1. Permission Denied: 45 (35.4%)
#   2. File Not Found: 32 (25.2%)
#   3. Timeout: 28 (22.0%)
#   4. Invalid Input: 22 (17.3%)
#
# Error Trends:
#   - Permission errors increased 15% vs yesterday
#   - Timeout errors decreased 8% vs yesterday
```

## Network Debugging

### Request/Response Monitoring
```bash
# Monitor network requests
mcp-debug network monitor --mcp api-mcp --capture-all

# Filter specific requests
mcp-debug network monitor --filter "method=POST" --capture-body

# Analyze network performance
mcp-debug network analyze --latency --throughput --errors
```

### Network Trace Analysis
```typescript
// Network debugging integration
import { NetworkDebugger } from '@mcp/debugger';

export class APIHandler {
  async makeRequest(url: string, options: RequestOptions): Promise<Response> {
    const trace = NetworkDebugger.startTrace('api_request', {
      url,
      method: options.method,
      headers: options.headers
    });

    try {
      const response = await fetch(url, options);
      
      trace.recordResponse({
        status: response.status,
        headers: response.headers,
        size: response.headers.get('content-length')
      });

      return response;
    } catch (error) {
      trace.recordError(error);
      throw error;
    } finally {
      trace.end();
    }
  }
}
```

## Integration with IDEs

### VS Code Integration
```json
// .vscode/launch.json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug MCP",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/src/index.ts",
      "env": {
        "MCP_DEBUG": "true",
        "MCP_DEBUG_PORT": "9229"
      },
      "runtimeArgs": ["--inspect=9229"],
      "console": "integratedTerminal",
      "restart": true,
      "protocol": "inspector"
    }
  ]
}
```

### IntelliJ Integration
```xml
<!-- .idea/runConfigurations/Debug_MCP.xml -->
<component name="ProjectRunConfigurationManager">
  <configuration default="false" name="Debug MCP" type="NodeJSConfigurationType">
    <option name="workingDir" value="$PROJECT_DIR$" />
    <option name="interpreterRef" value="project" />
    <option name="parameters" value="--inspect=9229" />
    <option name="applicationParameters" value="" />
    <option name="envs">
      <env name="MCP_DEBUG" value="true" />
      <env name="MCP_DEBUG_PORT" value="9229" />
    </option>
  </configuration>
</component>
```

## Automated Debugging

### CI/CD Integration
```yaml
# .github/workflows/debug-analysis.yml
name: Debug Analysis

on: [push, pull_request]

jobs:
  debug-analysis:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18
      
      - name: Install dependencies
        run: npm ci
      
      - name: Install MCP Debugger
        run: npm install -g @mcp/debugger
      
      - name: Run debug analysis
        run: |
          mcp-debug analyze --automated \
            --performance-check \
            --memory-check \
            --error-check \
            --output debug-report.json
      
      - name: Upload debug report
        uses: actions/upload-artifact@v3
        with:
          name: debug-report
          path: debug-report.json
```

## Best Practices

### Debugging Workflow
1. **Start with Logs**: Enable debug logging before using breakpoints
2. **Use Conditional Breakpoints**: Avoid stopping on every request
3. **Monitor Performance**: Watch for performance regressions during debugging
4. **Capture Context**: Always capture relevant context when errors occur
5. **Clean Up**: Remove debug code and breakpoints before production

### Performance Debugging
1. **Profile Regularly**: Run performance profiles during development
2. **Set Baselines**: Establish performance baselines for comparison
3. **Monitor Trends**: Track performance trends over time
4. **Optimize Hot Paths**: Focus optimization efforts on frequently used code
5. **Test Under Load**: Debug performance issues under realistic load

### Error Debugging
1. **Comprehensive Logging**: Log all relevant context for errors
2. **Error Categorization**: Categorize errors for better analysis
3. **Reproduction Steps**: Document steps to reproduce errors
4. **Fix Root Causes**: Address root causes, not just symptoms
5. **Monitor Error Rates**: Track error rates and trends

## Troubleshooting

### Common Issues
```bash
# Debugger not connecting
mcp-debug check-connection --port 9229

# Performance issues during debugging
mcp-debug optimize --reduce-overhead --sampling-rate 0.1

# Memory issues
mcp-debug memory --gc-force --heap-limit 512MB

# Network debugging issues
mcp-debug network --check-connectivity --dns-resolution
```

---

*MCP Debugger provides comprehensive debugging capabilities to help developers build reliable and performant MCPs.*

