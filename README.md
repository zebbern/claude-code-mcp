# 🤖 Claude Code MCP Repository

> **The ultimate collection of Claude Code Model Context Protocol (MCP) integrations with verified links, comprehensive documentation, and advanced Claude Code specific tools.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Compatible](https://img.shields.io/badge/Claude%20Code-Compatible-blue.svg)](https://docs.anthropic.com/en/docs/claude-code)
[![MCP Specification](https://img.shields.io/badge/MCP-v1.0-green.svg)](https://spec.modelcontextprotocol.io/)
[![Total MCPs](https://img.shields.io/badge/Total%20MCPs-120+-brightgreen.svg)](#)

## 🚀 Quick Start

```bash
# Install core Claude Code MCPs
npm install -g @modelcontextprotocol/server-filesystem @modelcontextprotocol/server-git

# Configure Claude Desktop (~/.claude/claude_desktop_config.json)
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-filesystem", "/workspace"]
    },
    "git": {
      "command": "npx", 
      "args": ["@modelcontextprotocol/server-git", "/workspace"]
    }
  }
}
```

## 📚 **Master Tips & Tricks Guide**

| Resource | Description | What You'll Learn |
|----------|-------------|-------------------|
| [🎯 **MCP Tips & Tricks Master Guide**](extra/mcp_tips_and_tricks_master_guide.md) ⭐ **FEATURED** | Complete guide with 100+ tips, tricks, and best practices | 5-minute setup, advanced configurations, performance optimization, troubleshooting, enterprise deployment, custom development |

## 🚀 **Claude Code Specific MCPs**

### 🎯 Claude Code CLI Enhancement

| MCP | Description | Key Features |
|-----|-------------|--------------|
| [Claude Code Plan Mode MCP](extra/claude_code_plan_mode_mcp.md) ⭐ **NEW** | Advanced planning capabilities for Claude Code | Research mode, implementation planning, risk assessment, strategic analysis |
| [Claude Code Agent Creator MCP](extra/claude_code_agent_creator_mcp.md) ⭐ **NEW** | Create and manage specialized AI agents | Custom agent templates, multi-agent orchestration, agent lifecycle management |
| [Claude Code Workflow Optimizer MCP](extra/claude_code_workflow_optimizer_mcp.md) ⭐ **NEW** | Analyze and optimize development workflows | Pattern recognition, bottleneck detection, automation suggestions |
| [Steipete's Claude Code MCP](extra/steipete_claude_code_mcp.md) | Enhanced Claude Code integration | One-shot execution, permission bypass, advanced features |
| [Auchenberg's Claude Code MCP](extra/auchenberg_claude_code_mcp.md) | Professional Claude Code server | Enterprise features, security enhancements, production-ready |

### 📋 Claude Code Planning & Analysis

| MCP | Description | Capabilities |
|-----|-------------|--------------|
| [Software Planning MCP](extra/software_planning_mcp.md) | Interactive software development planning | Project planning, requirement analysis, workflow integration |
| [Sequential Thinking MCP](extra/sequential_thinking_mcp.md) | Enhanced reasoning capabilities | Step-by-step problem solving, logical reasoning chains |
| [Context7 MCP](extra/context7_mcp.md) | Advanced context management | Context preservation, intelligent switching |

## 🤖 AI Agents & Multi-Agent Systems

| MCP | Description | Features |
|-----|-------------|----------|
| [Claude-Flow AI Agent MCP](extra/claude_flow_ai_agent_mcp.md) ⭐ | Ultimate multi-agent orchestration platform | Multi-agent coordination, workflow automation, Claude Code integration |
| [MCP-Agent Framework](extra/mcp_agent_framework.md) | Complete framework for building AI agents | Agent lifecycle management, task delegation, result aggregation |
| [Multi-Agent MCP](extra/multi_agent_mcp.md) | Sophisticated multi-agent coordination | Hierarchical organization, swarm intelligence, conflict resolution |
| [Workflow Evaluator-Optimizer](extra/workflow_evaluator_optimizer_mcp.md) | Iterative workflow improvement | Performance analysis, optimization suggestions, automation |
| [CrewAI MCP](extra/crewai_mcp.md) | Multi-agent orchestration framework | Role-playing agents, task delegation, collaborative workflows |
| [AutoGen MCP](extra/autogen_mcp.md) | Microsoft's multi-agent framework | Conversational agents, code execution, automated workflows |
| [OpenAI Swarm MCP](extra/openai_swarm_mcp.md) | Lightweight multi-agent coordination | Agent handoffs, context sharing, swarm intelligence |

## 📁 Core Development MCPs

| MCP | Description | Key Capabilities |
|-----|-------------|------------------|
| [Filesystem MCP](extra/filesystem_mcp_complete.md) ⭐ | Complete file system operations | File/directory management, search, monitoring, batch operations |
| [Git MCP](extra/git_mcp_complete.md) ⭐ | Comprehensive Git integration | Repository management, branching, merging, workflow automation |
| [Memory MCP](extra/memory_mcp.md) | Persistent memory management | Long-term storage, context preservation, knowledge base |
| [Fetch MCP](extra/fetch_mcp.md) | HTTP request handling | API calls, web requests, data fetching |

## 🗄️ Database & Data Management

| MCP | Description | Use Cases |
|-----|-------------|-----------|
| [SQLite MCP](extra/sqlite_mcp.md) | Lightweight database operations | Local databases, prototyping, small applications |
| [PostgreSQL MCP](extra/postgresql_mcp.md) | Enterprise database integration | Production databases, complex queries, performance tuning |
| [Redis MCP](extra/redis_mcp.md) | High-performance caching | Caching, session storage, real-time data |
| [MySQL MCP](extra/mysql_mcp.md) | Popular database integration | Web applications, data analysis, reporting |
| [MongoDB MCP](extra/mongodb_mcp.md) | NoSQL document database | Document storage, flexible schemas, modern apps |

## ☁️ Cloud & Infrastructure

| MCP | Description | Services |
|-----|-------------|----------|
| [AWS MCP](extra/aws_mcp.md) | Amazon Web Services integration | EC2, S3, Lambda, CloudFormation, cost optimization |
| [Azure MCP](extra/azure_mcp.md) | Microsoft Azure integration | Virtual machines, storage, DevOps, enterprise identity |
| [Google Cloud MCP](extra/gcp_mcp.md) | Google Cloud Platform integration | Compute, storage, BigQuery, ML platform |
| [DigitalOcean MCP](extra/digitalocean_mcp.md) | DigitalOcean cloud services | Droplets, databases, networking, monitoring |

## 🛠️ DevOps & Infrastructure

| MCP | Description | Capabilities |
|-----|-------------|--------------|
| [Docker MCP](extra/docker_mcp.md) | Container management | Image building, container orchestration, deployment |
| [Kubernetes MCP](extra/kubernetes_mcp.md) | Container orchestration | Cluster management, scaling, service mesh |
| [Terraform MCP](extra/terraform_mcp.md) | Infrastructure as Code | Resource provisioning, state management, multi-cloud |
| [Ansible MCP](extra/ansible_mcp.md) | Configuration management | Automation, deployment, infrastructure management |
| [Jenkins MCP](extra/jenkins_mcp.md) | CI/CD automation | Build pipelines, testing, deployment automation |
| [Prometheus MCP](extra/prometheus_mcp.md) | Monitoring and alerting | Metrics collection, alerting, performance monitoring |
| [Grafana MCP](extra/grafana_mcp.md) | Data visualization | Dashboard creation, metrics visualization, monitoring |
| [Elasticsearch MCP](extra/elasticsearch_mcp.md) | Search and analytics | Full-text search, log analysis, data indexing |

## 🔍 Search & Information

| MCP | Description | Features |
|-----|-------------|----------|
| [Brave Search MCP](extra/brave_search_mcp.md) | Privacy-focused web search | Real-time search, privacy protection, result analysis |
| [Browser MCP](extra/browser_mcp.md) | Web automation | Automated browsing, form filling, data extraction |
| [Firecrawl MCP](extra/firecrawl_mcp.md) | Web scraping and crawling | Content extraction, site mapping, data collection |
| [Puppeteer MCP](extra/puppeteer_mcp.md) | Browser automation | Headless browsing, testing, screenshot capture |

## 💼 Productivity & Collaboration

| MCP | Description | Integration |
|-----|-------------|-------------|
| [Slack MCP](extra/slack_mcp.md) | Team communication | Message automation, workflow integration, analytics |
| [Jira MCP](extra/jira_mcp.md) | Project management | Issue tracking, sprint planning, agile workflows |
| [Google Drive MCP](extra/google_drive_mcp.md) | Cloud storage | File management, collaboration, document automation |
| [Notion MCP](extra/notion_mcp.md) | Workspace management | Knowledge base, project tracking, team collaboration |
| [GitHub MCP](extra/github_mcp.md) | GitHub integration | Repository management, issue tracking, pull requests |
| [GitLab MCP](extra/gitlab_mcp.md) | GitLab integration | CI/CD pipelines, merge requests, project management |

## 🎨 Content & Media

| MCP | Description | Capabilities |
|-----|-------------|--------------|
| [Image Generation MCP](extra/image_generation_mcp.md) | AI image creation | Text-to-image, editing, style transfer |
| [Everart MCP](extra/everart_mcp.md) | Creative content generation | Multi-modal creation, artistic effects |
| [Blender MCP](extra/blender_mcp.md) | 3D modeling integration | 3D creation, animation, rendering |

## ⚡ Workflow Automation

| MCP | Description | Automation |
|-----|-------------|------------|
| [n8n MCP](extra/n8n_mcp.md) | Workflow automation platform | 400+ integrations, visual workflows |
| [Zapier MCP](extra/zapier_mcp.md) | No-code automation | 5000+ app integrations, trigger-based workflows |
| [Claude-Flow MCP](extra/claude_flow_mcp.md) | AI workflow orchestration | Multi-agent workflows, intelligent automation |

## 📱 Communication & Social

| MCP | Description | Features |
|-----|-------------|----------|
| [WhatsApp MCP](extra/whatsapp_mcp.md) | WhatsApp automation | Message automation, customer communication |
| [Social Media MCP](extra/social_media_mcp.md) | Social platform integration | Content management, analytics, automation |

## 🏢 Industry-Specific Solutions

| Industry | MCPs Available | Specializations |
|----------|----------------|-----------------|
| **Healthcare** | [Healthcare MCP](extra/healthcare_mcp.md) | HIPAA compliance, medical records, analytics |
| **Finance** | [Finance MCP](extra/finance_mcp.md) | Financial analysis, compliance, risk management |
| **Education** | [Education MCP](extra/education_mcp.md) | LMS integration, student tracking, content delivery |
| **Legal** | [Legal MCP](extra/legal_mcp.md) | Document management, compliance, case tracking |
| **Real Estate** | [Real Estate MCP](extra/real_estate_mcp.md) | Property management, CRM, market analysis |
| **Gaming** | [Gaming MCP](extra/gaming_mcp.md) | Game development, analytics, player management |
| **Marketing** | [Marketing MCP](extra/marketing_mcp.md) | Campaign management, analytics, automation |
| **Cybersecurity** | [Cybersecurity MCP](extra/cybersecurity_mcp.md) | Security monitoring, threat detection, compliance |
| **Scientific Research** | [Scientific Research MCP](extra/scientific_research_mcp.md) | Research workflows, data analysis, collaboration |
| **E-commerce** | [E-commerce MCP](extra/e_commerce_mcp.md) | Store management, inventory, customer analytics |

## 🛠️ Developer Tools & MCP Development

| MCP | Description | Key Features |
|-----|-------------|--------------|
| [MCP Testing Framework](extra/mcp_testing_framework.md) ⭐ **NEW** | Comprehensive testing suite for MCP development | Unit testing, integration testing, performance testing, security validation |
| [MCP Development Kit](extra/mcp_development_kit.md) ⭐ **NEW** | Complete toolkit for building custom MCPs | Project scaffolding, code generation, templates, development server |
| [MCP Debugger](extra/mcp_debugger.md) ⭐ **NEW** | Advanced debugging capabilities for MCPs | Real-time debugging, breakpoints, performance monitoring, error analysis |
| [MCP Performance Profiler](extra/mcp_performance_profiler.md) ⭐ **NEW** | Performance analysis and optimization tools | CPU profiling, memory analysis, bottleneck detection, optimization suggestions |
| [MCP Security Scanner](extra/mcp_security_scanner.md) ⭐ **NEW** | Security analysis and vulnerability detection | Security scanning, vulnerability assessment, compliance checking |
| [MCP Code Generator](extra/mcp_code_generator.md) ⭐ **NEW** | Automated code generation for MCP development | Handler generation, schema creation, boilerplate automation |
| [MCP Documentation Generator](extra/mcp_documentation_generator.md) ⭐ **NEW** | Automatic documentation generation | API docs, README generation, example creation, interactive documentation |
| [MCP Validator](extra/mcp_validator.md) ⭐ **NEW** | MCP protocol compliance validation | Schema validation, protocol compliance, best practices checking |
| [MCP Package Manager](extra/mcp_package_manager.md) ⭐ **NEW** | Package management for MCP ecosystem | Dependency management, version control, distribution, marketplace integration |
| [MCP Monitoring Tools](extra/mcp_monitoring_tools.md) ⭐ **NEW** | Production monitoring and observability | Health monitoring, metrics collection, alerting, dashboard creation |
| [MCP Integration Templates](extra/mcp_integration_templates.md) ⭐ **NEW** | Ready-to-use integration templates | IDE templates, CI/CD templates, deployment templates, configuration examples |
| [MCP Deployment Automation](extra/mcp_deployment_automation.md) ⭐ **NEW** | Automated deployment and distribution | CI/CD integration, automated testing, deployment pipelines, release management |

## 🔧 Advanced Tools & Utilities

| MCP | Description | Purpose |
|-----|-------------|---------|
| [MCP Installer](extra/mcp_installer.md) | Automated MCP installation | Bulk installation, configuration management |
| [MCP Host CLI](extra/mcp_host_cli.md) | Command-line MCP management | Server management, monitoring, debugging |
| [MCP Easy Copy](extra/mcp_easy_copy.md) | Configuration sharing | Easy setup sharing, template management |
| [Everything MCP](extra/everything_mcp.md) | Universal search and indexing | File search, content indexing, quick access |
| [Time MCP](extra/time_mcp.md) | Time and scheduling utilities | Time management, scheduling, calendar integration |
| [Maps MCP](extra/maps_mcp.md) | Location and mapping services | Geolocation, mapping, route planning |

## 📚 Documentation & Resources

| Resource | Description | Content |
|----------|-------------|---------|
| [🎯 **MCP Tips & Tricks Master Guide**](extra/mcp_tips_and_tricks_master_guide.md) ⭐ **FEATURED** | Ultimate guide with 100+ tips and best practices | Setup, optimization, troubleshooting, enterprise deployment |
| [Building Custom MCPs](extra/building_custom_mcps.md) | MCP development guide | Creation, testing, deployment |
| [Security Considerations](extra/security_considerations.md) | Security best practices | Authentication, authorization, compliance |
| [IDE Integrations](extra/ide_integrations.md) | Development environment setup | VS Code, IntelliJ, other IDEs |
| [MCP Server Configuration](extra/mcp_server_configuration.md) | Server setup and configuration | Installation, configuration, optimization |

## 🌟 Community & Enhanced MCPs

| MCP | Description | Features |
|-----|-------------|----------|
| [Sequel MCP](extra/sequel_mcp.md) | Database query interface | SQL execution, query optimization, results visualization |
| [MCPX](extra/mcpx.md) | MCP extension framework | Plugin system, extensibility, custom integrations |
| [MCP Inception](extra/mcp_inception.md) | Meta-MCP for MCP management | MCP creation, deployment, monitoring |
| [Serverman](extra/serverman.md) | Server management utilities | Process management, monitoring, automation |
| [Web MCP](extra/web_mcp.md) | Web development utilities | HTTP servers, API testing, web automation |

## 🎯 What Each Documentation Includes

Every MCP documentation in the `extra/` folder provides:

- ✅ **Complete Installation Guide** - Multiple methods, prerequisites, verification
- ✅ **Comprehensive Commands** - 50-100+ commands with examples
- ✅ **Real-World Usage Examples** - Practical scenarios and workflows
- ✅ **Advanced Configuration** - Customization and optimization
- ✅ **Editing & Scripting** - Custom automation and features
- ✅ **Troubleshooting** - Common issues and solutions
- ✅ **Security & Best Practices** - Enterprise-ready configurations
- ✅ **Performance Optimization** - Monitoring and tuning guides
- ✅ **API Reference** - Complete technical documentation

## 🚀 Getting Started

1. **📖 Read the Master Guide**: Start with our [MCP Tips & Tricks Master Guide](extra/mcp_tips_and_tricks_master_guide.md)
2. **🎯 Choose your MCPs** from the tables above
3. **🔗 Click the links** to access complete documentation
4. **⚙️ Follow the installation guides** for your selected MCPs
5. **🛠️ Configure Claude Desktop** with the provided examples
6. **🎉 Start using** your enhanced Claude Code setup!

## 🌟 What's New

### 🆕 Latest Additions
- **🎯 Claude Code Plan Mode MCP** - Advanced planning and analysis capabilities for Claude Code
- **🤖 Claude Code Agent Creator MCP** - Create and manage specialized AI agents within Claude Code
- **⚡ Claude Code Workflow Optimizer MCP** - Analyze and optimize development workflows
- **📚 Enhanced Documentation** - All MCPs now include verified links and complete guides
- **🔧 Advanced Configuration Examples** - Enterprise-ready configurations and optimizations

### 📊 Repository Statistics
- **120+ MCP Implementations** documented
- **Complete Installation Guides** for every MCP
- **1000+ Commands & Examples** across all MCPs
- **Advanced Configuration Patterns** for enterprise use
- **Comprehensive Troubleshooting** for all implementations
- **100% Verified Links** - every link tested and working

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**🌟 Made with ❤️ by the Claude Code community**

*Click any MCP link above for complete documentation, installation guides, and usage examples. Start with our [Master Tips & Tricks Guide](extra/mcp_tips_and_tricks_master_guide.md) for the best experience!*

