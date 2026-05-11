# Jira Reader

Read Jira tickets, projects, boards, and sprints using the `acli` CLI tool.

## What It Does

Answers questions about Jira content by fetching data via the Atlassian CLI (`acli`). Supports:

- Viewing tickets, comments, attachments, and links
- Searching with JQL queries
- Listing projects, boards, sprints, dashboards, and filters

## Requirements

- [acli](https://github.com/atlassian/acli) installed and authenticated (`acli jira auth status`)
- Claude Code with skill support

## Installation

```bash
/plugins marketplace add sachchidanandx/ClaudeSkills
/plugins install jira-reader@sachchidanand-skills
```

## Usage

Ask questions naturally:

- "What's the status of PROJ-123?"
- "Show me my open tickets"
- "What's in the current sprint?"
- "List all projects"
