# Docker MCP

## Overview
The Docker MCP provides Claude with comprehensive Docker container management capabilities, enabling container lifecycle management, image operations, network configuration, and volume management. This MCP is essential for containerized development workflows and DevOps operations.

## Installation

### Prerequisites
- Docker Engine installed and running
- Docker CLI accessible
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Appropriate Docker permissions

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx docker-mcp-server
```

#### Option 2: From GitHub
```bash
git clone https://github.com/QuantGeekDev/docker-mcp.git
cd docker-mcp
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install docker-mcp-server
```

#### Option 4: Docker Container
```bash
docker run -d --name docker-mcp \
  -v /var/run/docker.sock:/var/run/docker.sock \
  docker-mcp-server
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "docker": {
      "command": "npx",
      "args": ["docker-mcp-server"]
    }
  }
}
```

### With Custom Docker Host
```json
{
  "mcpServers": {
    "docker": {
      "command": "npx",
      "args": [
        "docker-mcp-server",
        "--host", "tcp://remote-docker:2376"
      ]
    }
  }
}
```

### With Docker Socket
```json
{
  "mcpServers": {
    "docker": {
      "command": "npx",
      "args": [
        "docker-mcp-server",
        "--socket", "/var/run/docker.sock"
      ]
    }
  }
}
```

### Environment Variables
```bash
export DOCKER_HOST=tcp://localhost:2376
export DOCKER_TLS_VERIFY=1
export DOCKER_CERT_PATH=/path/to/certs
```

## Usage Examples

### Container Management
```
# List running containers
Show me all currently running Docker containers.

# Start a new container
Start a new nginx container with port 80 exposed.

# Stop containers
Stop all containers with the label "environment=development".

# Remove containers
Remove all stopped containers to free up space.

# Container logs
Show me the logs for the container named "web-server".
```

### Image Operations
```
# List images
Show me all Docker images on this system.

# Pull images
Pull the latest Ubuntu 22.04 image from Docker Hub.

# Build images
Build a Docker image from the Dockerfile in the current directory.

# Tag images
Tag the image "myapp:latest" as "myapp:v1.0.0".

# Push images
Push the image "myapp:v1.0.0" to the registry.
```

### Advanced Container Operations
```
# Execute commands in containers
Run a bash shell in the running container "web-app".

# Copy files
Copy the file "config.json" from the host to the container "/app/config.json".

# Container inspection
Show me detailed information about the container "database".

# Resource monitoring
Display CPU and memory usage for all running containers.
```

### Docker Compose Integration
```
# Compose operations
Start all services defined in docker-compose.yml.

# Scale services
Scale the "web" service to 3 replicas.

# View compose logs
Show logs for all services in the compose stack.

# Compose down
Stop and remove all containers, networks, and volumes defined in compose.
```

## Features

### Container Lifecycle
- **Create**: Create new containers from images
- **Start/Stop**: Control container execution state
- **Restart**: Restart containers with various policies
- **Remove**: Clean up stopped containers
- **Pause/Unpause**: Temporarily suspend container execution

### Image Management
- **Pull**: Download images from registries
- **Build**: Create images from Dockerfiles
- **Tag**: Apply tags to images
- **Push**: Upload images to registries
- **Remove**: Delete unused images
- **History**: View image layer history

### Network Operations
- **Create Networks**: Set up custom networks
- **Connect/Disconnect**: Manage container network connections
- **List Networks**: View available networks
- **Inspect Networks**: Detailed network information
- **Remove Networks**: Clean up unused networks

### Volume Management
- **Create Volumes**: Set up persistent storage
- **Mount Volumes**: Attach volumes to containers
- **List Volumes**: View available volumes
- **Inspect Volumes**: Volume details and usage
- **Remove Volumes**: Clean up unused volumes

### Monitoring & Logs
- **Container Stats**: Real-time resource usage
- **Logs**: Container output and error logs
- **Events**: Docker daemon events
- **System Info**: Docker system information
- **Health Checks**: Container health monitoring

## Requirements

### System Requirements
- **Docker Engine**: Version 20.10 or higher
- **Operating System**: Linux, macOS, or Windows with WSL2
- **Memory**: 2GB+ available RAM
- **Disk Space**: Varies by images and containers
- **CPU**: Multi-core recommended for multiple containers

### Permissions
- Docker daemon access (usually via docker group)
- Read/write access to Docker socket
- Network permissions for container networking
- File system access for volume mounts

### Docker Configuration
```bash
# Add user to docker group (Linux)
sudo usermod -aG docker $USER

# Verify Docker installation
docker --version
docker info
```

## Security Considerations

### Best Practices
- **Least Privilege**: Run containers with minimal permissions
- **User Namespaces**: Use user namespace remapping
- **Resource Limits**: Set CPU and memory limits
- **Network Isolation**: Use custom networks for isolation
- **Image Security**: Scan images for vulnerabilities

### Secure Configuration
```json
{
  "mcpServers": {
    "docker": {
      "command": "npx",
      "args": [
        "docker-mcp-server",
        "--read-only",
        "--no-privileged"
      ]
    }
  }
}
```

### Docker Security Options
```bash
# Run container with security options
docker run --security-opt no-new-privileges \
  --cap-drop ALL \
  --cap-add NET_BIND_SERVICE \
  nginx
```

## Troubleshooting

### Common Issues

#### Docker Daemon Not Running
**Problem**: Cannot connect to Docker daemon
**Solution**:
```bash
# Start Docker service (Linux)
sudo systemctl start docker

# Start Docker Desktop (macOS/Windows)
# Launch Docker Desktop application

# Verify Docker is running
docker info
```

#### Permission Denied
**Problem**: Permission denied accessing Docker socket
**Solution**:
```bash
# Add user to docker group
sudo usermod -aG docker $USER
newgrp docker

# Or use sudo (not recommended for production)
sudo docker ps
```

#### Container Won't Start
**Problem**: Container fails to start
**Solution**:
- Check container logs: `docker logs <container>`
- Verify image exists: `docker images`
- Check port conflicts: `docker ps -a`
- Review resource constraints

#### Image Pull Failures
**Problem**: Cannot pull images from registry
**Solution**:
- Check network connectivity
- Verify registry credentials: `docker login`
- Check image name and tag
- Try alternative registry mirrors

### Diagnostic Commands
```bash
# System information
docker system info
docker system df

# Container diagnostics
docker inspect <container>
docker logs --details <container>

# Network diagnostics
docker network ls
docker network inspect bridge
```

## Advanced Configuration

### Custom Registry Configuration
```json
{
  "mcpServers": {
    "docker": {
      "command": "npx",
      "args": [
        "docker-mcp-server",
        "--registry", "my-registry.com:5000",
        "--insecure-registry"
      ]
    }
  }
}
```

### Docker Daemon Configuration
```json
{
  "hosts": ["unix:///var/run/docker.sock", "tcp://0.0.0.0:2376"],
  "tls": true,
  "tlscert": "/path/to/cert.pem",
  "tlskey": "/path/to/key.pem",
  "tlsverify": true,
  "tlscacert": "/path/to/ca.pem"
}
```

### Resource Constraints
```bash
# Set resource limits
docker run -d \
  --memory="512m" \
  --cpus="1.5" \
  --restart=unless-stopped \
  nginx
```

## Workflow Examples

### Development Workflow
```
1. Build application image
2. Start development containers
3. Mount source code volumes
4. Run tests in containers
5. Debug and iterate
```

### CI/CD Pipeline
```
1. Pull base images
2. Build application images
3. Run automated tests
4. Push images to registry
5. Deploy to staging/production
```

### Multi-Service Application
```
1. Define services in docker-compose.yml
2. Start all services with dependencies
3. Scale services based on load
4. Monitor service health
5. Update services rolling deployment
```

## Integration with Other MCPs

### With Git MCP
```
# Combined workflow
1. Use git MCP to clone repository
2. Use docker MCP to build images
3. Deploy containerized applications
```

### With Kubernetes MCP
```
# Container orchestration
1. Build images with docker MCP
2. Deploy to Kubernetes with k8s MCP
3. Monitor and scale applications
```

## Docker Compose Examples

### Basic Web Application
```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
    depends_on:
      - db
  
  db:
    image: postgres:13
    environment:
      - POSTGRES_DB=myapp
      - POSTGRES_PASSWORD=secret
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```

### Microservices Stack
```yaml
version: '3.8'
services:
  api:
    image: myapp/api:latest
    ports:
      - "8080:8080"
    networks:
      - backend
  
  frontend:
    image: myapp/frontend:latest
    ports:
      - "80:80"
    networks:
      - frontend
  
  database:
    image: postgres:13
    networks:
      - backend
    volumes:
      - db_data:/var/lib/postgresql/data

networks:
  frontend:
  backend:

volumes:
  db_data:
```

## Links

- [Docker MCP Repository](https://github.com/QuantGeekDev/docker-mcp)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Docker Security Best Practices](https://docs.docker.com/engine/security/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Docker Community](https://www.docker.com/community)
- [Docker Forums](https://forums.docker.com/)
- [MCP Discord](https://discord.gg/mcp)
- [Awesome Docker](https://github.com/veggiemonk/awesome-docker)
- [Docker Best Practices](https://docs.docker.com/develop/dev-best-practices/)

