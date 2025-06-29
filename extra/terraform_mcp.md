# Terraform MCP

## Overview
The Terraform MCP provides Claude with comprehensive Infrastructure as Code (IaC) capabilities, enabling infrastructure provisioning, state management, and resource orchestration across multiple cloud providers. This MCP is essential for managing infrastructure declaratively and implementing GitOps workflows.

## Installation

### Prerequisites
- Terraform CLI installed (version 1.0+)
- Cloud provider credentials configured
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Access to Terraform state storage

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx terraform-mcp-server
```

#### Option 2: From GitHub
```bash
git clone https://github.com/terraform-mcp/terraform-mcp-server.git
cd terraform-mcp-server
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install terraform-mcp-server
```

#### Option 4: Terraform Provider
```hcl
terraform {
  required_providers {
    mcp = {
      source = "terraform-mcp/mcp"
      version = "~> 1.0"
    }
  }
}
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "terraform": {
      "command": "npx",
      "args": ["terraform-mcp-server"]
    }
  }
}
```

### With Specific Working Directory
```json
{
  "mcpServers": {
    "terraform": {
      "command": "npx",
      "args": [
        "terraform-mcp-server",
        "--working-dir", "/path/to/terraform/project"
      ]
    }
  }
}
```

### With Multiple Environments
```json
{
  "mcpServers": {
    "terraform-prod": {
      "command": "npx",
      "args": [
        "terraform-mcp-server",
        "--working-dir", "/path/to/terraform/production",
        "--workspace", "production"
      ]
    },
    "terraform-staging": {
      "command": "npx",
      "args": [
        "terraform-mcp-server",
        "--working-dir", "/path/to/terraform/staging",
        "--workspace", "staging"
      ]
    }
  }
}
```

### Environment Variables
```bash
export TF_VAR_region=us-west-2
export TF_VAR_environment=production
export AWS_ACCESS_KEY_ID=your-access-key
export AWS_SECRET_ACCESS_KEY=your-secret-key
export TERRAFORM_WORKSPACE=production
```

## Usage Examples

### Basic Terraform Operations
```
# Initialize Terraform
Initialize the Terraform working directory with required providers.

# Plan infrastructure changes
Generate and show an execution plan for the current configuration.

# Apply changes
Apply the Terraform configuration to create or update infrastructure.

# Show current state
Display the current state of managed infrastructure resources.

# Destroy infrastructure
Destroy all resources managed by this Terraform configuration.
```

### State Management
```
# List resources in state
Show all resources currently tracked in the Terraform state.

# Import existing resources
Import the existing AWS EC2 instance i-1234567890abcdef0 into Terraform state.

# Remove resources from state
Remove the aws_instance.example resource from Terraform state without destroying it.

# Move resources in state
Move the aws_instance.old_name resource to aws_instance.new_name in state.

# Refresh state
Update the state file with real-world resource information.
```

### Workspace Management
```
# List workspaces
Show all available Terraform workspaces.

# Create new workspace
Create a new workspace called "development".

# Switch workspaces
Switch to the "production" workspace.

# Delete workspace
Delete the "old-environment" workspace.

# Show current workspace
Display the currently selected workspace.
```

### Advanced Operations
```
# Validate configuration
Check whether the Terraform configuration is valid.

# Format configuration
Format all Terraform configuration files in the current directory.

# Generate dependency graph
Create a visual dependency graph of the Terraform resources.

# Taint resources
Mark the aws_instance.web resource for recreation on next apply.

# Untaint resources
Remove the taint from the aws_instance.web resource.
```

## Features

### Core Terraform Operations
- **Infrastructure Planning**: Generate execution plans before applying changes
- **Resource Management**: Create, update, and destroy infrastructure resources
- **State Management**: Track and manage infrastructure state
- **Provider Integration**: Support for 100+ cloud and service providers
- **Workspace Management**: Manage multiple environments and configurations

### Advanced Features
- **Remote State**: Store state in remote backends (S3, Consul, Terraform Cloud)
- **State Locking**: Prevent concurrent modifications to state
- **Module System**: Reusable infrastructure components
- **Variable Management**: Parameterize configurations with variables
- **Output Values**: Extract information from infrastructure

### Multi-Cloud Support
- **AWS**: Complete AWS resource management
- **Azure**: Microsoft Azure infrastructure provisioning
- **Google Cloud**: GCP resource orchestration
- **Kubernetes**: Container orchestration platform management
- **VMware**: On-premises virtualization infrastructure

### DevOps Integration
- **CI/CD Pipelines**: Integrate with Jenkins, GitLab CI, GitHub Actions
- **Version Control**: Git-based infrastructure versioning
- **Policy as Code**: Implement governance with Sentinel or OPA
- **Cost Management**: Track and optimize infrastructure costs
- **Compliance**: Ensure infrastructure meets regulatory requirements

## Requirements

### System Requirements
- **Terraform**: Version 1.0 or higher
- **Operating System**: Linux, macOS, or Windows
- **Memory**: 1GB+ available RAM
- **Disk Space**: Varies by provider and resource count
- **Network**: Internet access for provider APIs

### Provider Requirements
```hcl
terraform {
  required_version = ">= 1.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
    google = {
      source  = "hashicorp/google"
      version = "~> 4.0"
    }
  }
}
```

### Authentication
- Cloud provider credentials properly configured
- Service account keys or access tokens
- Appropriate IAM permissions for resource management
- Network access to cloud provider APIs

## Security Considerations

### Best Practices
- **State Security**: Encrypt state files and use remote backends
- **Credential Management**: Use environment variables or credential files
- **Least Privilege**: Grant minimal required permissions
- **State Locking**: Enable state locking to prevent conflicts
- **Sensitive Data**: Mark sensitive variables appropriately

### Secure Configuration
```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-state-bucket"
    key            = "production/terraform.tfstate"
    region         = "us-west-2"
    encrypt        = true
    dynamodb_table = "terraform-locks"
  }
}

variable "database_password" {
  description = "Database password"
  type        = string
  sensitive   = true
}
```

### Access Control
```json
{
  "mcpServers": {
    "terraform": {
      "command": "npx",
      "args": [
        "terraform-mcp-server",
        "--read-only",
        "--workspace", "production"
      ]
    }
  }
}
```

## Troubleshooting

### Common Issues

#### Provider Authentication Failed
**Problem**: Cannot authenticate with cloud provider
**Solution**:
```bash
# AWS
aws configure list
aws sts get-caller-identity

# Azure
az account show
az login

# Google Cloud
gcloud auth list
gcloud auth application-default login
```

#### State Lock Conflicts
**Problem**: State is locked by another operation
**Solution**:
```bash
# Force unlock (use with caution)
terraform force-unlock LOCK_ID

# Check lock status
terraform state list
```

#### Resource Conflicts
**Problem**: Resources already exist or conflicts detected
**Solution**:
```bash
# Import existing resources
terraform import aws_instance.example i-1234567890abcdef0

# Show detailed plan
terraform plan -detailed-exitcode
```

#### Configuration Errors
**Problem**: Invalid Terraform configuration
**Solution**:
```bash
# Validate configuration
terraform validate

# Format configuration
terraform fmt -recursive

# Check syntax
terraform plan -input=false
```

### Diagnostic Commands
```bash
# Terraform version
terraform version

# Provider versions
terraform providers

# Configuration validation
terraform validate

# State inspection
terraform show
terraform state list
```

## Advanced Configuration

### Remote Backend Configuration
```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "infrastructure/terraform.tfstate"
    region         = "us-west-2"
    encrypt        = true
    dynamodb_table = "terraform-state-locks"
    
    # Optional: workspace-specific state
    workspace_key_prefix = "workspaces"
  }
}
```

### Module Development
```hcl
# modules/vpc/main.tf
variable "cidr_block" {
  description = "CIDR block for VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "availability_zones" {
  description = "Availability zones"
  type        = list(string)
}

resource "aws_vpc" "main" {
  cidr_block           = var.cidr_block
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name = "main-vpc"
  }
}

output "vpc_id" {
  description = "ID of the VPC"
  value       = aws_vpc.main.id
}
```

### Variable Configuration
```hcl
# variables.tf
variable "environment" {
  description = "Environment name"
  type        = string
  validation {
    condition     = contains(["dev", "staging", "prod"], var.environment)
    error_message = "Environment must be dev, staging, or prod."
  }
}

variable "instance_types" {
  description = "EC2 instance types by environment"
  type        = map(string)
  default = {
    dev     = "t3.micro"
    staging = "t3.small"
    prod    = "t3.medium"
  }
}
```

## Terraform Examples

### Basic AWS Infrastructure
```hcl
# main.tf
provider "aws" {
  region = var.aws_region
}

resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name        = "${var.project_name}-vpc"
    Environment = var.environment
  }
}

resource "aws_subnet" "public" {
  count             = length(var.availability_zones)
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.${count.index + 1}.0/24"
  availability_zone = var.availability_zones[count.index]

  map_public_ip_on_launch = true

  tags = {
    Name = "${var.project_name}-public-${count.index + 1}"
    Type = "public"
  }
}

resource "aws_internet_gateway" "main" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "${var.project_name}-igw"
  }
}

resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.main.id
  }

  tags = {
    Name = "${var.project_name}-public-rt"
  }
}

resource "aws_route_table_association" "public" {
  count          = length(aws_subnet.public)
  subnet_id      = aws_subnet.public[count.index].id
  route_table_id = aws_route_table.public.id
}
```

### Kubernetes Cluster
```hcl
# kubernetes.tf
resource "aws_eks_cluster" "main" {
  name     = "${var.project_name}-cluster"
  role_arn = aws_iam_role.cluster.arn
  version  = var.kubernetes_version

  vpc_config {
    subnet_ids              = aws_subnet.private[*].id
    endpoint_private_access = true
    endpoint_public_access  = true
    public_access_cidrs     = var.allowed_cidr_blocks
  }

  encryption_config {
    provider {
      key_arn = aws_kms_key.eks.arn
    }
    resources = ["secrets"]
  }

  depends_on = [
    aws_iam_role_policy_attachment.cluster_AmazonEKSClusterPolicy,
  ]

  tags = {
    Name        = "${var.project_name}-cluster"
    Environment = var.environment
  }
}

resource "aws_eks_node_group" "main" {
  cluster_name    = aws_eks_cluster.main.name
  node_group_name = "${var.project_name}-nodes"
  node_role_arn   = aws_iam_role.node_group.arn
  subnet_ids      = aws_subnet.private[*].id

  scaling_config {
    desired_size = var.node_desired_size
    max_size     = var.node_max_size
    min_size     = var.node_min_size
  }

  update_config {
    max_unavailable = 1
  }

  instance_types = [var.node_instance_type]
  capacity_type  = "ON_DEMAND"

  depends_on = [
    aws_iam_role_policy_attachment.node_group_AmazonEKSWorkerNodePolicy,
    aws_iam_role_policy_attachment.node_group_AmazonEKS_CNI_Policy,
    aws_iam_role_policy_attachment.node_group_AmazonEC2ContainerRegistryReadOnly,
  ]

  tags = {
    Name        = "${var.project_name}-nodes"
    Environment = var.environment
  }
}
```

### Multi-Environment Setup
```hcl
# environments/production/main.tf
module "infrastructure" {
  source = "../../modules/infrastructure"

  environment         = "production"
  instance_type      = "t3.large"
  min_size           = 3
  max_size           = 10
  desired_capacity   = 5
  
  database_instance_class = "db.r5.xlarge"
  database_allocated_storage = 100
  
  enable_monitoring = true
  enable_backups   = true
  
  tags = {
    Environment = "production"
    Owner       = "platform-team"
    Project     = "main-application"
  }
}
```

## Integration with Other MCPs

### With Git MCP
```
# GitOps workflow
1. Use git MCP to manage Terraform configurations
2. Use terraform MCP to apply infrastructure changes
3. Track infrastructure changes via version control
```

### With Kubernetes MCP
```
# Container infrastructure workflow
1. Use terraform MCP to provision Kubernetes cluster
2. Use kubernetes MCP to deploy applications
3. Manage both infrastructure and applications
```

### With Ansible MCP
```
# Hybrid infrastructure management
1. Use terraform MCP for resource provisioning
2. Use ansible MCP for configuration management
3. Coordinate infrastructure and configuration
```

## Workflow Examples

### Infrastructure Provisioning
```
1. Define infrastructure requirements
2. Create Terraform configurations
3. Plan and review changes
4. Apply infrastructure changes
5. Validate deployed resources
```

### Environment Management
```
1. Create workspace for new environment
2. Customize variables for environment
3. Deploy infrastructure with terraform apply
4. Configure monitoring and alerting
5. Document environment specifications
```

### Disaster Recovery
```
1. Backup Terraform state and configurations
2. Document recovery procedures
3. Test recovery in staging environment
4. Implement automated backup processes
5. Maintain recovery runbooks
```

## Links

- [Terraform MCP Repository](https://github.com/terraform-mcp/terraform-mcp-server)
- [Terraform Documentation](https://www.terraform.io/docs/)
- [Terraform Registry](https://registry.terraform.io/)
- [Terraform Best Practices](https://www.terraform.io/docs/cloud/guides/recommended-practices/)
- [HashiCorp Learn](https://learn.hashicorp.com/terraform)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Terraform Community](https://www.terraform.io/community.html)
- [HashiCorp Discuss](https://discuss.hashicorp.com/c/terraform-core/)
- [MCP Discord](https://discord.gg/mcp)
- [Awesome Terraform](https://github.com/shuaibiyy/awesome-terraform)
- [Terraform Examples](https://github.com/hashicorp/terraform-guides)

