
# AWS Knowledge Base MCP

The AWS Knowledge Base MCP enables Claude Code to retrieve information from AWS Knowledge Bases using Bedrock Agent Runtime. This is highly valuable for organizations that store vast amounts of proprietary data, documentation, or internal knowledge within AWS, allowing Claude to access and synthesize this information for various tasks.

## Capabilities

*   **Information Retrieval**: Query and retrieve relevant information from configured AWS Knowledge Bases.
*   **Contextual Understanding**: Leverage internal company data for more accurate and context-aware responses.
*   **Secure Access**: Integrates with AWS security mechanisms to ensure controlled access to sensitive information.

## Configuration

To add the AWS Knowledge Base MCP, you typically use `npx` to run the official server. You will need appropriate AWS credentials configured (e.g., via environment variables or AWS CLI configuration) that have permissions to access Bedrock Agent Runtime and your specific Knowledge Bases.

```bash
claude mcp add aws-kb-server --command npx --args -y @modelcontextprotocol/server-aws-knowledge-base --env AWS_REGION=<YOUR_AWS_REGION> --env AWS_ACCESS_KEY_ID=<YOUR_ACCESS_KEY> --env AWS_SECRET_ACCESS_KEY=<YOUR_SECRET_KEY>
```

*   Replace placeholders with your AWS region and credentials. It is highly recommended to use IAM roles or temporary credentials for production environments.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "aws-knowledge-base": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-aws-knowledge-base"
      ],
      "env": {
        "AWS_REGION": "us-east-1",
        "AWS_ACCESS_KEY_ID": "<YOUR_ACCESS_KEY>",
        "AWS_SECRET_ACCESS_KEY": "<YOUR_SECRET_KEY>"
      }
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the AWS Knowledge Base MCP to retrieve internal information.

### 1. Answering Questions from Internal Documentation

Ask Claude a question that can be answered by your internal knowledge base:

```
According to our internal documentation, what is the process for requesting a new software license?
```

Claude will query the AWS Knowledge Base and provide the relevant information.

### 2. Summarizing Project Specifications

Instruct Claude to summarize a project specification document stored in your knowledge base:

```
Summarize the key requirements for Project Alpha from the document in our AWS Knowledge Base.
```

Claude will retrieve the document and provide a concise summary.

### 3. Troubleshooting Internal Systems

Ask Claude to help troubleshoot an issue based on past incidents or troubleshooting guides:

```
What are the common causes for 'database connection refused' errors in our production environment, based on our AWS Knowledge Base?
```

Claude can provide insights from your stored operational knowledge.

## Best Practices

*   **AWS Security**: Follow AWS best practices for credential management, using IAM roles with least privilege access.
*   **Knowledge Base Quality**: The effectiveness of this MCP heavily depends on the quality, relevance, and organization of the data within your AWS Knowledge Bases.
*   **Query Specificity**: Guide Claude with precise questions to ensure it retrieves the most accurate and relevant information.

For more details, refer to the [official AWS Knowledge Base MCP documentation](https://modelcontextprotocol.io/examples/aws-knowledge-base).

