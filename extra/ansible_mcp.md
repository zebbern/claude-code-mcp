# Ansible MCP

## Overview
The Ansible MCP provides Claude with comprehensive automation and configuration management capabilities, enabling infrastructure provisioning, application deployment, and system administration tasks. This MCP is essential for Infrastructure as Code (IaC) workflows and DevOps automation.

## Installation

### Prerequisites
- Ansible installed on your system
- Python 3.8+ with ansible-core
- SSH access to target hosts
- Claude Desktop application
- Inventory files configured

### Install Steps

#### Option 1: NPX (Recommended)
```bash
npx ansible-mcp-server
```

#### Option 2: From GitHub
```bash
git clone https://github.com/ansible-mcp/ansible-mcp-server.git
cd ansible-mcp-server
npm install
npm run build
```

#### Option 3: Python Implementation
```bash
pip install ansible-mcp-server
```

#### Option 4: Ansible Collection
```bash
ansible-galaxy collection install community.mcp
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "ansible": {
      "command": "npx",
      "args": ["ansible-mcp-server"]
    }
  }
}
```

### With Custom Inventory
```json
{
  "mcpServers": {
    "ansible": {
      "command": "npx",
      "args": [
        "ansible-mcp-server",
        "--inventory", "/path/to/inventory.yml"
      ]
    }
  }
}
```

### With Ansible Configuration
```json
{
  "mcpServers": {
    "ansible": {
      "command": "npx",
      "args": [
        "ansible-mcp-server",
        "--config", "/path/to/ansible.cfg",
        "--vault-password-file", "/path/to/vault-pass"
      ]
    }
  }
}
```

### Environment Variables
```bash
export ANSIBLE_CONFIG=/path/to/ansible.cfg
export ANSIBLE_INVENTORY=/path/to/inventory
export ANSIBLE_VAULT_PASSWORD_FILE=/path/to/vault-pass
export ANSIBLE_HOST_KEY_CHECKING=False
```

## Usage Examples

### Basic Ansible Operations
```
# Run ad-hoc commands
Run the command "uptime" on all web servers.

# Check connectivity
Ping all hosts in the inventory to check connectivity.

# Gather facts
Collect system information from all database servers.

# Install packages
Install nginx on all web servers using the package module.

# Manage services
Ensure the apache2 service is running on all web servers.
```

### Playbook Execution
```
# Run playbooks
Execute the site.yml playbook against the production inventory.

# Dry run playbooks
Run the deployment playbook in check mode to see what would change.

# Limit execution
Run the update playbook only on the web-server group.

# Tag-based execution
Execute only tasks tagged with "configuration" from the main playbook.

# Vault operations
Run the secure playbook using the encrypted vault file.
```

### Infrastructure Management
```
# Server provisioning
Provision new web servers using the server-setup playbook.

# Configuration management
Apply the latest configuration to all application servers.

# Software deployment
Deploy the latest application version to staging environment.

# System updates
Update all packages on production servers during maintenance window.

# Security hardening
Apply security configurations to all servers.
```

### Advanced Automation
```
# Rolling deployments
Perform a rolling deployment of the application with zero downtime.

# Backup operations
Execute backup procedures across all database servers.

# Monitoring setup
Deploy monitoring agents to all infrastructure components.

# Load balancer management
Update load balancer configuration for new server additions.
```

## Features

### Core Ansible Capabilities
- **Ad-hoc Commands**: Execute single commands across multiple hosts
- **Playbook Execution**: Run complex automation workflows
- **Inventory Management**: Manage static and dynamic inventories
- **Module Execution**: Use Ansible's extensive module library
- **Fact Gathering**: Collect system information from hosts

### Advanced Features
- **Ansible Vault**: Encrypt sensitive data and variables
- **Role Management**: Organize and reuse automation code
- **Template Processing**: Generate configuration files from templates
- **Conditional Execution**: Execute tasks based on conditions
- **Error Handling**: Implement robust error handling and recovery

### Infrastructure as Code
- **Declarative Configuration**: Define desired system state
- **Idempotent Operations**: Safe to run multiple times
- **Version Control**: Track infrastructure changes
- **Environment Management**: Separate dev/staging/production
- **Compliance Automation**: Ensure systems meet standards

### Integration Capabilities
- **Cloud Providers**: AWS, Azure, GCP, DigitalOcean
- **Container Platforms**: Docker, Kubernetes, OpenShift
- **Network Devices**: Cisco, Juniper, F5, Palo Alto
- **Monitoring Tools**: Prometheus, Grafana, Nagios
- **CI/CD Pipelines**: Jenkins, GitLab CI, GitHub Actions

## Requirements

### System Requirements
- **Ansible**: Version 2.9 or higher (ansible-core 2.12+ recommended)
- **Python**: Version 3.8 or higher
- **Operating System**: Linux, macOS, or Windows (WSL)
- **Memory**: 1GB+ available RAM
- **Network**: SSH access to managed hosts

### Target Host Requirements
- **SSH Server**: OpenSSH or compatible
- **Python**: Python 2.7 or 3.5+ on managed hosts
- **Sudo Access**: For privileged operations
- **Network Connectivity**: Reachable from control node

### Authentication Setup
```bash
# Generate SSH key
ssh-keygen -t rsa -b 4096 -C "ansible@example.com"

# Copy public key to hosts
ssh-copy-id user@target-host

# Test SSH connectivity
ssh user@target-host
```

## Security Considerations

### Best Practices
- **SSH Keys**: Use SSH key authentication instead of passwords
- **Ansible Vault**: Encrypt sensitive variables and files
- **Least Privilege**: Use minimal required permissions
- **Network Security**: Restrict SSH access with firewalls
- **Audit Logging**: Enable comprehensive logging

### Secure Configuration
```ini
# ansible.cfg
[defaults]
host_key_checking = True
ansible_ssh_pipelining = True
vault_password_file = /secure/path/vault-pass

[ssh_connection]
ssh_args = -o ControlMaster=auto -o ControlPersist=60s -o UserKnownHostsFile=/dev/null
```

### Vault Usage
```bash
# Create encrypted file
ansible-vault create secrets.yml

# Edit encrypted file
ansible-vault edit secrets.yml

# Encrypt existing file
ansible-vault encrypt vars.yml

# Decrypt file
ansible-vault decrypt vars.yml
```

## Troubleshooting

### Common Issues

#### SSH Connection Failed
**Problem**: Cannot connect to target hosts
**Solution**:
```bash
# Test SSH connectivity
ssh -vvv user@target-host

# Check SSH agent
ssh-add -l

# Verify host key
ssh-keyscan target-host >> ~/.ssh/known_hosts
```

#### Permission Denied
**Problem**: Insufficient privileges on target hosts
**Solution**:
```bash
# Test sudo access
ssh user@target-host sudo whoami

# Configure passwordless sudo
echo "user ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/user
```

#### Module Not Found
**Problem**: Ansible module not available
**Solution**:
```bash
# List available modules
ansible-doc -l

# Install collections
ansible-galaxy collection install community.general

# Check module documentation
ansible-doc module_name
```

#### Playbook Syntax Error
**Problem**: YAML syntax errors in playbooks
**Solution**:
```bash
# Validate playbook syntax
ansible-playbook --syntax-check playbook.yml

# Check YAML syntax
python -c "import yaml; yaml.safe_load(open('playbook.yml'))"
```

### Diagnostic Commands
```bash
# Test inventory
ansible-inventory --list

# Check connectivity
ansible all -m ping

# Gather facts
ansible all -m setup

# Test module
ansible localhost -m debug -a "msg='Hello World'"
```

## Advanced Configuration

### Dynamic Inventory
```python
#!/usr/bin/env python3
# dynamic_inventory.py
import json
import subprocess

def get_inventory():
    # Custom logic to generate inventory
    inventory = {
        'web': {
            'hosts': ['web1.example.com', 'web2.example.com'],
            'vars': {'http_port': 80}
        },
        'db': {
            'hosts': ['db1.example.com'],
            'vars': {'mysql_port': 3306}
        }
    }
    return inventory

if __name__ == '__main__':
    print(json.dumps(get_inventory()))
```

### Custom Modules
```python
#!/usr/bin/python
# library/custom_module.py

from ansible.module_utils.basic import AnsibleModule

def main():
    module = AnsibleModule(
        argument_spec=dict(
            name=dict(type='str', required=True),
            state=dict(type='str', default='present', choices=['present', 'absent'])
        )
    )
    
    name = module.params['name']
    state = module.params['state']
    
    # Custom module logic here
    result = {'changed': False, 'name': name}
    
    module.exit_json(**result)

if __name__ == '__main__':
    main()
```

### Ansible Configuration
```ini
# ansible.cfg
[defaults]
inventory = ./inventory
remote_user = ansible
private_key_file = ~/.ssh/ansible_key
host_key_checking = False
retry_files_enabled = False
gathering = smart
fact_caching = jsonfile
fact_caching_connection = /tmp/ansible_facts
fact_caching_timeout = 86400

[ssh_connection]
ssh_args = -o ControlMaster=auto -o ControlPersist=60s
pipelining = True
```

## Playbook Examples

### Basic Server Setup
```yaml
---
- name: Basic server setup
  hosts: all
  become: yes
  tasks:
    - name: Update package cache
      apt:
        update_cache: yes
        cache_valid_time: 3600
      when: ansible_os_family == "Debian"
    
    - name: Install essential packages
      package:
        name:
          - curl
          - wget
          - git
          - htop
        state: present
    
    - name: Create application user
      user:
        name: appuser
        shell: /bin/bash
        create_home: yes
    
    - name: Configure SSH
      lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^PasswordAuthentication'
        line: 'PasswordAuthentication no'
      notify: restart ssh
  
  handlers:
    - name: restart ssh
      service:
        name: ssh
        state: restarted
```

### Application Deployment
```yaml
---
- name: Deploy web application
  hosts: web
  become: yes
  vars:
    app_name: myapp
    app_version: "{{ version | default('latest') }}"
    app_port: 3000
  
  tasks:
    - name: Install Node.js
      apt:
        name: nodejs
        state: present
    
    - name: Create application directory
      file:
        path: "/opt/{{ app_name }}"
        state: directory
        owner: appuser
        group: appuser
    
    - name: Download application
      get_url:
        url: "https://releases.example.com/{{ app_name }}-{{ app_version }}.tar.gz"
        dest: "/tmp/{{ app_name }}-{{ app_version }}.tar.gz"
    
    - name: Extract application
      unarchive:
        src: "/tmp/{{ app_name }}-{{ app_version }}.tar.gz"
        dest: "/opt/{{ app_name }}"
        remote_src: yes
        owner: appuser
        group: appuser
    
    - name: Install dependencies
      npm:
        path: "/opt/{{ app_name }}"
        state: present
      become_user: appuser
    
    - name: Start application service
      systemd:
        name: "{{ app_name }}"
        state: started
        enabled: yes
```

### Rolling Deployment
```yaml
---
- name: Rolling deployment
  hosts: web
  serial: 1
  max_fail_percentage: 0
  
  pre_tasks:
    - name: Remove from load balancer
      uri:
        url: "http://lb.example.com/api/remove/{{ inventory_hostname }}"
        method: POST
      delegate_to: localhost
  
  tasks:
    - name: Deploy new version
      include_tasks: deploy.yml
    
    - name: Health check
      uri:
        url: "http://{{ inventory_hostname }}:{{ app_port }}/health"
        status_code: 200
      retries: 5
      delay: 10
  
  post_tasks:
    - name: Add back to load balancer
      uri:
        url: "http://lb.example.com/api/add/{{ inventory_hostname }}"
        method: POST
      delegate_to: localhost
```

## Integration with Other MCPs

### With Git MCP
```
# GitOps workflow
1. Use git MCP to clone infrastructure repository
2. Use ansible MCP to apply configurations
3. Track changes and rollbacks via git
```

### With Docker MCP
```
# Container deployment workflow
1. Use ansible MCP to provision hosts
2. Use docker MCP to deploy containers
3. Use ansible MCP for host-level configuration
```

### With Kubernetes MCP
```
# Hybrid infrastructure
1. Use ansible MCP for node preparation
2. Use kubernetes MCP for container orchestration
3. Use ansible MCP for cluster maintenance
```

## Workflow Examples

### Infrastructure Provisioning
```
1. Define infrastructure in inventory
2. Create provisioning playbooks
3. Execute server setup automation
4. Configure monitoring and logging
5. Deploy applications
```

### Configuration Management
```
1. Define desired system state
2. Create configuration playbooks
3. Apply configurations across environments
4. Validate compliance
5. Report on changes
```

### Application Lifecycle
```
1. Provision infrastructure
2. Deploy application stack
3. Configure load balancing
4. Set up monitoring
5. Implement backup procedures
```

## Links

- [Ansible MCP Repository](https://github.com/ansible-mcp/ansible-mcp-server)
- [Ansible Documentation](https://docs.ansible.com/)
- [Ansible Galaxy](https://galaxy.ansible.com/)
- [Ansible Modules](https://docs.ansible.com/ansible/latest/collections/index.html)
- [Ansible Best Practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Ansible Community](https://www.ansible.com/community)
- [Ansible Mailing Lists](https://groups.google.com/forum/#!forum/ansible-project)
- [MCP Discord](https://discord.gg/mcp)
- [Awesome Ansible](https://github.com/KeyboardInterrupt/awesome-ansible)
- [Ansible Examples](https://github.com/ansible/ansible-examples)

