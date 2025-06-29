# MCP-Agent Framework

## Overview
The MCP-Agent framework by LastMile AI is a simple, composable framework for building effective AI agents using the Model Context Protocol (MCP). It provides workflow patterns, agent orchestration capabilities, and seamless integration with Claude and other LLMs to create sophisticated agentic AI systems.

## Installation

### Prerequisites
- Python 3.8+ or Node.js 16+
- Claude Desktop application or API access
- Model Context Protocol understanding
- Basic knowledge of agent workflows

### Install Steps

#### Option 1: Python Installation
```bash
pip install mcp-agent
```

#### Option 2: From GitHub
```bash
git clone https://github.com/lastmile-ai/mcp-agent.git
cd mcp-agent
pip install -e .
```

#### Option 3: Docker Container
```bash
docker run -d --name mcp-agent \
  -v $(pwd):/workspace \
  lastmile/mcp-agent
```

#### Option 4: Development Setup
```bash
git clone https://github.com/lastmile-ai/mcp-agent.git
cd mcp-agent
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -e ".[dev]"
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "mcp-agent": {
      "command": "python",
      "args": [
        "-m", "mcp_agent.server",
        "--config", "/path/to/agent-config.json"
      ]
    }
  }
}
```

### Agent Configuration File
```json
{
  "agents": {
    "research_agent": {
      "type": "research",
      "model": "claude-3-5-sonnet-20241022",
      "tools": ["web_search", "document_analysis"],
      "memory": {
        "type": "file",
        "path": "./memory/research_agent"
      }
    },
    "writing_agent": {
      "type": "content_creator",
      "model": "claude-3-5-sonnet-20241022",
      "tools": ["text_generation", "style_analysis"],
      "memory": {
        "type": "file",
        "path": "./memory/writing_agent"
      }
    }
  },
  "workflows": {
    "content_pipeline": {
      "type": "sequential",
      "agents": ["research_agent", "writing_agent"],
      "coordination": "handoff"
    }
  }
}
```

### Environment Variables
```bash
export ANTHROPIC_API_KEY=your-api-key
export MCP_AGENT_CONFIG=/path/to/config.json
export MCP_AGENT_MEMORY_PATH=/path/to/memory
export MCP_AGENT_LOG_LEVEL=INFO
```

## Usage Examples

### Basic Agent Creation
```python
from mcp_agent import Agent, Workflow

# Create a research agent
research_agent = Agent(
    name="research_agent",
    model="claude-3-5-sonnet-20241022",
    tools=["web_search", "document_analysis"],
    system_prompt="You are a research specialist focused on gathering and analyzing information."
)

# Create a writing agent
writing_agent = Agent(
    name="writing_agent",
    model="claude-3-5-sonnet-20241022",
    tools=["text_generation", "style_analysis"],
    system_prompt="You are a content creator focused on producing high-quality written content."
)

# Create a workflow
workflow = Workflow(
    name="content_creation",
    agents=[research_agent, writing_agent],
    pattern="sequential"
)
```

### Evaluator-Optimizer Workflow
```python
from mcp_agent.workflows import EvaluatorOptimizer

# Create evaluator-optimizer workflow
evaluator_optimizer = EvaluatorOptimizer(
    generator_agent=Agent(
        name="content_generator",
        model="claude-3-5-sonnet-20241022",
        system_prompt="Generate high-quality content based on requirements."
    ),
    evaluator_agent=Agent(
        name="content_evaluator",
        model="claude-3-5-sonnet-20241022",
        system_prompt="Evaluate content quality and provide specific improvement suggestions."
    ),
    max_iterations=3,
    improvement_threshold=0.8
)

# Run the workflow
result = evaluator_optimizer.run(
    task="Write a comprehensive blog post about AI agents",
    requirements={
        "length": "1500-2000 words",
        "tone": "professional",
        "audience": "technical professionals"
    }
)
```

### Multi-Agent Coordination
```python
from mcp_agent.coordination import AgentCoordinator

# Create coordinator
coordinator = AgentCoordinator(
    agents=[research_agent, writing_agent, review_agent],
    coordination_strategy="consensus",
    communication_protocol="shared_memory"
)

# Execute coordinated task
result = coordinator.execute_task(
    task="Create a technical whitepaper on MCP",
    coordination_rules={
        "research_phase": ["research_agent"],
        "writing_phase": ["writing_agent"],
        "review_phase": ["review_agent"],
        "consensus_required": True
    }
)
```

### Agent Memory Management
```python
from mcp_agent.memory import FileMemory, VectorMemory

# File-based memory
file_memory = FileMemory(
    path="./agent_memory",
    format="json",
    compression=True
)

# Vector-based memory for semantic search
vector_memory = VectorMemory(
    embedding_model="text-embedding-ada-002",
    vector_store="chroma",
    collection_name="agent_knowledge"
)

# Agent with memory
agent_with_memory = Agent(
    name="knowledge_agent",
    model="claude-3-5-sonnet-20241022",
    memory=vector_memory,
    memory_config={
        "max_context_length": 8000,
        "relevance_threshold": 0.7,
        "memory_decay": 0.95
    }
)
```

## Features

### Core Agent Capabilities
- **Agent Creation**: Simple agent instantiation with customizable models and tools
- **Workflow Patterns**: Pre-built patterns for common agent interactions
- **Memory Management**: Persistent and semantic memory systems
- **Tool Integration**: Seamless integration with external tools and APIs
- **Model Flexibility**: Support for multiple LLM providers and models

### Advanced Workflow Patterns
- **Sequential Workflows**: Agents work in sequence, passing results forward
- **Parallel Workflows**: Multiple agents work simultaneously on different aspects
- **Evaluator-Optimizer**: Iterative improvement through evaluation and optimization
- **Consensus Workflows**: Multiple agents collaborate to reach consensus
- **Hierarchical Workflows**: Supervisor agents coordinate worker agents

### Agent Coordination Features
- **Shared Memory**: Agents share context and knowledge
- **Message Passing**: Direct communication between agents
- **Event-Driven**: Agents respond to events and triggers
- **Resource Management**: Efficient allocation of computational resources
- **Conflict Resolution**: Mechanisms for handling agent disagreements

### Integration Capabilities
- **MCP Protocol**: Native Model Context Protocol support
- **Claude Integration**: Optimized for Claude models and capabilities
- **Tool Ecosystem**: Integration with existing MCP tools and servers
- **API Connectivity**: Connect to external APIs and services
- **Database Integration**: Persistent storage and retrieval systems

## Requirements

### System Requirements
- **Python**: Version 3.8 or higher
- **Memory**: 2GB+ available RAM (scales with agent count)
- **Storage**: Varies by memory configuration and data volume
- **Network**: Internet access for LLM API calls
- **Operating System**: Linux, macOS, or Windows

### Model Requirements
- Access to Claude API or other supported LLM providers
- Appropriate API keys and authentication
- Sufficient API quota for agent operations
- Model compatibility with agent workflows

### Dependencies
```python
# Core dependencies
anthropic>=0.25.0
pydantic>=2.0.0
asyncio>=3.4.3
aiohttp>=3.8.0
numpy>=1.21.0

# Optional dependencies
chromadb>=0.4.0  # For vector memory
openai>=1.0.0    # For OpenAI models
langchain>=0.1.0 # For additional tools
```

## Security Considerations

### Best Practices
- **API Security**: Secure storage and rotation of API keys
- **Agent Isolation**: Proper isolation between agent instances
- **Memory Security**: Secure handling of sensitive information in memory
- **Tool Permissions**: Minimal permissions for agent tools
- **Audit Logging**: Comprehensive logging of agent activities

### Secure Configuration
```python
from mcp_agent.security import SecureAgent, PermissionManager

# Create secure agent with limited permissions
secure_agent = SecureAgent(
    name="restricted_agent",
    model="claude-3-5-sonnet-20241022",
    permissions=PermissionManager(
        allowed_tools=["web_search", "text_analysis"],
        denied_actions=["file_write", "system_command"],
        rate_limits={"api_calls": 100, "memory_writes": 50}
    ),
    security_config={
        "encrypt_memory": True,
        "audit_all_actions": True,
        "sandbox_execution": True
    }
)
```

### Data Protection
```python
# Memory encryption configuration
memory_config = {
    "encryption": {
        "enabled": True,
        "algorithm": "AES-256-GCM",
        "key_rotation": "weekly"
    },
    "access_control": {
        "agent_isolation": True,
        "read_permissions": ["owner", "collaborators"],
        "write_permissions": ["owner"]
    }
}
```

## Troubleshooting

### Common Issues

#### Agent Initialization Errors
**Problem**: Agent fails to initialize properly
**Solution**:
```python
# Check configuration
try:
    agent = Agent(name="test_agent", model="claude-3-5-sonnet-20241022")
    print("Agent initialized successfully")
except Exception as e:
    print(f"Initialization error: {e}")
    # Check API keys, model availability, and configuration
```

#### Memory Issues
**Problem**: Agent memory not persisting or loading
**Solution**:
```python
# Verify memory configuration
from mcp_agent.memory import MemoryDiagnostics

diagnostics = MemoryDiagnostics()
memory_status = diagnostics.check_memory_system(agent)
print(f"Memory status: {memory_status}")

# Fix common memory issues
if not memory_status["writable"]:
    # Fix file permissions
    import os
    os.chmod(memory_path, 0o755)
```

#### Workflow Coordination Problems
**Problem**: Agents not coordinating properly
**Solution**:
```python
# Debug coordination
from mcp_agent.debug import WorkflowDebugger

debugger = WorkflowDebugger()
coordination_log = debugger.trace_workflow(workflow)
print(f"Coordination issues: {coordination_log}")

# Check agent communication
for agent in workflow.agents:
    status = debugger.check_agent_status(agent)
    print(f"Agent {agent.name}: {status}")
```

#### Performance Issues
**Problem**: Slow agent response times
**Solution**:
```python
# Performance optimization
from mcp_agent.optimization import PerformanceOptimizer

optimizer = PerformanceOptimizer()
optimized_config = optimizer.optimize_agent_config(agent)
agent.update_config(optimized_config)

# Monitor performance
metrics = optimizer.get_performance_metrics(agent)
print(f"Performance metrics: {metrics}")
```

## Advanced Configuration

### Custom Workflow Patterns
```python
from mcp_agent.workflows import BaseWorkflow

class CustomResearchWorkflow(BaseWorkflow):
    def __init__(self, research_agents, synthesis_agent):
        self.research_agents = research_agents
        self.synthesis_agent = synthesis_agent
        
    async def execute(self, task):
        # Parallel research phase
        research_tasks = []
        for agent in self.research_agents:
            research_tasks.append(agent.execute(task))
        
        research_results = await asyncio.gather(*research_tasks)
        
        # Synthesis phase
        synthesis_input = {
            "task": task,
            "research_results": research_results
        }
        
        final_result = await self.synthesis_agent.execute(synthesis_input)
        return final_result
```

### Agent Specialization
```python
# Specialized agent configurations
agents_config = {
    "data_analyst": {
        "model": "claude-3-5-sonnet-20241022",
        "tools": ["data_analysis", "visualization", "statistics"],
        "system_prompt": "You are a data analyst specialized in extracting insights from complex datasets.",
        "memory_config": {
            "type": "vector",
            "embedding_model": "text-embedding-ada-002",
            "max_context": 16000
        }
    },
    "code_reviewer": {
        "model": "claude-3-5-sonnet-20241022",
        "tools": ["code_analysis", "security_scan", "performance_check"],
        "system_prompt": "You are a senior code reviewer focused on code quality, security, and performance.",
        "memory_config": {
            "type": "file",
            "format": "structured",
            "retention_policy": "30_days"
        }
    },
    "project_manager": {
        "model": "claude-3-5-sonnet-20241022",
        "tools": ["task_management", "timeline_planning", "resource_allocation"],
        "system_prompt": "You are a project manager focused on coordination and delivery.",
        "memory_config": {
            "type": "hybrid",
            "file_memory": True,
            "vector_memory": True
        }
    }
}
```

### Workflow Orchestration
```python
from mcp_agent.orchestration import WorkflowOrchestrator

# Complex workflow orchestration
orchestrator = WorkflowOrchestrator()

# Define workflow graph
workflow_graph = {
    "nodes": [
        {"id": "research", "agent": "research_agent", "type": "parallel"},
        {"id": "analysis", "agent": "analysis_agent", "type": "sequential"},
        {"id": "synthesis", "agent": "synthesis_agent", "type": "sequential"},
        {"id": "review", "agent": "review_agent", "type": "evaluator"}
    ],
    "edges": [
        {"from": "research", "to": "analysis"},
        {"from": "analysis", "to": "synthesis"},
        {"from": "synthesis", "to": "review"},
        {"from": "review", "to": "synthesis", "condition": "needs_improvement"}
    ]
}

# Execute workflow
result = orchestrator.execute_workflow(workflow_graph, initial_task)
```

## Workflow Examples

### Content Creation Pipeline
```python
# Multi-agent content creation
content_pipeline = Workflow(
    name="content_creation_pipeline",
    agents=[
        Agent(name="researcher", tools=["web_search", "document_analysis"]),
        Agent(name="writer", tools=["text_generation", "style_analysis"]),
        Agent(name="editor", tools=["grammar_check", "fact_verification"]),
        Agent(name="seo_optimizer", tools=["keyword_analysis", "seo_optimization"])
    ],
    pattern="sequential_with_feedback"
)

# Execute pipeline
content_result = content_pipeline.execute({
    "topic": "AI Agent Frameworks",
    "target_audience": "technical professionals",
    "content_type": "blog_post",
    "length": "2000_words"
})
```

### Software Development Team
```python
# Simulated development team
dev_team = AgentCoordinator(
    agents=[
        Agent(name="product_manager", tools=["requirement_analysis", "user_story_creation"]),
        Agent(name="architect", tools=["system_design", "technology_selection"]),
        Agent(name="developer", tools=["code_generation", "testing", "debugging"]),
        Agent(name="qa_engineer", tools=["test_planning", "bug_detection", "quality_assurance"]),
        Agent(name="devops", tools=["deployment", "monitoring", "infrastructure"])
    ],
    coordination_strategy="agile_methodology"
)

# Execute development cycle
development_result = dev_team.execute_sprint({
    "sprint_goal": "Implement user authentication system",
    "user_stories": ["As a user, I want to login securely"],
    "acceptance_criteria": ["Multi-factor authentication", "Session management"],
    "timeline": "2_weeks"
})
```

### Research and Analysis Team
```python
# Research team workflow
research_team = EvaluatorOptimizer(
    generator_agents=[
        Agent(name="literature_reviewer", tools=["academic_search", "citation_analysis"]),
        Agent(name="data_collector", tools=["survey_design", "data_gathering"]),
        Agent(name="analyst", tools=["statistical_analysis", "pattern_recognition"])
    ],
    evaluator_agent=Agent(name="research_supervisor", tools=["methodology_review", "quality_assessment"]),
    optimization_criteria=["methodological_rigor", "data_quality", "insight_depth"]
)

# Execute research project
research_result = research_team.execute({
    "research_question": "What are the most effective AI agent coordination patterns?",
    "methodology": "mixed_methods",
    "timeline": "3_months"
})
```

## Integration with Other MCPs

### With Database MCPs
```python
# Agent with database integration
database_agent = Agent(
    name="data_agent",
    model="claude-3-5-sonnet-20241022",
    tools=["mysql_query", "mongodb_operations", "data_visualization"],
    mcp_servers=["mysql_mcp", "mongodb_mcp"]
)

# Workflow with database operations
data_workflow = Workflow(
    name="data_analysis_pipeline",
    agents=[database_agent, analysis_agent],
    coordination="data_driven"
)
```

### With Workflow Automation MCPs
```python
# Integration with n8n and Zapier
automation_agent = Agent(
    name="automation_specialist",
    model="claude-3-5-sonnet-20241022",
    tools=["n8n_workflow", "zapier_automation", "process_optimization"],
    mcp_servers=["n8n_mcp", "zapier_mcp"]
)

# Automated workflow creation
automation_result = automation_agent.execute({
    "task": "Create automated lead processing workflow",
    "triggers": ["form_submission", "email_inquiry"],
    "actions": ["crm_update", "email_response", "task_creation"]
})
```

### With Productivity MCPs
```python
# Integration with productivity tools
productivity_agent = Agent(
    name="productivity_assistant",
    model="claude-3-5-sonnet-20241022",
    tools=["notion_management", "calendar_scheduling", "task_prioritization"],
    mcp_servers=["notion_mcp", "calendar_mcp"]
)

# Productivity optimization workflow
productivity_workflow = Workflow(
    name="productivity_optimization",
    agents=[productivity_agent, analysis_agent],
    pattern="continuous_improvement"
)
```

## Performance Optimization

### Agent Performance Tuning
```python
from mcp_agent.optimization import AgentOptimizer

# Performance optimization
optimizer = AgentOptimizer()

# Optimize agent configuration
optimized_agent = optimizer.optimize_agent(
    agent=base_agent,
    optimization_targets=["response_time", "accuracy", "resource_usage"],
    constraints={"max_memory": "2GB", "max_api_calls": 1000}
)

# Monitor performance
performance_metrics = optimizer.monitor_agent_performance(optimized_agent)
```

### Memory Optimization
```python
# Memory optimization strategies
memory_optimizer = MemoryOptimizer()

# Optimize memory usage
optimized_memory = memory_optimizer.optimize_memory_config(
    agent=agent,
    optimization_strategy="balanced",
    constraints={"max_memory_size": "1GB", "retrieval_speed": "fast"}
)

# Implement memory compression
compressed_memory = memory_optimizer.compress_memory(
    memory=agent.memory,
    compression_ratio=0.7,
    preserve_recent=True
)
```

### Workflow Optimization
```python
# Workflow performance optimization
workflow_optimizer = WorkflowOptimizer()

# Analyze workflow bottlenecks
bottlenecks = workflow_optimizer.analyze_bottlenecks(workflow)

# Optimize workflow execution
optimized_workflow = workflow_optimizer.optimize_workflow(
    workflow=workflow,
    optimization_targets=["execution_time", "resource_efficiency"],
    parallelization_strategy="aggressive"
)
```

## Links

- [MCP-Agent Repository](https://github.com/lastmile-ai/mcp-agent)
- [LastMile AI Documentation](https://docs.lastmileai.dev/)
- [Model Context Protocol Specification](https://spec.modelcontextprotocol.io/)
- [Anthropic Agent Building Guide](https://www.anthropic.com/research/building-effective-agents)
- [Agent Workflow Patterns](https://github.com/lastmile-ai/mcp-agent/tree/main/examples)
- [MCP Community Discord](https://discord.gg/mcp)

## Community Resources

- [LastMile AI Community](https://community.lastmileai.dev/)
- [MCP-Agent Examples](https://github.com/lastmile-ai/mcp-agent/tree/main/examples)
- [Agent Building Best Practices](https://docs.lastmileai.dev/best-practices)
- [Workflow Pattern Library](https://github.com/lastmile-ai/mcp-agent/wiki/patterns)
- [Agent Performance Benchmarks](https://benchmarks.lastmileai.dev/)
- [Community Contributions](https://github.com/lastmile-ai/mcp-agent/discussions)

