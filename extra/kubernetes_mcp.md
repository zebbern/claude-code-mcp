# Kubernetes MCP

## Overview
The Kubernetes MCP provides Claude with comprehensive Kubernetes cluster management capabilities, enabling pod orchestration, service management, deployment operations, and cluster administration. This MCP is essential for cloud-native application development and container orchestration workflows.

## Installation

### Prerequisites
- Kubernetes cluster access (local or remote)
- kubectl CLI tool installed and configured
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Valid kubeconfig file

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx kubernetes-mcp-server
```

#### Option 2: From GitHub
```bash
git clone https://github.com/kubernetes-mcp/kubernetes-mcp-server.git
cd kubernetes-mcp-server
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install kubernetes-mcp-server
```

#### Option 4: Helm Chart
```bash
helm repo add kubernetes-mcp https://kubernetes-mcp.github.io/helm-charts
helm install kubernetes-mcp kubernetes-mcp/kubernetes-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "kubernetes": {
      "command": "npx",
      "args": ["kubernetes-mcp-server"]
    }
  }
}
```

### With Custom Kubeconfig
```json
{
  "mcpServers": {
    "kubernetes": {
      "command": "npx",
      "args": [
        "kubernetes-mcp-server",
        "--kubeconfig", "/path/to/kubeconfig"
      ]
    }
  }
}
```

### With Specific Context
```json
{
  "mcpServers": {
    "kubernetes": {
      "command": "npx",
      "args": [
        "kubernetes-mcp-server",
        "--context", "production-cluster"
      ]
    }
  }
}
```

### Multiple Clusters
```json
{
  "mcpServers": {
    "kubernetes-dev": {
      "command": "npx",
      "args": [
        "kubernetes-mcp-server",
        "--context", "development"
      ]
    },
    "kubernetes-prod": {
      "command": "npx",
      "args": [
        "kubernetes-mcp-server",
        "--context", "production"
      ]
    }
  }
}
```

## Usage Examples

### Pod Management
```
# List pods
Show me all pods in the default namespace.

# Create pod
Create a new nginx pod with the latest image.

# Delete pods
Delete all pods with the label "app=old-version".

# Pod logs
Show me the logs for the pod "web-server-abc123".

# Execute in pod
Run a bash shell in the pod "debug-pod".
```

### Deployment Operations
```
# Create deployment
Create a deployment for nginx with 3 replicas.

# Scale deployment
Scale the "web-app" deployment to 5 replicas.

# Update deployment
Update the "api-server" deployment to use image version "v2.0.0".

# Rollback deployment
Rollback the "frontend" deployment to the previous version.

# Deployment status
Check the rollout status of the "backend" deployment.
```

### Service Management
```
# Create service
Create a LoadBalancer service for the "web" deployment on port 80.

# List services
Show me all services in the "production" namespace.

# Service endpoints
Display the endpoints for the "database" service.

# Port forwarding
Set up port forwarding from local port 8080 to service "api" port 3000.
```

### Namespace Operations
```
# List namespaces
Show me all namespaces in the cluster.

# Create namespace
Create a new namespace called "staging".

# Switch namespace
Set the default namespace to "development".

# Namespace resources
Show me all resources in the "production" namespace.
```

## Features

### Core Kubernetes Operations
- **Pod Management**: Create, delete, list, and monitor pods
- **Deployment Control**: Manage application deployments and rollouts
- **Service Discovery**: Create and manage services and endpoints
- **Namespace Management**: Organize resources with namespaces
- **ConfigMap/Secret**: Manage configuration and sensitive data

### Advanced Features
- **Horizontal Pod Autoscaling**: Automatic scaling based on metrics
- **Ingress Management**: HTTP/HTTPS routing and load balancing
- **Persistent Volumes**: Storage management and provisioning
- **RBAC**: Role-based access control configuration
- **Network Policies**: Network security and isolation

### Monitoring & Observability
- **Resource Metrics**: CPU, memory, and storage usage
- **Event Monitoring**: Cluster events and notifications
- **Log Aggregation**: Centralized logging from pods
- **Health Checks**: Liveness and readiness probes
- **Custom Metrics**: Application-specific metrics

### Multi-Cluster Support
- **Context Switching**: Manage multiple cluster contexts
- **Cross-Cluster Operations**: Coordinate across clusters
- **Cluster Federation**: Federated resource management
- **Hybrid Cloud**: On-premises and cloud integration

## Requirements

### System Requirements
- **Kubernetes**: Version 1.20 or higher
- **kubectl**: Compatible version with cluster
- **Operating System**: Linux, macOS, or Windows
- **Memory**: 1GB+ available RAM
- **Network**: Cluster network connectivity

### Cluster Access
- Valid kubeconfig file
- Appropriate RBAC permissions
- Network access to Kubernetes API server
- Authentication credentials (certificates, tokens, etc.)

### Permissions
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: kubernetes-mcp-role
rules:
- apiGroups: [""]
  resources: ["pods", "services", "configmaps", "secrets"]
  verbs: ["get", "list", "create", "update", "delete"]
- apiGroups: ["apps"]
  resources: ["deployments", "replicasets"]
  verbs: ["get", "list", "create", "update", "delete"]
```

## Security Considerations

### Best Practices
- **RBAC**: Use role-based access control
- **Network Policies**: Implement network segmentation
- **Pod Security**: Use security contexts and policies
- **Secret Management**: Encrypt secrets at rest
- **Image Security**: Scan container images for vulnerabilities

### Secure Configuration
```json
{
  "mcpServers": {
    "kubernetes": {
      "command": "npx",
      "args": [
        "kubernetes-mcp-server",
        "--read-only",
        "--namespace", "safe-namespace"
      ]
    }
  }
}
```

### Pod Security Context
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  securityContext:
    runAsNonRoot: true
    runAsUser: 1000
    fsGroup: 2000
  containers:
  - name: app
    image: nginx
    securityContext:
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      capabilities:
        drop:
        - ALL
```

## Troubleshooting

### Common Issues

#### Cannot Connect to Cluster
**Problem**: Unable to connect to Kubernetes API server
**Solution**:
```bash
# Check cluster connectivity
kubectl cluster-info

# Verify kubeconfig
kubectl config view

# Test authentication
kubectl auth can-i get pods
```

#### Permission Denied
**Problem**: Insufficient RBAC permissions
**Solution**:
```bash
# Check current permissions
kubectl auth can-i --list

# View current user/context
kubectl config current-context

# Check role bindings
kubectl get rolebindings,clusterrolebindings
```

#### Pod Scheduling Issues
**Problem**: Pods stuck in Pending state
**Solution**:
```bash
# Check node resources
kubectl top nodes

# Describe pod for events
kubectl describe pod <pod-name>

# Check node selectors and taints
kubectl get nodes --show-labels
```

#### Service Not Accessible
**Problem**: Cannot reach service endpoints
**Solution**:
```bash
# Check service endpoints
kubectl get endpoints <service-name>

# Verify service selector
kubectl describe service <service-name>

# Test DNS resolution
kubectl run test-pod --image=busybox --rm -it -- nslookup <service-name>
```

### Diagnostic Commands
```bash
# Cluster status
kubectl get componentstatuses

# Node information
kubectl get nodes -o wide

# Resource usage
kubectl top nodes
kubectl top pods

# Events
kubectl get events --sort-by=.metadata.creationTimestamp
```

## Advanced Configuration

### Custom Resource Definitions
```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: applications.example.com
spec:
  group: example.com
  versions:
  - name: v1
    served: true
    storage: true
    schema:
      openAPIV3Schema:
        type: object
        properties:
          spec:
            type: object
            properties:
              replicas:
                type: integer
              image:
                type: string
  scope: Namespaced
  names:
    plural: applications
    singular: application
    kind: Application
```

### Helm Integration
```bash
# Install with Helm
helm install my-app ./chart

# Upgrade release
helm upgrade my-app ./chart

# Rollback release
helm rollback my-app 1
```

### Kustomize Configuration
```yaml
# kustomization.yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
- deployment.yaml
- service.yaml

patchesStrategicMerge:
- patch.yaml

images:
- name: nginx
  newTag: 1.21
```

## Workflow Examples

### Application Deployment
```
1. Create namespace for application
2. Deploy database with persistent storage
3. Create ConfigMaps for application config
4. Deploy application with multiple replicas
5. Expose application with LoadBalancer service
6. Configure ingress for external access
```

### Blue-Green Deployment
```
1. Deploy new version (green) alongside current (blue)
2. Test green deployment thoroughly
3. Switch traffic from blue to green
4. Monitor application metrics
5. Remove blue deployment if successful
```

### Canary Deployment
```
1. Deploy canary version with small percentage of traffic
2. Monitor metrics and error rates
3. Gradually increase canary traffic
4. Rollback if issues detected
5. Complete rollout if successful
```

## Integration with Other MCPs

### With Docker MCP
```
# Container to orchestration workflow
1. Build images with docker MCP
2. Push to container registry
3. Deploy to Kubernetes with k8s MCP
4. Monitor and scale applications
```

### With Git MCP
```
# GitOps workflow
1. Use git MCP to manage manifests
2. Apply changes to cluster
3. Track deployment status
4. Rollback via git history
```

## Kubernetes Manifests Examples

### Deployment with Service
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
  labels:
    app: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: web
        image: nginx:1.21
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"
---
apiVersion: v1
kind: Service
metadata:
  name: web-app-service
spec:
  selector:
    app: web-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer
```

### ConfigMap and Secret
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  database_url: "postgresql://db:5432/myapp"
  log_level: "info"
---
apiVersion: v1
kind: Secret
metadata:
  name: app-secrets
type: Opaque
data:
  database_password: cGFzc3dvcmQ=  # base64 encoded
  api_key: YWJjZGVmZ2hpams=
```

## Links

- [Kubernetes MCP Repository](https://github.com/kubernetes-mcp/kubernetes-mcp-server)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [kubectl Reference](https://kubernetes.io/docs/reference/kubectl/)
- [Kubernetes API Reference](https://kubernetes.io/docs/reference/kubernetes-api/)
- [Helm Documentation](https://helm.sh/docs/)
- [Kustomize Documentation](https://kustomize.io/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Kubernetes Community](https://kubernetes.io/community/)
- [Kubernetes Slack](https://kubernetes.slack.com/)
- [MCP Discord](https://discord.gg/mcp)
- [CNCF Landscape](https://landscape.cncf.io/)
- [Kubernetes Best Practices](https://kubernetes.io/docs/concepts/configuration/overview/)

