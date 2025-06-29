# Jenkins MCP

## Overview
The Jenkins MCP provides Claude with comprehensive CI/CD pipeline management capabilities, enabling build automation, deployment orchestration, and continuous integration workflows. This MCP is essential for DevOps teams implementing automated software delivery pipelines.

## Installation

### Prerequisites
- Jenkins server running and accessible
- Jenkins CLI or REST API access
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Jenkins authentication credentials

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx jenkins-mcp-server
```

#### Option 2: From GitHub
```bash
git clone https://github.com/jenkins-mcp/jenkins-mcp-server.git
cd jenkins-mcp-server
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install jenkins-mcp-server
```

#### Option 4: Jenkins Plugin
```bash
# Install via Jenkins Plugin Manager
# Search for "MCP Integration Plugin"
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "jenkins": {
      "command": "npx",
      "args": [
        "jenkins-mcp-server",
        "--url", "http://localhost:8080",
        "--username", "admin",
        "--token", "your-api-token"
      ]
    }
  }
}
```

### With HTTPS and Authentication
```json
{
  "mcpServers": {
    "jenkins": {
      "command": "npx",
      "args": [
        "jenkins-mcp-server",
        "--url", "https://jenkins.example.com",
        "--username", "ci-user",
        "--token", "${JENKINS_API_TOKEN}",
        "--verify-ssl"
      ]
    }
  }
}
```

### Multiple Jenkins Instances
```json
{
  "mcpServers": {
    "jenkins-prod": {
      "command": "npx",
      "args": [
        "jenkins-mcp-server",
        "--url", "https://jenkins-prod.example.com",
        "--username", "prod-user",
        "--token", "${JENKINS_PROD_TOKEN}"
      ]
    },
    "jenkins-dev": {
      "command": "npx",
      "args": [
        "jenkins-mcp-server",
        "--url", "http://jenkins-dev:8080",
        "--username", "dev-user",
        "--token", "${JENKINS_DEV_TOKEN}"
      ]
    }
  }
}
```

### Environment Variables
```bash
export JENKINS_URL=http://localhost:8080
export JENKINS_USER=admin
export JENKINS_API_TOKEN=your-token
export JENKINS_CLI_JAR=/path/to/jenkins-cli.jar
```

## Usage Examples

### Job Management
```
# List all jobs
Show me all Jenkins jobs and their current status.

# Create new job
Create a new freestyle job called "build-frontend" that builds a React application.

# Trigger builds
Start a build for the "deploy-production" job with parameters.

# Job configuration
Show me the configuration for the "test-suite" job.

# Delete jobs
Remove the old "legacy-build" job that's no longer needed.
```

### Build Operations
```
# Build status
Check the status of the last 10 builds for the "main-pipeline" job.

# Build logs
Show me the console output for build #42 of the "api-tests" job.

# Build artifacts
List all artifacts from the latest successful build of "package-app".

# Build parameters
Display the parameters used for build #15 of the "deploy-staging" job.

# Stop builds
Cancel the currently running build of the "long-running-tests" job.
```

### Pipeline Management
```
# Pipeline status
Show me the status of all pipeline jobs in the "production" folder.

# Pipeline visualization
Display the pipeline flow for the "full-deployment" job.

# Pipeline history
Show me the last 20 pipeline executions with their results.

# Pipeline configuration
Export the Jenkinsfile for the "microservice-deploy" pipeline.

# Pipeline metrics
Generate a report on pipeline success rates over the last month.
```

### Advanced Operations
```
# Node management
Show me all Jenkins agents and their current status.

# Plugin management
List all installed plugins and check for updates.

# System information
Display Jenkins system information and resource usage.

# Backup operations
Trigger a backup of Jenkins configuration and job definitions.

# Security audit
Review user permissions and access controls.
```

## Features

### Core Jenkins Operations
- **Job Management**: Create, configure, and delete Jenkins jobs
- **Build Execution**: Trigger, monitor, and control builds
- **Pipeline Orchestration**: Manage complex CI/CD pipelines
- **Artifact Management**: Handle build artifacts and dependencies
- **Log Analysis**: Access and analyze build logs

### Advanced Features
- **Multi-branch Pipelines**: Automatic pipeline creation for branches
- **Blue Ocean Integration**: Modern pipeline visualization
- **Distributed Builds**: Manage multiple build agents
- **Plugin Integration**: Leverage Jenkins plugin ecosystem
- **Webhook Management**: Configure automated triggers

### CI/CD Capabilities
- **Source Control Integration**: Git, SVN, Mercurial support
- **Testing Automation**: Unit, integration, and acceptance tests
- **Deployment Automation**: Automated deployment to multiple environments
- **Quality Gates**: Code quality and security checks
- **Notification Systems**: Email, Slack, and custom notifications

### Monitoring & Reporting
- **Build Metrics**: Success rates, duration, and trends
- **Performance Monitoring**: Resource usage and bottlenecks
- **Custom Dashboards**: Tailored views for different teams
- **Audit Trails**: Complete history of changes and actions
- **Health Checks**: System and job health monitoring

## Requirements

### System Requirements
- **Jenkins**: Version 2.400 or higher (LTS recommended)
- **Java**: OpenJDK 11 or 17
- **Operating System**: Linux, macOS, or Windows
- **Memory**: 2GB+ available RAM (4GB+ recommended)
- **Disk Space**: Varies by build artifacts and logs

### Jenkins Configuration
```groovy
// jenkins.yaml (Configuration as Code)
jenkins:
  systemMessage: "Jenkins configured automatically by JCasC"
  numExecutors: 2
  mode: NORMAL
  scmCheckoutRetryCount: 3
  
security:
  globalJobDslSecurityConfiguration:
    useScriptSecurity: false

credentials:
  system:
    domainCredentials:
    - credentials:
      - usernamePassword:
          scope: GLOBAL
          id: "github-credentials"
          username: "ci-user"
          password: "${GITHUB_TOKEN}"
```

### Network Access
- HTTP/HTTPS access to Jenkins server
- Git repository access for source control
- Deployment target access for CD operations
- Artifact repository access (Nexus, Artifactory)

## Security Considerations

### Best Practices
- **API Tokens**: Use API tokens instead of passwords
- **Role-Based Access**: Implement proper user permissions
- **Secure Credentials**: Use Jenkins credential store
- **Network Security**: Restrict access with firewalls
- **Regular Updates**: Keep Jenkins and plugins updated

### Secure Configuration
```json
{
  "mcpServers": {
    "jenkins": {
      "command": "npx",
      "args": [
        "jenkins-mcp-server",
        "--url", "https://jenkins.example.com",
        "--username", "ci-user",
        "--token", "${JENKINS_API_TOKEN}",
        "--verify-ssl",
        "--timeout", "30"
      ]
    }
  }
}
```

### Jenkins Security Settings
```groovy
// Security configuration
security:
  authorizationStrategy:
    roleBased:
      roles:
        global:
        - name: "admin"
          description: "Jenkins administrators"
          permissions:
          - "Overall/Administer"
        - name: "developer"
          description: "Developers"
          permissions:
          - "Overall/Read"
          - "Job/Build"
          - "Job/Read"
```

## Troubleshooting

### Common Issues

#### Connection Failed
**Problem**: Cannot connect to Jenkins server
**Solution**:
```bash
# Test Jenkins connectivity
curl -I http://jenkins:8080

# Check Jenkins status
curl http://jenkins:8080/api/json

# Verify authentication
curl -u username:token http://jenkins:8080/api/json
```

#### Authentication Failed
**Problem**: Invalid credentials or permissions
**Solution**:
```bash
# Generate API token in Jenkins UI
# User -> Configure -> API Token -> Add new Token

# Test authentication
curl -u username:token http://jenkins:8080/me/api/json

# Check user permissions
curl -u username:token http://jenkins:8080/user/username/api/json
```

#### Build Failures
**Problem**: Jobs failing to execute
**Solution**:
- Check build logs for error details
- Verify agent availability and capacity
- Review job configuration and parameters
- Check workspace permissions and disk space

#### Plugin Issues
**Problem**: Plugin-related errors
**Solution**:
```bash
# List installed plugins
curl -u username:token http://jenkins:8080/pluginManager/api/json?depth=1

# Check plugin updates
# Navigate to Manage Jenkins -> Manage Plugins

# Restart Jenkins if needed
curl -u username:token -X POST http://jenkins:8080/restart
```

### Diagnostic Commands
```bash
# Jenkins system info
curl -u username:token http://jenkins:8080/systemInfo/api/json

# Node information
curl -u username:token http://jenkins:8080/computer/api/json

# Job list
curl -u username:token http://jenkins:8080/api/json?tree=jobs[name,url]

# Build queue
curl -u username:token http://jenkins:8080/queue/api/json
```

## Advanced Configuration

### Pipeline as Code (Jenkinsfile)
```groovy
pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY = 'registry.example.com'
        APP_NAME = 'myapp'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/company/app.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        
        stage('Test') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        sh 'npm run test:unit'
                    }
                    post {
                        always {
                            publishTestResults testResultsPattern: 'test-results.xml'
                        }
                    }
                }
                stage('Integration Tests') {
                    steps {
                        sh 'npm run test:integration'
                    }
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    def image = docker.build("${DOCKER_REGISTRY}/${APP_NAME}:${BUILD_NUMBER}")
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'docker-registry-credentials') {
                        image.push()
                        image.push('latest')
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                sh "kubectl set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_REGISTRY}/${APP_NAME}:${BUILD_NUMBER}"
                sh "kubectl rollout status deployment/${APP_NAME}"
            }
        }
        
        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            input {
                message "Deploy to production?"
                ok "Deploy"
                parameters {
                    choice(name: 'ENVIRONMENT', choices: ['production', 'staging'], description: 'Target environment')
                }
            }
            steps {
                sh "kubectl --context=production set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_REGISTRY}/${APP_NAME}:${BUILD_NUMBER}"
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
        success {
            slackSend channel: '#deployments', 
                     color: 'good', 
                     message: "✅ ${env.JOB_NAME} - ${env.BUILD_NUMBER} deployed successfully"
        }
        failure {
            slackSend channel: '#deployments', 
                     color: 'danger', 
                     message: "❌ ${env.JOB_NAME} - ${env.BUILD_NUMBER} failed"
        }
    }
}
```

### Shared Libraries
```groovy
// vars/deployApp.groovy
def call(Map config) {
    pipeline {
        agent any
        stages {
            stage('Deploy') {
                steps {
                    script {
                        sh "kubectl set image deployment/${config.appName} ${config.appName}=${config.image}"
                        sh "kubectl rollout status deployment/${config.appName}"
                    }
                }
            }
        }
    }
}

// Usage in Jenkinsfile
@Library('shared-library') _
deployApp([
    appName: 'myapp',
    image: 'registry.example.com/myapp:latest'
])
```

### Job DSL
```groovy
// Create jobs programmatically
job('build-frontend') {
    scm {
        git('https://github.com/company/frontend.git')
    }
    triggers {
        scm('H/5 * * * *')
    }
    steps {
        shell('npm install')
        shell('npm run build')
        shell('npm test')
    }
    publishers {
        archiveArtifacts('dist/**')
        publishHtml([
            allowMissing: false,
            alwaysLinkToLastBuild: true,
            keepAll: true,
            reportDir: 'coverage',
            reportFiles: 'index.html',
            reportName: 'Coverage Report'
        ])
    }
}
```

## Integration Examples

### With Git MCP
```
# Source control integration
1. Use git MCP to manage repository operations
2. Use jenkins MCP to trigger builds on commits
3. Coordinate branch-based deployments
```

### With Docker MCP
```
# Container build pipeline
1. Use jenkins MCP to orchestrate builds
2. Use docker MCP to build and push images
3. Deploy containers to target environments
```

### With Kubernetes MCP
```
# Cloud-native deployment
1. Use jenkins MCP for CI/CD orchestration
2. Use kubernetes MCP for deployment operations
3. Monitor application health and performance
```

## Workflow Examples

### Basic CI Pipeline
```
1. Code commit triggers webhook
2. Jenkins pulls latest code
3. Run automated tests
4. Build application artifacts
5. Deploy to staging environment
6. Run integration tests
7. Notify team of results
```

### Advanced CD Pipeline
```
1. Multi-stage pipeline execution
2. Parallel test execution
3. Security and quality scans
4. Container image building
5. Progressive deployment (canary/blue-green)
6. Automated rollback on failure
7. Metrics and monitoring integration
```

### Release Management
```
1. Feature branch development
2. Pull request validation
3. Merge to main branch
4. Release candidate creation
5. Staging environment deployment
6. Production deployment approval
7. Release tagging and documentation
```

## Links

- [Jenkins MCP Repository](https://github.com/jenkins-mcp/jenkins-mcp-server)
- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [Jenkins Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/)
- [Jenkins Plugin Index](https://plugins.jenkins.io/)
- [Jenkins Configuration as Code](https://github.com/jenkinsci/configuration-as-code-plugin)
- [Blue Ocean Documentation](https://www.jenkins.io/doc/book/blueocean/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Jenkins Community](https://www.jenkins.io/participate/)
- [Jenkins User Mailing List](https://groups.google.com/g/jenkinsci-users)
- [MCP Discord](https://discord.gg/mcp)
- [Awesome Jenkins](https://github.com/sahilsk/awesome-jenkins)
- [Jenkins Best Practices](https://www.jenkins.io/doc/book/pipeline/pipeline-best-practices/)

