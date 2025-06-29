# Notion MCP

## Overview
The Notion MCP provides Claude with comprehensive Notion workspace integration, enabling page management, database operations, content creation, and knowledge base interactions. This MCP is essential for productivity workflows, project management, and building AI-powered second brains with Notion.

## Installation

### Prerequisites
- Notion workspace with API access
- Notion integration token
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Appropriate Notion permissions

### Install Steps

#### Option 1: Official Notion MCP
```bash
npx @makenotion/notion-mcp-server
```

#### Option 2: Via Smithery
```bash
npx -y @smithery/cli install @makenotion/notion-mcp-server --client claude
```

#### Option 3: Community Implementation
```bash
git clone https://github.com/danhilse/notion_mcp.git
cd notion_mcp
npm install
npm run build
```

#### Option 4: Python Implementation
```bash
pip install notion-mcp-server
```

## Configuration

### Notion API Setup
1. Go to [Notion Developers](https://developers.notion.com/)
2. Create a new integration
3. Copy the integration token
4. Share your Notion pages/databases with the integration

### Claude Desktop Configuration
```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": [
        "@makenotion/notion-mcp-server",
        "--token", "your-notion-integration-token"
      ]
    }
  }
}
```

### With Environment Variables
```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["@makenotion/notion-mcp-server"],
      "env": {
        "NOTION_TOKEN": "your-notion-integration-token",
        "NOTION_DATABASE_ID": "your-default-database-id"
      }
    }
  }
}
```

### Multiple Workspaces
```json
{
  "mcpServers": {
    "notion-personal": {
      "command": "npx",
      "args": ["@makenotion/notion-mcp-server"],
      "env": {
        "NOTION_TOKEN": "${NOTION_PERSONAL_TOKEN}"
      }
    },
    "notion-work": {
      "command": "npx",
      "args": ["@makenotion/notion-mcp-server"],
      "env": {
        "NOTION_TOKEN": "${NOTION_WORK_TOKEN}"
      }
    }
  }
}
```

## Usage Examples

### Page Management
```
# Create pages
Create a new page titled "Project Planning" in my workspace.

# Read pages
Show me the content of the page titled "Meeting Notes - 2024-01-15".

# Update pages
Add a new section about "Risk Assessment" to the project planning page.

# Delete pages
Remove the outdated page "Old Project Ideas" from my workspace.

# Search pages
Find all pages that mention "machine learning" in the content.
```

### Database Operations
```
# Query databases
Show me all tasks in my todo database that are marked as "In Progress".

# Add database entries
Add a new task "Review MCP documentation" with priority "High" to my todo list.

# Update database entries
Mark the task with ID "abc123" as completed and add completion notes.

# Filter databases
Show me all projects from the last quarter with status "Completed".

# Sort and organize
Sort my reading list database by priority and show the top 10 items.
```

### Content Creation
```
# Generate content
Create a comprehensive project proposal page for a new AI initiative.

# Template creation
Create a meeting notes template with sections for agenda, discussion, and action items.

# Documentation
Generate API documentation for our new service and organize it in Notion.

# Knowledge base
Create a knowledge base entry about MCP best practices.

# Content analysis
Analyze my weekly review pages and summarize key insights.
```

### Productivity Workflows
```
# Task management
Review my todo list and suggest priorities for today.

# Project tracking
Update project status across all active projects in my database.

# Meeting preparation
Create an agenda for tomorrow's team meeting based on recent project updates.

# Weekly reviews
Generate a weekly summary based on completed tasks and project progress.

# Goal tracking
Update my quarterly goals database with current progress.
```

## Features

### Core Notion Operations
- **Page Management**: Create, read, update, and delete Notion pages
- **Database Operations**: Query, filter, and manipulate Notion databases
- **Content Creation**: Generate rich content with formatting and blocks
- **Search Functionality**: Full-text search across pages and databases
- **Block Management**: Handle various Notion block types and structures

### Advanced Features
- **Template System**: Create and use page and database templates
- **Automation**: Automate repetitive tasks and workflows
- **Integration**: Connect with other tools and services
- **Collaboration**: Manage shared pages and collaborative workflows
- **Analytics**: Track productivity metrics and insights

### Content Types
- **Rich Text**: Formatted text with styling and links
- **Databases**: Structured data with properties and views
- **Media**: Images, files, and embedded content
- **Code Blocks**: Syntax-highlighted code snippets
- **Formulas**: Calculated fields and dynamic content

### Productivity Features
- **Task Management**: Todo lists and project tracking
- **Knowledge Management**: Documentation and note-taking
- **Project Planning**: Roadmaps and milestone tracking
- **Meeting Management**: Agendas, notes, and action items
- **Goal Tracking**: OKRs and progress monitoring

## Requirements

### System Requirements
- **Operating System**: Linux, macOS, or Windows
- **Node.js**: Version 16 or higher
- **Memory**: 512MB+ available RAM
- **Network**: Internet access for Notion API
- **Storage**: Minimal local storage for caching

### Notion Requirements
- Active Notion workspace
- Integration created in Notion Developers portal
- Pages/databases shared with the integration
- Appropriate permissions for read/write operations

### API Limits
```javascript
// Notion API rate limits
const rateLimits = {
  requestsPerSecond: 3,
  requestsPerMinute: 100,
  maxPageSize: 100,
  maxBlockChildren: 100
};
```

## Security Considerations

### Best Practices
- **Token Security**: Store integration tokens securely
- **Minimal Permissions**: Grant only necessary permissions
- **Access Control**: Limit integration access to required pages
- **Regular Audits**: Review integration permissions regularly
- **Secure Storage**: Use environment variables for sensitive data

### Secure Configuration
```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["@makenotion/notion-mcp-server"],
      "env": {
        "NOTION_TOKEN": "${NOTION_TOKEN}",
        "NOTION_READ_ONLY": "true"
      }
    }
  }
}
```

### Permission Management
```javascript
// Integration capabilities
const integrationCapabilities = {
  "read_content": true,
  "update_content": true,
  "insert_content": true,
  "read_user": false,
  "read_comments": false
};
```

## Troubleshooting

### Common Issues

#### Authentication Failed
**Problem**: Invalid or expired integration token
**Solution**:
- Verify token in Notion Developers portal
- Check token permissions and scope
- Regenerate token if necessary
- Ensure integration is shared with target pages

#### Permission Denied
**Problem**: Integration lacks access to pages/databases
**Solution**:
- Share pages with the integration
- Check integration permissions
- Verify workspace access
- Review page-level sharing settings

#### API Rate Limits
**Problem**: Too many requests to Notion API
**Solution**:
- Implement request throttling
- Use batch operations when possible
- Cache frequently accessed data
- Optimize query patterns

#### Content Formatting Issues
**Problem**: Rich text or blocks not displaying correctly
**Solution**:
- Check block type compatibility
- Verify rich text formatting
- Review API response structure
- Update content parsing logic

### Diagnostic Commands
```bash
# Test Notion API connectivity
curl -H "Authorization: Bearer $NOTION_TOKEN" \
  -H "Notion-Version: 2022-06-28" \
  https://api.notion.com/v1/users/me

# List accessible databases
curl -H "Authorization: Bearer $NOTION_TOKEN" \
  -H "Notion-Version: 2022-06-28" \
  https://api.notion.com/v1/search

# Check integration permissions
curl -H "Authorization: Bearer $NOTION_TOKEN" \
  -H "Notion-Version: 2022-06-28" \
  https://api.notion.com/v1/users
```

## Advanced Configuration

### Database Schema
```javascript
// Task database schema
const taskDatabaseSchema = {
  "Title": {
    "type": "title"
  },
  "Status": {
    "type": "select",
    "select": {
      "options": [
        {"name": "Not Started", "color": "gray"},
        {"name": "In Progress", "color": "yellow"},
        {"name": "Completed", "color": "green"},
        {"name": "Blocked", "color": "red"}
      ]
    }
  },
  "Priority": {
    "type": "select",
    "select": {
      "options": [
        {"name": "Low", "color": "gray"},
        {"name": "Medium", "color": "yellow"},
        {"name": "High", "color": "red"}
      ]
    }
  },
  "Due Date": {
    "type": "date"
  },
  "Assignee": {
    "type": "people"
  },
  "Tags": {
    "type": "multi_select",
    "multi_select": {
      "options": [
        {"name": "Development", "color": "blue"},
        {"name": "Design", "color": "purple"},
        {"name": "Research", "color": "green"}
      ]
    }
  }
};
```

### Page Templates
```javascript
// Meeting notes template
const meetingNotesTemplate = {
  "parent": {"page_id": "parent-page-id"},
  "properties": {
    "title": {
      "title": [
        {
          "text": {
            "content": "Meeting Notes - {{date}}"
          }
        }
      ]
    }
  },
  "children": [
    {
      "object": "block",
      "type": "heading_2",
      "heading_2": {
        "rich_text": [{"type": "text", "text": {"content": "Agenda"}}]
      }
    },
    {
      "object": "block",
      "type": "bulleted_list_item",
      "bulleted_list_item": {
        "rich_text": [{"type": "text", "text": {"content": "Topic 1"}}]
      }
    },
    {
      "object": "block",
      "type": "heading_2",
      "heading_2": {
        "rich_text": [{"type": "text", "text": {"content": "Discussion"}}]
      }
    },
    {
      "object": "block",
      "type": "heading_2",
      "heading_2": {
        "rich_text": [{"type": "text", "text": {"content": "Action Items"}}]
      }
    }
  ]
};
```

### Automation Workflows
```javascript
// Daily standup automation
const dailyStandupWorkflow = {
  trigger: "daily_schedule",
  time: "09:00",
  actions: [
    {
      type: "query_database",
      database_id: "tasks_database_id",
      filter: {
        and: [
          {
            property: "Assignee",
            people: {
              contains: "current_user_id"
            }
          },
          {
            property: "Status",
            select: {
              equals: "In Progress"
            }
          }
        ]
      }
    },
    {
      type: "create_page",
      template: "standup_template",
      data: "query_results"
    }
  ]
};
```

## API Examples

### Basic Operations
```javascript
// Create a new page
const newPage = await notion.pages.create({
  parent: {
    database_id: "database-id"
  },
  properties: {
    "Name": {
      title: [
        {
          text: {
            content: "New Task"
          }
        }
      ]
    },
    "Status": {
      select: {
        name: "Not Started"
      }
    }
  }
});

// Query database
const response = await notion.databases.query({
  database_id: "database-id",
  filter: {
    property: "Status",
    select: {
      equals: "In Progress"
    }
  },
  sorts: [
    {
      property: "Created",
      direction: "descending"
    }
  ]
});

// Update page properties
await notion.pages.update({
  page_id: "page-id",
  properties: {
    "Status": {
      select: {
        name: "Completed"
      }
    }
  }
});
```

### Advanced Queries
```javascript
// Complex database query
const complexQuery = await notion.databases.query({
  database_id: "projects-database-id",
  filter: {
    and: [
      {
        property: "Status",
        select: {
          equals: "Active"
        }
      },
      {
        property: "Priority",
        select: {
          equals: "High"
        }
      },
      {
        property: "Due Date",
        date: {
          on_or_before: "2024-12-31"
        }
      }
    ]
  },
  sorts: [
    {
      property: "Due Date",
      direction: "ascending"
    },
    {
      property: "Priority",
      direction: "descending"
    }
  ]
});

// Search across workspace
const searchResults = await notion.search({
  query: "machine learning",
  filter: {
    value: "page",
    property: "object"
  },
  sort: {
    direction: "descending",
    timestamp: "last_edited_time"
  }
});
```

### Block Operations
```javascript
// Add content blocks to page
await notion.blocks.children.append({
  block_id: "page-id",
  children: [
    {
      object: "block",
      type: "paragraph",
      paragraph: {
        rich_text: [
          {
            type: "text",
            text: {
              content: "This is a paragraph with "
            }
          },
          {
            type: "text",
            text: {
              content: "bold text",
              link: null
            },
            annotations: {
              bold: true
            }
          }
        ]
      }
    },
    {
      object: "block",
      type: "code",
      code: {
        caption: [],
        rich_text: [
          {
            type: "text",
            text: {
              content: "console.log('Hello, World!');"
            }
          }
        ],
        language: "javascript"
      }
    }
  ]
});
```

## Integration with Other MCPs

### With Git MCP
```
# Documentation workflow
1. Use git MCP to track code changes
2. Use notion MCP to update project documentation
3. Sync commit messages with project notes
4. Maintain development logs in Notion
```

### With Calendar MCP
```
# Meeting management
1. Use calendar MCP to schedule meetings
2. Use notion MCP to create meeting agendas
3. Automatically generate meeting notes
4. Track action items and follow-ups
```

### With Slack MCP
```
# Team collaboration
1. Use slack MCP for team communication
2. Use notion MCP for knowledge sharing
3. Sync important discussions to Notion
4. Create shared team documentation
```

## Workflow Examples

### Project Management
```
1. Create project database with tasks, milestones, and resources
2. Set up automated status updates and notifications
3. Generate weekly progress reports
4. Track team performance and productivity metrics
5. Maintain project documentation and lessons learned
```

### Knowledge Management
```
1. Create structured knowledge base with categories
2. Implement tagging and cross-referencing system
3. Set up automated content organization
4. Generate summaries and insights
5. Maintain searchable documentation library
```

### Personal Productivity
```
1. Set up personal dashboard with goals and metrics
2. Create automated daily and weekly reviews
3. Track habits and productivity patterns
4. Generate insights and recommendations
5. Maintain personal knowledge repository
```

## Links

- [Official Notion MCP](https://github.com/makenotion/notion-mcp-server)
- [Notion API Documentation](https://developers.notion.com/)
- [Notion Integration Guide](https://developers.notion.com/docs/getting-started)
- [Notion Database Properties](https://developers.notion.com/reference/property-object)
- [Notion Block Types](https://developers.notion.com/reference/block)
- [MCP Specification](https://spec.modelcontextprotocol.io/)

## Community Resources

- [Notion Community](https://www.notion.so/community)
- [Notion API Community](https://developers.notion.com/community)
- [MCP Discord](https://discord.gg/mcp)
- [Reddit r/Notion](https://reddit.com/r/Notion)
- [Notion Templates](https://www.notion.so/templates)

