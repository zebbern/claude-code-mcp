# Workflow Evaluator-Optimizer MCP

## Overview
The Workflow Evaluator-Optimizer MCP implements the evaluator-optimizer pattern for iterative improvement of AI-generated content and processes. This sophisticated workflow system uses one agent to generate solutions while another evaluates and provides feedback, creating a continuous improvement loop that enhances quality and accuracy over multiple iterations.

## Installation

### Prerequisites
- Claude Desktop application or API access
- Node.js 16+ or Python 3.8+
- Understanding of evaluator-optimizer patterns
- Access to multiple LLM instances for parallel processing
- Sufficient API quota for iterative processing

### Install Steps

#### Option 1: From MCP-Agent Framework
```bash
git clone https://github.com/lastmile-ai/mcp-agent.git
cd mcp-agent
pip install -e .
```

#### Option 2: Standalone Installation
```bash
npm install workflow-evaluator-optimizer-mcp
```

#### Option 3: Python Package
```bash
pip install workflow-evaluator-optimizer
```

#### Option 4: Docker Container
```bash
docker run -d --name evaluator-optimizer \
  -e ANTHROPIC_API_KEY=your-key \
  workflow-evaluator-optimizer-mcp
```

## Configuration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "evaluator-optimizer": {
      "command": "python",
      "args": [
        "-m", "workflow_evaluator_optimizer",
        "--max-iterations", "5",
        "--improvement-threshold", "0.8"
      ]
    }
  }
}
```

### Workflow Configuration
```json
{
  "evaluator_optimizer": {
    "generator": {
      "model": "claude-3-5-sonnet-20241022",
      "temperature": 0.7,
      "max_tokens": 4000,
      "system_prompt": "You are a content generator focused on creating high-quality outputs based on requirements."
    },
    "evaluator": {
      "model": "claude-3-5-sonnet-20241022",
      "temperature": 0.3,
      "max_tokens": 2000,
      "system_prompt": "You are an expert evaluator providing constructive feedback and specific improvement suggestions."
    },
    "optimization": {
      "max_iterations": 5,
      "improvement_threshold": 0.8,
      "convergence_criteria": "quality_score",
      "early_stopping": true
    }
  }
}
```

### Advanced Configuration
```json
{
  "workflow_config": {
    "evaluation_criteria": {
      "accuracy": {"weight": 0.3, "threshold": 0.8},
      "completeness": {"weight": 0.25, "threshold": 0.7},
      "clarity": {"weight": 0.2, "threshold": 0.75},
      "relevance": {"weight": 0.15, "threshold": 0.8},
      "creativity": {"weight": 0.1, "threshold": 0.6}
    },
    "feedback_types": {
      "structural": "Organization and flow improvements",
      "content": "Factual accuracy and completeness",
      "style": "Tone, voice, and readability",
      "technical": "Technical accuracy and implementation details"
    },
    "termination_conditions": {
      "max_iterations": 10,
      "quality_threshold": 0.9,
      "improvement_plateau": 0.05,
      "time_limit": "30m"
    }
  }
}
```

## Usage Examples

### Content Creation Workflow
```
# Blog post optimization
Create a blog post about "AI Agent Coordination Patterns" and optimize it through evaluator-optimizer workflow.

# Technical documentation
Generate technical documentation for the MCP protocol and iteratively improve it based on expert evaluation.

# Marketing copy
Create marketing copy for a new product and optimize it for conversion and engagement.

# Research paper
Draft a research paper on multi-agent systems and refine it through academic peer review simulation.

# Code documentation
Generate comprehensive code documentation and improve it through technical review cycles.
```

### Business Process Optimization
```
# Process improvement
Analyze the customer onboarding process and optimize it through iterative evaluation and refinement.

# Workflow design
Design a new employee training workflow and optimize it based on effectiveness criteria.

# Quality assurance
Create a quality assurance checklist and refine it through expert evaluation and testing.

# Risk assessment
Develop a risk assessment framework and optimize it through scenario testing and expert review.

# Performance metrics
Design performance measurement systems and optimize them through stakeholder feedback.
```

### Creative Content Optimization
```
# Story development
Create a short story and optimize it through literary evaluation and creative feedback.

# Video script
Write a video script and optimize it through production and audience engagement criteria.

# Presentation design
Create a presentation outline and optimize it through audience impact and clarity evaluation.

# User experience design
Design a user interface and optimize it through usability evaluation and user feedback simulation.

# Brand messaging
Develop brand messaging and optimize it through market positioning and audience resonance evaluation.
```

### Technical Solution Optimization
```
# Architecture design
Create a system architecture and optimize it through technical evaluation and scalability assessment.

# Algorithm optimization
Develop an algorithm and optimize it through performance evaluation and efficiency analysis.

# Database design
Create a database schema and optimize it through normalization and performance evaluation.

# API design
Design a RESTful API and optimize it through usability and performance evaluation.

# Security framework
Develop a security framework and optimize it through threat modeling and vulnerability assessment.
```

## Features

### Core Workflow Capabilities
- **Iterative Improvement**: Continuous refinement through evaluation cycles
- **Multi-Criteria Evaluation**: Comprehensive assessment across multiple dimensions
- **Adaptive Feedback**: Context-aware feedback generation and application
- **Quality Convergence**: Automatic detection of quality improvement plateaus
- **Flexible Termination**: Multiple termination criteria for optimal stopping

### Advanced Evaluation Features
- **Weighted Scoring**: Customizable evaluation criteria with adjustable weights
- **Contextual Assessment**: Domain-specific evaluation frameworks
- **Comparative Analysis**: Comparison with benchmarks and best practices
- **Trend Analysis**: Quality improvement trend tracking and prediction
- **Stakeholder Simulation**: Multi-perspective evaluation from different viewpoints

### Optimization Capabilities
- **Targeted Improvements**: Specific, actionable improvement recommendations
- **Incremental Refinement**: Step-by-step enhancement strategies
- **Quality Metrics**: Quantitative quality assessment and tracking
- **Performance Optimization**: Efficiency and effectiveness improvements
- **Creative Enhancement**: Innovation and creativity boosting techniques

### Integration Features
- **Workflow Orchestration**: Integration with broader workflow systems
- **Template Library**: Pre-built evaluation and optimization templates
- **Custom Criteria**: User-defined evaluation criteria and metrics
- **Export Capabilities**: Results export in multiple formats
- **Audit Trail**: Complete history of iterations and improvements

## Requirements

### System Requirements
- **Computational Resources**: Sufficient for parallel agent execution
- **API Access**: Multiple LLM API calls for iterative processing
- **Memory**: 2GB+ for workflow state management
- **Storage**: Persistent storage for iteration history and results
- **Network**: Stable internet connection for API communications

### Workflow Requirements
```javascript
// Minimum workflow specifications
const workflowRequirements = {
  "generator_agent": {
    "model_access": "claude-3-5-sonnet-20241022",
    "context_window": "200k tokens",
    "response_time": "< 30s",
    "quality_baseline": 0.6
  },
  "evaluator_agent": {
    "model_access": "claude-3-5-sonnet-20241022",
    "evaluation_expertise": "domain_specific",
    "feedback_quality": "actionable",
    "consistency": "high"
  },
  "optimization_engine": {
    "iteration_tracking": true,
    "convergence_detection": true,
    "quality_metrics": "quantitative",
    "early_stopping": "configurable"
  }
};
```

### Performance Requirements
- Maximum iteration time: 5 minutes per cycle
- Quality improvement detection: 5% minimum improvement
- Convergence detection: 3 consecutive iterations without improvement
- Memory usage: < 1GB per workflow instance
- Concurrent workflows: Up to 10 parallel instances

## Security Considerations

### Best Practices
- **Data Privacy**: Secure handling of sensitive content during optimization
- **Access Control**: Restricted access to evaluation criteria and feedback
- **Audit Logging**: Complete logging of all optimization activities
- **Content Filtering**: Inappropriate content detection and filtering
- **Resource Limits**: Proper resource limits to prevent abuse

### Secure Configuration
```json
{
  "security": {
    "content_filtering": {
      "enabled": true,
      "filters": ["profanity", "sensitive_data", "harmful_content"],
      "action": "reject_and_log"
    },
    "access_control": {
      "evaluation_criteria_access": "admin_only",
      "workflow_modification": "authorized_users",
      "result_access": "role_based"
    },
    "data_protection": {
      "encryption_at_rest": true,
      "encryption_in_transit": true,
      "data_retention": "30_days",
      "anonymization": "automatic"
    }
  }
}
```

### Privacy Protection
```javascript
// Privacy protection measures
const privacyProtection = {
  "data_minimization": "Only store necessary iteration data",
  "anonymization": "Remove personally identifiable information",
  "retention_limits": "Automatic deletion after 30 days",
  "access_logging": "Log all data access attempts",
  "consent_management": "Explicit consent for data processing"
};
```

## Troubleshooting

### Common Issues

#### Convergence Problems
**Problem**: Workflow not converging to satisfactory quality
**Solution**:
```python
# Adjust convergence parameters
convergence_config = {
    "improvement_threshold": 0.05,  # Lower threshold
    "max_iterations": 10,           # More iterations
    "quality_weights": {            # Rebalance criteria
        "accuracy": 0.4,
        "completeness": 0.3,
        "clarity": 0.3
    }
}
```

#### Evaluation Inconsistency
**Problem**: Evaluator providing inconsistent feedback
**Solution**:
- Refine evaluator system prompts
- Add evaluation criteria examples
- Implement evaluation calibration
- Use multiple evaluators for consensus

#### Performance Issues
**Problem**: Slow iteration cycles
**Solution**:
```python
# Performance optimization
performance_config = {
    "parallel_evaluation": True,
    "caching_enabled": True,
    "batch_processing": True,
    "timeout_limits": {
        "generation": "60s",
        "evaluation": "30s"
    }
}
```

#### Quality Plateau
**Problem**: Quality improvements plateau early
**Solution**:
- Diversify evaluation criteria
- Introduce creative constraints
- Use different evaluator perspectives
- Implement breakthrough techniques

### Diagnostic Tools
```bash
# Workflow analysis
evaluator-optimizer --analyze-workflow --workflow-id <id>

# Quality trend analysis
evaluator-optimizer --quality-trends --time-range 7d

# Performance metrics
evaluator-optimizer --performance-report --detailed

# Convergence analysis
evaluator-optimizer --convergence-analysis --workflow-id <id>
```

## Advanced Configuration

### Custom Evaluation Frameworks
```python
# Custom evaluation framework
class TechnicalDocumentationEvaluator:
    def __init__(self):
        self.criteria = {
            "technical_accuracy": {
                "weight": 0.35,
                "sub_criteria": ["factual_correctness", "technical_depth", "current_standards"]
            },
            "clarity": {
                "weight": 0.25,
                "sub_criteria": ["readability", "structure", "examples"]
            },
            "completeness": {
                "weight": 0.25,
                "sub_criteria": ["coverage", "detail_level", "edge_cases"]
            },
            "usability": {
                "weight": 0.15,
                "sub_criteria": ["actionability", "searchability", "navigation"]
            }
        }
    
    def evaluate(self, content, context):
        scores = {}
        for criterion, config in self.criteria.items():
            score = self._evaluate_criterion(content, criterion, config)
            scores[criterion] = score
        
        overall_score = sum(
            scores[criterion] * config["weight"]
            for criterion, config in self.criteria.items()
        )
        
        return {
            "overall_score": overall_score,
            "detailed_scores": scores,
            "feedback": self._generate_feedback(scores, content)
        }
```

### Multi-Stage Optimization
```python
# Multi-stage optimization workflow
class MultiStageOptimizer:
    def __init__(self):
        self.stages = [
            {
                "name": "structure_optimization",
                "focus": ["organization", "flow", "hierarchy"],
                "iterations": 3
            },
            {
                "name": "content_optimization",
                "focus": ["accuracy", "completeness", "relevance"],
                "iterations": 4
            },
            {
                "name": "style_optimization",
                "focus": ["clarity", "tone", "readability"],
                "iterations": 3
            }
        ]
    
    def optimize(self, initial_content):
        current_content = initial_content
        
        for stage in self.stages:
            stage_optimizer = self._create_stage_optimizer(stage)
            current_content = stage_optimizer.optimize(current_content)
        
        return current_content
```

### Adaptive Learning
```python
# Adaptive learning system
class AdaptiveLearningOptimizer:
    def __init__(self):
        self.learning_history = []
        self.adaptation_threshold = 0.1
    
    def adapt_criteria(self, workflow_results):
        # Analyze successful optimization patterns
        successful_patterns = self._analyze_success_patterns(workflow_results)
        
        # Adjust evaluation criteria weights
        if self._should_adapt(successful_patterns):
            self._update_criteria_weights(successful_patterns)
            self._update_feedback_strategies(successful_patterns)
    
    def _analyze_success_patterns(self, results):
        # Machine learning analysis of successful optimizations
        return self._ml_pattern_analysis(results)
```

## Workflow Examples

### Content Creation Pipeline
```python
# Blog post optimization workflow
blog_post_workflow = {
    "task": "Create a comprehensive blog post about AI ethics",
    "requirements": {
        "length": "2000-2500 words",
        "audience": "technical professionals",
        "tone": "informative and engaging",
        "structure": "introduction, main sections, conclusion"
    },
    "evaluation_criteria": {
        "technical_accuracy": 0.3,
        "engagement": 0.25,
        "clarity": 0.2,
        "completeness": 0.15,
        "seo_optimization": 0.1
    },
    "optimization_stages": [
        "content_generation",
        "structure_refinement",
        "technical_review",
        "engagement_optimization",
        "final_polish"
    ]
}
```

### Code Review Optimization
```python
# Code review workflow
code_review_workflow = {
    "task": "Review and optimize Python code for performance and maintainability",
    "evaluation_criteria": {
        "code_quality": 0.3,
        "performance": 0.25,
        "maintainability": 0.2,
        "security": 0.15,
        "documentation": 0.1
    },
    "optimization_focus": [
        "algorithmic_efficiency",
        "code_structure",
        "error_handling",
        "documentation_quality",
        "test_coverage"
    ],
    "tools": ["static_analysis", "performance_profiling", "security_scanning"]
}
```

### Business Process Design
```python
# Business process optimization
process_optimization_workflow = {
    "task": "Design and optimize customer onboarding process",
    "stakeholder_perspectives": [
        "customer_experience",
        "operational_efficiency",
        "compliance_requirements",
        "cost_effectiveness"
    ],
    "evaluation_criteria": {
        "user_experience": 0.35,
        "efficiency": 0.25,
        "compliance": 0.2,
        "scalability": 0.2
    },
    "optimization_techniques": [
        "process_mapping",
        "bottleneck_analysis",
        "automation_opportunities",
        "quality_checkpoints"
    ]
}
```

## Integration with Other MCPs

### With Planning MCPs
```
# Integrated planning and optimization
1. Use planning MCPs for initial project structure
2. Use evaluator-optimizer for iterative plan refinement
3. Optimize resource allocation and timeline estimates
4. Continuously improve planning accuracy
```

### With Multi-Agent MCPs
```
# Multi-agent optimization workflows
1. Use multi-agent MCPs for diverse perspective generation
2. Use evaluator-optimizer for consensus building
3. Optimize team coordination and communication
4. Improve collective decision-making processes
```

### With Content MCPs
```
# Content optimization pipeline
1. Use content generation MCPs for initial creation
2. Use evaluator-optimizer for quality improvement
3. Optimize content for specific audiences and platforms
4. Maintain content quality standards
```

## Performance Optimization

### Parallel Processing
```python
# Parallel evaluation and optimization
import asyncio

class ParallelOptimizer:
    async def optimize_parallel(self, content, criteria_groups):
        tasks = []
        for group in criteria_groups:
            task = asyncio.create_task(
                self.optimize_for_criteria_group(content, group)
            )
            tasks.append(task)
        
        results = await asyncio.gather(*tasks)
        return self.merge_optimization_results(results)
```

### Caching Strategies
```python
# Intelligent caching for optimization workflows
class OptimizationCache:
    def __init__(self):
        self.content_cache = {}
        self.evaluation_cache = {}
        self.pattern_cache = {}
    
    def get_cached_evaluation(self, content_hash, criteria):
        cache_key = f"{content_hash}:{hash(str(criteria))}"
        return self.evaluation_cache.get(cache_key)
    
    def cache_evaluation(self, content_hash, criteria, evaluation):
        cache_key = f"{content_hash}:{hash(str(criteria))}"
        self.evaluation_cache[cache_key] = evaluation
```

### Resource Management
```python
# Resource-aware optimization
class ResourceAwareOptimizer:
    def __init__(self, resource_limits):
        self.cpu_limit = resource_limits.get("cpu", 80)
        self.memory_limit = resource_limits.get("memory", "2GB")
        self.api_rate_limit = resource_limits.get("api_calls", 100)
    
    def optimize_with_constraints(self, content, criteria):
        if self.should_throttle():
            return self.lightweight_optimization(content, criteria)
        else:
            return self.full_optimization(content, criteria)
```

## Links

- [MCP-Agent Evaluator-Optimizer](https://github.com/lastmile-ai/mcp-agent/tree/main/src/mcp_agent/workflows/evaluator_optimizer)
- [Anthropic Agent Building Guide](https://www.anthropic.com/research/building-effective-agents)
- [Evaluator-Optimizer Pattern Documentation](https://github.com/lastmile-ai/mcp-agent/blob/main/examples/workflow_evaluator_optimizer/README.md)
- [Workflow Optimization Best Practices](https://docs.lastmileai.dev/workflows/optimization)
- [Quality Assessment Frameworks](https://github.com/lastmile-ai/mcp-agent/wiki/quality-frameworks)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Evaluator-Optimizer Community](https://github.com/lastmile-ai/mcp-agent/discussions/categories/evaluator-optimizer)
- [Workflow Pattern Library](https://github.com/lastmile-ai/mcp-agent/wiki/workflow-patterns)
- [Optimization Examples](https://github.com/lastmile-ai/mcp-agent/tree/main/examples)
- [Quality Metrics Research](https://github.com/lastmile-ai/mcp-agent/wiki/quality-research)
- [MCP Discord](https://discord.gg/mcp)
- [Best Practices Guide](https://docs.lastmileai.dev/best-practices/evaluator-optimizer)

