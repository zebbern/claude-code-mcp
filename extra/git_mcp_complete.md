# Git MCP - Complete Guide

## Overview
The Git MCP is an essential Model Context Protocol implementation that provides comprehensive Git version control integration for Claude Code. This MCP transforms Claude Code into a powerful Git client capable of performing complex version control operations, repository management, branch operations, and collaborative development workflows. It enables Claude Code to understand and manipulate Git repositories with full context awareness.

## What Does Git MCP Do?
- **Repository Management**: Initialize, clone, and manage Git repositories
- **Branch Operations**: Create, switch, merge, and delete branches
- **Commit Operations**: Stage, commit, and manage commit history
- **Remote Operations**: Push, pull, fetch, and manage remote repositories
- **Diff and Status**: View changes, diffs, and repository status
- **History Analysis**: Explore commit history, logs, and blame information
- **Conflict Resolution**: Handle merge conflicts and resolution strategies
- **Tag Management**: Create, list, and manage Git tags
- **Stash Operations**: Save and restore work-in-progress changes
- **Advanced Git Features**: Rebase, cherry-pick, bisect, and more

## Installation

### Prerequisites
- Claude Code CLI installed and configured
- Git 2.20+ installed on your system
- Node.js 16+ or Python 3.8+
- Claude Desktop application
- Valid Anthropic API key
- Git configured with user credentials

### Step 1: Install Git MCP Server

#### Option 1: NPM Installation (Recommended)
```bash
# Install the official MCP Git server
npm install -g @modelcontextprotocol/server-git

# Verify installation
npx @modelcontextprotocol/server-git --version

# Test the server
npx @modelcontextprotocol/server-git --help
```

#### Option 2: Python Installation
```bash
# Install Python version
pip install mcp-server-git

# Verify installation
mcp-server-git --version

# Test the server
mcp-server-git --help
```

#### Option 3: Direct from GitHub
```bash
# Clone the repository
git clone https://github.com/modelcontextprotocol/servers.git
cd servers/src/git

# Install dependencies
npm install

# Build the server
npm run build

# Test the server
npm start -- --help
```

#### Option 4: Docker Installation
```bash
# Pull the Docker image
docker pull mcpservers/git:latest

# Run the container
docker run -d --name git-mcp \
  -v /workspace:/workspace \
  -v ~/.gitconfig:/root/.gitconfig:ro \
  -v ~/.ssh:/root/.ssh:ro \
  mcpservers/git:latest

# Verify container is running
docker ps | grep git-mcp
```

### Step 2: Configure Git Credentials
```bash
# Set up Git user information
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Configure SSH keys for GitHub/GitLab (if needed)
ssh-keygen -t ed25519 -C "your.email@example.com"
ssh-add ~/.ssh/id_ed25519

# Test SSH connection
ssh -T git@github.com
ssh -T git@gitlab.com

# Configure credential helper
git config --global credential.helper store
# Or for macOS
git config --global credential.helper osxkeychain
# Or for Windows
git config --global credential.helper manager-core
```

### Step 3: Configure Claude Desktop

#### Basic Configuration
```json
{
  "mcpServers": {
    "git": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "/workspace"
      ],
      "env": {
        "GIT_AUTHOR_NAME": "Claude Code",
        "GIT_AUTHOR_EMAIL": "claude@anthropic.com",
        "GIT_COMMITTER_NAME": "Claude Code",
        "GIT_COMMITTER_EMAIL": "claude@anthropic.com"
      }
    }
  }
}
```

#### Advanced Configuration
```json
{
  "mcpServers": {
    "git-advanced": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "/workspace",
        "--allow-push",
        "--allow-force",
        "--enable-hooks",
        "--max-diff-size", "10MB"
      ],
      "env": {
        "GIT_AUTHOR_NAME": "Claude Code Assistant",
        "GIT_AUTHOR_EMAIL": "claude@yourcompany.com",
        "GIT_COMMITTER_NAME": "Claude Code Assistant",
        "GIT_COMMITTER_EMAIL": "claude@yourcompany.com",
        "GIT_SSH_COMMAND": "ssh -i ~/.ssh/id_ed25519",
        "GIT_TERMINAL_PROMPT": "0",
        "GIT_MERGE_AUTOEDIT": "no",
        "LOG_LEVEL": "info"
      }
    }
  }
}
```

#### Multiple Repository Configuration
```json
{
  "mcpServers": {
    "git-main": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "/workspace/main-project"
      ]
    },
    "git-frontend": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "/workspace/frontend"
      ]
    },
    "git-backend": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-git",
        "/workspace/backend"
      ]
    }
  }
}
```

### Step 4: Verify Installation
```bash
# Check Git installation
git --version

# Test Git MCP server
npx @modelcontextprotocol/server-git /workspace --test

# Initialize a test repository
cd /workspace
git init test-repo
cd test-repo
echo "# Test Repository" > README.md
git add README.md
git commit -m "Initial commit"

# In Claude Desktop, ask:
# "Show me the Git status of the current repository"
# "What is the commit history?"
# "Create a new branch called 'feature/test'"
```

## Commands and Usage

### Repository Management

#### Initializing and Cloning Repositories
```bash
# Claude Code commands:
"Initialize a new Git repository in the current directory"
"Clone the repository https://github.com/user/repo.git"
"Clone the repository into a specific directory called 'my-project'"
"Set up a bare repository for sharing"

# Direct MCP tool calls:
git_init: {
  "path": "/workspace/new-project",
  "bare": false
}

git_clone: {
  "url": "https://github.com/user/repo.git",
  "destination": "/workspace/cloned-repo",
  "branch": "main",
  "depth": 1
}
```

#### Repository Status and Information
```bash
# Claude Code commands:
"Show me the current Git status"
"What files have been modified?"
"Display the repository information and remotes"
"Check if the working directory is clean"

# Direct MCP tool calls:
git_status: {
  "path": "/workspace/project",
  "porcelain": false,
  "show_branch": true
}

git_remote: {
  "action": "list",
  "verbose": true
}
```

### Branch Operations

#### Creating and Managing Branches
```bash
# Claude Code commands:
"Create a new branch called 'feature/user-authentication'"
"Switch to the 'development' branch"
"List all local and remote branches"
"Delete the 'old-feature' branch"
"Rename the current branch to 'main'"

# Direct MCP tool calls:
git_branch: {
  "action": "create",
  "name": "feature/user-authentication",
  "start_point": "main"
}

git_checkout: {
  "branch": "development",
  "create": false,
  "force": false
}

git_branch: {
  "action": "list",
  "remote": true,
  "verbose": true
}
```

#### Branch Merging and Rebasing
```bash
# Claude Code commands:
"Merge the 'feature/login' branch into 'main'"
"Rebase the current branch onto 'main'"
"Perform an interactive rebase for the last 5 commits"
"Abort the current merge/rebase operation"

# Direct MCP tool calls:
git_merge: {
  "branch": "feature/login",
  "strategy": "recursive",
  "no_ff": true,
  "message": "Merge feature/login into main"
}

git_rebase: {
  "onto": "main",
  "interactive": false,
  "preserve_merges": false
}
```

### Commit Operations

#### Staging and Committing Changes
```bash
# Claude Code commands:
"Stage all modified files for commit"
"Stage only the changes in src/main.js"
"Commit the staged changes with message 'Add user authentication'"
"Commit all changes with a descriptive message"
"Amend the last commit with additional changes"

# Direct MCP tool calls:
git_add: {
  "files": ["src/main.js", "src/auth.js"],
  "all": false,
  "force": false
}

git_commit: {
  "message": "Add user authentication feature\n\n- Implement login/logout functionality\n- Add password validation\n- Update user interface",
  "all": false,
  "amend": false,
  "sign_off": true
}
```

#### Viewing and Managing Commit History
```bash
# Claude Code commands:
"Show the commit history for the last 10 commits"
"Display the commit log with file changes"
"Show the details of commit abc123"
"Find commits that modified the file 'config.js'"
"Show commits by author 'John Doe' in the last month"

# Direct MCP tool calls:
git_log: {
  "max_count": 10,
  "oneline": false,
  "graph": true,
  "stat": true,
  "since": "1 month ago",
  "author": "John Doe"
}

git_show: {
  "commit": "abc123",
  "stat": true,
  "name_only": false
}
```

### Diff and Change Analysis

#### Viewing Changes and Differences
```bash
# Claude Code commands:
"Show the differences between the working directory and the last commit"
"Display the changes in the staging area"
"Compare the current branch with 'main'"
"Show the differences for a specific file between two commits"

# Direct MCP tool calls:
git_diff: {
  "staged": false,
  "cached": false,
  "name_only": false,
  "stat": true
}

git_diff: {
  "commit1": "main",
  "commit2": "feature/auth",
  "files": ["src/auth.js"],
  "word_diff": true
}
```

#### Blame and File History
```bash
# Claude Code commands:
"Show who last modified each line in 'src/main.js'"
"Display the commit history for 'README.md'"
"Find when a specific function was introduced"
"Show the evolution of a file over time"

# Direct MCP tool calls:
git_blame: {
  "file": "src/main.js",
  "line_start": 1,
  "line_end": 50,
  "show_email": true
}

git_log: {
  "file": "README.md",
  "follow": true,
  "patch": true
}
```

### Remote Operations

#### Working with Remote Repositories
```bash
# Claude Code commands:
"Add a remote repository called 'upstream'"
"Fetch the latest changes from all remotes"
"Pull the latest changes from 'origin/main'"
"Push the current branch to 'origin'"
"Push all tags to the remote repository"

# Direct MCP tool calls:
git_remote: {
  "action": "add",
  "name": "upstream",
  "url": "https://github.com/original/repo.git"
}

git_fetch: {
  "remote": "origin",
  "all": true,
  "tags": true,
  "prune": true
}

git_pull: {
  "remote": "origin",
  "branch": "main",
  "rebase": false,
  "ff_only": true
}

git_push: {
  "remote": "origin",
  "branch": "feature/auth",
  "set_upstream": true,
  "force": false,
  "tags": false
}
```

### Advanced Git Operations

#### Stash Operations
```bash
# Claude Code commands:
"Stash the current changes with a message"
"List all stashes"
"Apply the most recent stash"
"Pop the stash and remove it from the stash list"
"Drop a specific stash"

# Direct MCP tool calls:
git_stash: {
  "action": "save",
  "message": "Work in progress on authentication feature",
  "include_untracked": true,
  "keep_index": false
}

git_stash: {
  "action": "list",
  "show_patch": true
}

git_stash: {
  "action": "apply",
  "stash": "stash@{0}",
  "index": false
}
```

#### Tag Management
```bash
# Claude Code commands:
"Create a new tag 'v1.0.0' for the current commit"
"List all tags in the repository"
"Create an annotated tag with a message"
"Delete a tag locally and remotely"
"Push all tags to the remote repository"

# Direct MCP tool calls:
git_tag: {
  "action": "create",
  "name": "v1.0.0",
  "message": "Release version 1.0.0",
  "annotated": true,
  "sign": false
}

git_tag: {
  "action": "list",
  "pattern": "v*",
  "sort": "version:refname"
}
```

#### Cherry-pick and Advanced Operations
```bash
# Claude Code commands:
"Cherry-pick commit abc123 to the current branch"
"Start a bisect session to find a bug"
"Reset the repository to a specific commit"
"Clean untracked files from the working directory"

# Direct MCP tool calls:
git_cherry_pick: {
  "commits": ["abc123", "def456"],
  "no_commit": false,
  "sign_off": true
}

git_reset: {
  "mode": "mixed",
  "commit": "HEAD~1",
  "hard": false
}

git_clean: {
  "force": true,
  "directories": true,
  "ignored": false,
  "dry_run": false
}
```

## Usage Examples

### Development Workflow Integration
```bash
# Example 1: Feature development workflow
"I'm starting work on a new user authentication feature. Please:
1. Create a new branch called 'feature/user-auth' from 'main'
2. Switch to this new branch
3. Show me the current status
4. List any existing authentication-related files"

# Example 2: Code review preparation
"Prepare this branch for code review by:
1. Showing all commits since branching from 'main'
2. Displaying the overall diff against 'main'
3. Listing all modified files
4. Checking for any merge conflicts with 'main'"

# Example 3: Release preparation
"Prepare for a new release by:
1. Merging 'development' into 'main'
2. Creating a tag 'v2.1.0' with release notes
3. Pushing the changes and tags to origin
4. Generating a changelog since the last release"
```

### Collaborative Development
```bash
# Example 1: Syncing with team changes
"Sync my local repository with the team's latest changes:
1. Fetch all remote branches and tags
2. Show what's new on 'origin/main'
3. Rebase my current feature branch onto the latest 'main'
4. Resolve any conflicts if they exist"

# Example 2: Contributing to open source
"Prepare to contribute to an open source project:
1. Add the upstream repository as a remote
2. Fetch the latest changes from upstream
3. Create a new branch for my contribution
4. Show the contribution guidelines if they exist"

# Example 3: Code archaeology
"Investigate when and why a bug was introduced:
1. Find all commits that modified the problematic file
2. Show the blame information for the buggy lines
3. Display the commit that introduced the issue
4. Show the full context of that commit"
```

### Repository Maintenance
```bash
# Example 1: Cleaning up the repository
"Clean up the repository by:
1. Removing merged feature branches
2. Cleaning up stale remote tracking branches
3. Garbage collecting to optimize storage
4. Checking repository integrity"

# Example 2: Backup and archiving
"Create a backup of the current state:
1. Create a comprehensive bundle of the repository
2. Export all branches and tags
3. Generate a summary of the repository state
4. Create an archive of the working directory"

# Example 3: Migration assistance
"Help migrate this repository:
1. List all remotes and their URLs
2. Show the complete branch structure
3. Identify any large files or binary assets
4. Generate a migration checklist"
```

## Editing and Customization

### Custom Git Workflows
```javascript
// Define custom Git workflows
const customWorkflows = {
  // Feature development workflow
  featureWorkflow: async (featureName) => {
    const branchName = `feature/${featureName}`;
    
    // Ensure we're on main and up to date
    await gitCheckout('main');
    await gitPull('origin', 'main');
    
    // Create and switch to feature branch
    await gitBranch('create', branchName, 'main');
    await gitCheckout(branchName);
    
    return {
      branch: branchName,
      status: 'ready for development',
      nextSteps: [
        'Make your changes',
        'Commit regularly with descriptive messages',
        'Push to origin when ready for review'
      ]
    };
  },

  // Release workflow
  releaseWorkflow: async (version) => {
    // Merge development into main
    await gitCheckout('main');
    await gitMerge('development', { noFf: true });
    
    // Create release tag
    await gitTag('create', `v${version}`, {
      annotated: true,
      message: `Release version ${version}`
    });
    
    // Push changes and tags
    await gitPush('origin', 'main');
    await gitPush('origin', '--tags');
    
    return {
      version: `v${version}`,
      status: 'released',
      actions: ['main updated', 'tag created', 'pushed to origin']
    };
  },

  // Hotfix workflow
  hotfixWorkflow: async (issueDescription) => {
    const branchName = `hotfix/${issueDescription.replace(/\s+/g, '-').toLowerCase()}`;
    
    // Create hotfix branch from main
    await gitCheckout('main');
    await gitBranch('create', branchName, 'main');
    await gitCheckout(branchName);
    
    return {
      branch: branchName,
      status: 'ready for hotfix',
      workflow: [
        'Fix the critical issue',
        'Test thoroughly',
        'Merge into main and development',
        'Tag with patch version'
      ]
    };
  }
};
```

### Git Hook Integration
```bash
#!/bin/bash
# Custom pre-commit hook

# File: .git/hooks/pre-commit
set -e

echo "Running pre-commit checks..."

# Check for debugging statements
if git diff --cached --name-only | xargs grep -l "console.log\|debugger\|pdb.set_trace" 2>/dev/null; then
    echo "Error: Debugging statements found in staged files"
    echo "Please remove console.log, debugger, or pdb.set_trace statements"
    exit 1
fi

# Check for merge conflict markers
if git diff --cached --name-only | xargs grep -l "<<<<<<< HEAD\|>>>>>>> \|=======" 2>/dev/null; then
    echo "Error: Merge conflict markers found in staged files"
    echo "Please resolve all merge conflicts before committing"
    exit 1
fi

# Run linting
echo "Running linter..."
npm run lint:staged || {
    echo "Error: Linting failed"
    echo "Please fix linting errors before committing"
    exit 1
}

# Run tests
echo "Running tests..."
npm test || {
    echo "Error: Tests failed"
    echo "Please ensure all tests pass before committing"
    exit 1
}

echo "Pre-commit checks passed!"
```

### Configuration Customization
```json
{
  "git": {
    "defaultBranch": "main",
    "autoFetch": {
      "enabled": true,
      "interval": 300,
      "remotes": ["origin", "upstream"]
    },
    "commitTemplate": {
      "enabled": true,
      "template": "{{type}}({{scope}}): {{description}}\n\n{{body}}\n\n{{footer}}"
    },
    "branchNaming": {
      "enforceConvention": true,
      "patterns": [
        "feature/*",
        "bugfix/*",
        "hotfix/*",
        "release/*",
        "chore/*"
      ]
    },
    "mergeStrategy": {
      "default": "merge",
      "featureBranches": "squash",
      "hotfixes": "merge",
      "releases": "merge"
    },
    "pushBehavior": {
      "autoSetUpstream": true,
      "requireReview": true,
      "protectedBranches": ["main", "development"]
    },
    "cleanup": {
      "autoDeleteMergedBranches": true,
      "pruneRemoteTrackingBranches": true,
      "gcAggressive": false
    }
  }
}
```

### Advanced Scripting
```bash
#!/bin/bash
# Advanced Git management script

# Function to create a comprehensive repository report
generate_repo_report() {
    local repo_path=$1
    local output_file="repo-report-$(date +%Y%m%d).md"
    
    cd "$repo_path" || exit 1
    
    cat > "$output_file" << EOF
# Repository Report - $(date)

## Repository Information
- **Path**: $(pwd)
- **Remote Origin**: $(git remote get-url origin 2>/dev/null || echo "No origin remote")
- **Current Branch**: $(git branch --show-current)
- **Total Commits**: $(git rev-list --all --count)
- **Contributors**: $(git shortlog -sn | wc -l)

## Branch Information
\`\`\`
$(git branch -a)
\`\`\`

## Recent Activity (Last 10 commits)
\`\`\`
$(git log --oneline -10)
\`\`\`

## Repository Statistics
- **Total Files**: $(git ls-files | wc -l)
- **Lines of Code**: $(git ls-files | xargs wc -l | tail -1)
- **Repository Size**: $(du -sh .git | cut -f1)

## Top Contributors
\`\`\`
$(git shortlog -sn | head -10)
\`\`\`

## File Type Distribution
\`\`\`
$(git ls-files | sed 's/.*\.//' | sort | uniq -c | sort -nr | head -10)
\`\`\`
EOF

    echo "Repository report generated: $output_file"
}

# Function to perform intelligent branch cleanup
intelligent_cleanup() {
    local repo_path=$1
    
    cd "$repo_path" || exit 1
    
    echo "Performing intelligent repository cleanup..."
    
    # Fetch latest changes
    git fetch --all --prune
    
    # Find merged branches (excluding main/master/development)
    local merged_branches=$(git branch --merged main | grep -v -E "(main|master|development|\*)" | xargs)
    
    if [ -n "$merged_branches" ]; then
        echo "Found merged branches: $merged_branches"
        read -p "Delete these merged branches? (y/N): " -n 1 -r
        echo
        if [[ $REPLY =~ ^[Yy]$ ]]; then
            echo "$merged_branches" | xargs git branch -d
            echo "Merged branches deleted"
        fi
    else
        echo "No merged branches found"
    fi
    
    # Clean up remote tracking branches
    git remote prune origin
    
    # Garbage collect
    git gc --aggressive --prune=now
    
    echo "Cleanup completed"
}

# Function to create a backup bundle
create_backup_bundle() {
    local repo_path=$1
    local backup_dir=${2:-"./backups"}
    
    cd "$repo_path" || exit 1
    
    mkdir -p "$backup_dir"
    local bundle_name="backup-$(basename $(pwd))-$(date +%Y%m%d-%H%M%S).bundle"
    local bundle_path="$backup_dir/$bundle_name"
    
    echo "Creating backup bundle: $bundle_path"
    git bundle create "$bundle_path" --all
    
    # Create verification file
    git bundle verify "$bundle_path" > "$backup_dir/${bundle_name}.verify"
    
    echo "Backup created successfully: $bundle_path"
    echo "Verification: $backup_dir/${bundle_name}.verify"
}

# Main execution
case "$1" in
    report)
        generate_repo_report "$2"
        ;;
    cleanup)
        intelligent_cleanup "$2"
        ;;
    backup)
        create_backup_bundle "$2" "$3"
        ;;
    *)
        echo "Usage: $0 {report|cleanup|backup} <repo_path> [backup_dir]"
        exit 1
        ;;
esac
```

## Advanced Features

### Git Flow Integration
```javascript
// Git Flow implementation
const gitFlow = {
  init: async (developBranch = 'develop', masterBranch = 'main') => {
    // Initialize git flow
    await gitCheckout(masterBranch);
    await gitBranch('create', developBranch, masterBranch);
    
    return {
      master: masterBranch,
      develop: developBranch,
      status: 'initialized'
    };
  },

  startFeature: async (featureName) => {
    const branchName = `feature/${featureName}`;
    await gitCheckout('develop');
    await gitPull('origin', 'develop');
    await gitBranch('create', branchName, 'develop');
    await gitCheckout(branchName);
    
    return { branch: branchName, status: 'started' };
  },

  finishFeature: async (featureName) => {
    const branchName = `feature/${featureName}`;
    
    // Merge feature into develop
    await gitCheckout('develop');
    await gitMerge(branchName, { noFf: true });
    
    // Delete feature branch
    await gitBranch('delete', branchName);
    
    // Push develop
    await gitPush('origin', 'develop');
    
    return { status: 'finished', merged: 'develop' };
  },

  startRelease: async (version) => {
    const branchName = `release/${version}`;
    await gitCheckout('develop');
    await gitBranch('create', branchName, 'develop');
    await gitCheckout(branchName);
    
    return { branch: branchName, version, status: 'started' };
  },

  finishRelease: async (version) => {
    const branchName = `release/${version}`;
    
    // Merge into main
    await gitCheckout('main');
    await gitMerge(branchName, { noFf: true });
    await gitTag('create', `v${version}`, { annotated: true });
    
    // Merge into develop
    await gitCheckout('develop');
    await gitMerge(branchName, { noFf: true });
    
    // Delete release branch
    await gitBranch('delete', branchName);
    
    // Push everything
    await gitPush('origin', 'main');
    await gitPush('origin', 'develop');
    await gitPush('origin', '--tags');
    
    return { version: `v${version}`, status: 'released' };
  }
};
```

### Conflict Resolution Assistant
```javascript
// Intelligent conflict resolution
const conflictResolver = {
  detectConflicts: async () => {
    const status = await gitStatus();
    const conflicts = status.files.filter(file => file.status === 'UU');
    
    return conflicts.map(file => ({
      file: file.path,
      type: this.analyzeConflictType(file.path),
      suggestions: this.generateResolutionSuggestions(file.path)
    }));
  },

  analyzeConflictType: (filePath) => {
    const content = readFile(filePath);
    const conflictMarkers = content.match(/<<<<<<< HEAD[\s\S]*?>>>>>>> /g) || [];
    
    return conflictMarkers.map(marker => {
      const lines = marker.split('\n');
      const headContent = lines.slice(1, lines.findIndex(l => l.includes('======='))).join('\n');
      const incomingContent = lines.slice(lines.findIndex(l => l.includes('=======')) + 1, -1).join('\n');
      
      return {
        type: this.classifyConflict(headContent, incomingContent),
        headContent,
        incomingContent,
        suggestion: this.suggestResolution(headContent, incomingContent)
      };
    });
  },

  classifyConflict: (head, incoming) => {
    if (head.trim() === '' || incoming.trim() === '') return 'deletion';
    if (head.includes('import') && incoming.includes('import')) return 'import';
    if (head.includes('function') && incoming.includes('function')) return 'function';
    if (head.includes('{') && incoming.includes('{')) return 'object';
    return 'content';
  },

  suggestResolution: (head, incoming) => {
    // Implement intelligent resolution suggestions
    return {
      strategy: 'manual',
      recommendation: 'Review both changes and merge manually',
      autoResolvable: false
    };
  },

  resolveConflict: async (filePath, resolution) => {
    const content = readFile(filePath);
    const resolved = this.applyResolution(content, resolution);
    await writeFile(filePath, resolved);
    await gitAdd([filePath]);
    
    return { file: filePath, status: 'resolved' };
  }
};
```

### Repository Analytics
```javascript
// Advanced repository analytics
const repoAnalytics = {
  generateMetrics: async () => {
    const commits = await gitLog({ all: true });
    const contributors = await this.getContributors();
    const fileStats = await this.getFileStatistics();
    
    return {
      overview: {
        totalCommits: commits.length,
        totalContributors: contributors.length,
        totalFiles: fileStats.totalFiles,
        totalLines: fileStats.totalLines,
        repositoryAge: this.calculateAge(commits[commits.length - 1].date)
      },
      activity: {
        commitsPerMonth: this.groupCommitsByMonth(commits),
        commitsPerContributor: this.groupCommitsByContributor(commits),
        filesChangedOverTime: this.analyzeFileChanges(commits)
      },
      codeQuality: {
        averageCommitSize: this.calculateAverageCommitSize(commits),
        commitMessageQuality: this.analyzeCommitMessages(commits),
        branchingStrategy: this.analyzeBranchingStrategy()
      },
      trends: {
        activityTrend: this.calculateActivityTrend(commits),
        contributorGrowth: this.calculateContributorGrowth(commits),
        codebaseGrowth: this.calculateCodebaseGrowth(commits)
      }
    };
  },

  generateReport: async (metrics) => {
    const report = `
# Repository Analytics Report

## Overview
- **Total Commits**: ${metrics.overview.totalCommits}
- **Contributors**: ${metrics.overview.totalContributors}
- **Files**: ${metrics.overview.totalFiles}
- **Lines of Code**: ${metrics.overview.totalLines}
- **Repository Age**: ${metrics.overview.repositoryAge}

## Activity Analysis
${this.formatActivityAnalysis(metrics.activity)}

## Code Quality Metrics
${this.formatQualityMetrics(metrics.codeQuality)}

## Trends and Insights
${this.formatTrends(metrics.trends)}

## Recommendations
${this.generateRecommendations(metrics)}
    `;

    await writeFile('repository-analytics.md', report);
    return report;
  }
};
```

## Troubleshooting

### Common Issues and Solutions

#### Authentication Problems
```bash
# Issue: SSH authentication fails
# Solution:
# 1. Check SSH key
ssh-add -l
ssh-keygen -t ed25519 -C "your.email@example.com"

# 2. Add key to SSH agent
ssh-add ~/.ssh/id_ed25519

# 3. Test connection
ssh -T git@github.com

# 4. Configure SSH in Git
git config --global core.sshCommand "ssh -i ~/.ssh/id_ed25519"

# Issue: HTTPS authentication fails
# Solution:
# 1. Update credentials
git config --global credential.helper store
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 2. Clear cached credentials
git config --global --unset credential.helper
git credential-manager-core erase

# 3. Use personal access token
git remote set-url origin https://username:token@github.com/user/repo.git
```

#### Repository Issues
```bash
# Issue: Repository corruption
# Solution:
# 1. Check repository integrity
git fsck --full

# 2. Recover from corruption
git reflog
git reset --hard HEAD@{1}

# 3. Rebuild index
rm .git/index
git reset

# Issue: Large repository size
# Solution:
# 1. Find large files
git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | sed -n 's/^blob //p' | sort --numeric-sort --key=2 | tail -10

# 2. Remove large files from history
git filter-branch --tree-filter 'rm -f large-file.bin' HEAD
git for-each-ref --format='delete %(refname)' refs/original | git update-ref --stdin

# 3. Garbage collect
git gc --aggressive --prune=now
```

#### Merge and Conflict Issues
```bash
# Issue: Complex merge conflicts
# Solution:
# 1. Use merge tool
git config --global merge.tool vimdiff
git mergetool

# 2. Abort and retry
git merge --abort
git rebase --abort

# 3. Use different merge strategy
git merge -X theirs branch-name
git merge -X ours branch-name

# Issue: Detached HEAD state
# Solution:
# 1. Create branch from current state
git checkout -b new-branch-name

# 2. Return to previous branch
git checkout main

# 3. Discard changes
git checkout main
```

### Diagnostic Commands
```bash
# Comprehensive Git diagnostics
git-diagnose() {
    echo "=== Git Diagnostics ==="
    echo "Git Version: $(git --version)"
    echo "Repository: $(git rev-parse --show-toplevel 2>/dev/null || echo 'Not in a Git repository')"
    echo "Current Branch: $(git branch --show-current 2>/dev/null || echo 'No branch')"
    echo "Remote Origin: $(git remote get-url origin 2>/dev/null || echo 'No origin remote')"
    echo "Working Directory Status: $(git status --porcelain | wc -l) files changed"
    echo "Stash Count: $(git stash list | wc -l)"
    echo "Local Branches: $(git branch | wc -l)"
    echo "Remote Branches: $(git branch -r | wc -l)"
    echo "Tags: $(git tag | wc -l)"
    echo "Last Commit: $(git log -1 --format='%h %s' 2>/dev/null || echo 'No commits')"
    echo "Repository Size: $(du -sh .git 2>/dev/null | cut -f1 || echo 'Unknown')"
    
    echo -e "\n=== Configuration ==="
    git config --list | grep -E "(user\.|core\.|remote\.)" | head -10
    
    echo -e "\n=== Recent Activity ==="
    git log --oneline -5 2>/dev/null || echo "No commit history"
    
    echo -e "\n=== Potential Issues ==="
    # Check for common issues
    if [ ! -d .git ]; then
        echo "❌ Not in a Git repository"
    else
        echo "✅ Valid Git repository"
    fi
    
    if git status --porcelain | grep -q "^UU"; then
        echo "❌ Merge conflicts detected"
    else
        echo "✅ No merge conflicts"
    fi
    
    if [ $(git stash list | wc -l) -gt 5 ]; then
        echo "⚠️  Many stashes ($(git stash list | wc -l)) - consider cleaning up"
    fi
}

# Performance analysis
git-performance() {
    echo "=== Git Performance Analysis ==="
    
    # Repository size analysis
    echo "Repository size breakdown:"
    echo "  .git directory: $(du -sh .git | cut -f1)"
    echo "  Working directory: $(du -sh --exclude=.git . | cut -f1)"
    echo "  Objects: $(git count-objects -v | grep 'count\|size')"
    
    # Performance metrics
    echo -e "\nPerformance metrics:"
    time git status >/dev/null 2>&1
    time git log --oneline -100 >/dev/null 2>&1
    
    # Recommendations
    echo -e "\nRecommendations:"
    if [ $(git count-objects -v | grep "^count" | cut -d' ' -f2) -gt 10000 ]; then
        echo "  - Consider running 'git gc --aggressive'"
    fi
    
    if [ $(du -s .git | cut -f1) -gt 100000 ]; then
        echo "  - Repository is large, consider using Git LFS for binary files"
    fi
}
```

## Security Considerations

### Repository Security
```json
{
  "security": {
    "authentication": {
      "enforceSSH": true,
      "requireSignedCommits": false,
      "allowedUsers": ["user1", "user2"],
      "sshKeyValidation": "strict"
    },
    "branchProtection": {
      "protectedBranches": ["main", "master", "develop"],
      "requireReviews": true,
      "minimumReviewers": 2,
      "dismissStaleReviews": true,
      "requireStatusChecks": true
    },
    "commitSigning": {
      "enabled": false,
      "requireGPG": false,
      "allowedSigners": [],
      "verifySignatures": true
    },
    "accessControl": {
      "allowForce": false,
      "allowRewrite": false,
      "allowDelete": false,
      "restrictPaths": [".github/", "config/", "secrets/"]
    },
    "auditLogging": {
      "enabled": true,
      "logFile": "/var/log/git-mcp-audit.log",
      "logLevel": "detailed",
      "events": ["push", "pull", "clone", "branch", "tag"]
    }
  }
}
```

### Sensitive Data Protection
```bash
#!/bin/bash
# Git security scanner

scan_for_secrets() {
    echo "Scanning for potential secrets..."
    
    # Common secret patterns
    local patterns=(
        "password\s*=\s*['\"][^'\"]+['\"]"
        "api[_-]?key\s*=\s*['\"][^'\"]+['\"]"
        "secret\s*=\s*['\"][^'\"]+['\"]"
        "token\s*=\s*['\"][^'\"]+['\"]"
        "-----BEGIN.*PRIVATE KEY-----"
        "ssh-rsa\s+[A-Za-z0-9+/]+"
    )
    
    for pattern in "${patterns[@]}"; do
        echo "Checking for: $pattern"
        git log --all -p | grep -E "$pattern" && echo "⚠️  Potential secret found!"
    done
}

# Pre-commit hook for secret detection
pre_commit_security_check() {
    # Check staged files for secrets
    git diff --cached --name-only | while read file; do
        if [ -f "$file" ]; then
            # Check for common secret patterns
            if grep -qE "(password|api_key|secret|token)\s*=\s*['\"][^'\"]+['\"]" "$file"; then
                echo "❌ Potential secret found in $file"
                exit 1
            fi
        fi
    done
    
    echo "✅ Security check passed"
}
```

## Performance Optimization

### Repository Optimization
```bash
#!/bin/bash
# Git repository optimization

optimize_repository() {
    local repo_path=$1
    cd "$repo_path" || exit 1
    
    echo "Optimizing Git repository..."
    
    # 1. Garbage collection
    echo "Running garbage collection..."
    git gc --aggressive --prune=now
    
    # 2. Repack objects
    echo "Repacking objects..."
    git repack -ad
    
    # 3. Clean up reflog
    echo "Cleaning reflog..."
    git reflog expire --expire=30.days --all
    
    # 4. Prune remote tracking branches
    echo "Pruning remote branches..."
    git remote prune origin
    
    # 5. Optimize configuration
    echo "Optimizing configuration..."
    git config core.preloadindex true
    git config core.fscache true
    git config gc.auto 256
    
    echo "Optimization complete!"
    
    # Show results
    echo "Repository size: $(du -sh .git | cut -f1)"
    echo "Object count: $(git count-objects -v | grep '^count' | cut -d' ' -f2)"
}

# Large file detection and management
manage_large_files() {
    echo "Analyzing large files..."
    
    # Find large files in history
    git rev-list --objects --all | \
    git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
    awk '/^blob/ {print substr($0,6)}' | \
    sort --numeric-sort --key=2 | \
    tail -20
    
    echo "Consider using Git LFS for files larger than 100MB"
}
```

### Performance Monitoring
```javascript
// Git performance monitoring
const performanceMonitor = {
  measureOperation: async (operation, ...args) => {
    const startTime = Date.now();
    const startMemory = process.memoryUsage();
    
    try {
      const result = await operation(...args);
      const endTime = Date.now();
      const endMemory = process.memoryUsage();
      
      return {
        result,
        metrics: {
          duration: endTime - startTime,
          memoryDelta: {
            rss: endMemory.rss - startMemory.rss,
            heapUsed: endMemory.heapUsed - startMemory.heapUsed
          }
        }
      };
    } catch (error) {
      return {
        error,
        metrics: {
          duration: Date.now() - startTime,
          failed: true
        }
      };
    }
  },

  benchmarkOperations: async () => {
    const operations = [
      { name: 'git status', fn: () => gitStatus() },
      { name: 'git log', fn: () => gitLog({ maxCount: 100 }) },
      { name: 'git diff', fn: () => gitDiff() },
      { name: 'git branch list', fn: () => gitBranch('list') }
    ];

    const results = {};
    
    for (const op of operations) {
      console.log(`Benchmarking ${op.name}...`);
      const result = await this.measureOperation(op.fn);
      results[op.name] = result.metrics;
    }
    
    return results;
  }
};
```

## API Reference

### Core Git Operations
```typescript
interface GitMCP {
  // Repository management
  init(path: string, options?: InitOptions): Promise<void>;
  clone(url: string, destination: string, options?: CloneOptions): Promise<void>;
  status(options?: StatusOptions): Promise<GitStatus>;
  
  // Branch operations
  branch(action: BranchAction, name?: string, options?: BranchOptions): Promise<BranchResult>;
  checkout(branch: string, options?: CheckoutOptions): Promise<void>;
  merge(branch: string, options?: MergeOptions): Promise<MergeResult>;
  rebase(onto: string, options?: RebaseOptions): Promise<void>;
  
  // Commit operations
  add(files: string[], options?: AddOptions): Promise<void>;
  commit(message: string, options?: CommitOptions): Promise<CommitResult>;
  log(options?: LogOptions): Promise<GitCommit[]>;
  show(commit: string, options?: ShowOptions): Promise<CommitDetails>;
  
  // Remote operations
  remote(action: RemoteAction, name?: string, url?: string): Promise<RemoteResult>;
  fetch(remote?: string, options?: FetchOptions): Promise<void>;
  pull(remote?: string, branch?: string, options?: PullOptions): Promise<void>;
  push(remote?: string, branch?: string, options?: PushOptions): Promise<void>;
  
  // Diff and analysis
  diff(options?: DiffOptions): Promise<GitDiff>;
  blame(file: string, options?: BlameOptions): Promise<BlameResult>;
  
  // Advanced operations
  stash(action: StashAction, options?: StashOptions): Promise<StashResult>;
  tag(action: TagAction, name?: string, options?: TagOptions): Promise<TagResult>;
  cherryPick(commits: string[], options?: CherryPickOptions): Promise<void>;
  reset(mode: ResetMode, commit?: string): Promise<void>;
  clean(options?: CleanOptions): Promise<void>;
}

interface GitStatus {
  branch: string;
  ahead: number;
  behind: number;
  files: GitFileStatus[];
  clean: boolean;
}

interface GitFileStatus {
  path: string;
  status: 'M' | 'A' | 'D' | 'R' | 'C' | 'U' | '??';
  staged: boolean;
  unstaged: boolean;
}

interface GitCommit {
  hash: string;
  shortHash: string;
  author: GitAuthor;
  committer: GitAuthor;
  date: Date;
  message: string;
  body: string;
  files: string[];
}

interface GitAuthor {
  name: string;
  email: string;
  date: Date;
}
```

## Links and Resources

- [Official Git MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/git)
- [Git Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book)
- [Git Flow Workflow](https://nvie.com/posts/a-successful-git-branching-model/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Hooks Documentation](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)

## Community and Support

- [Git Community](https://git-scm.com/community)
- [MCP Community Discord](https://discord.gg/mcp)
- [Stack Overflow Git](https://stackoverflow.com/questions/tagged/git)
- [GitHub Community](https://github.community/)
- [GitLab Community](https://about.gitlab.com/community/)
- [Git User Manual](https://git-scm.com/docs/user-manual)
- [Git Tutorial](https://git-scm.com/docs/gittutorial)

