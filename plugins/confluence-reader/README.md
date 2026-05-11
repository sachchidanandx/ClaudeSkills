# Confluence Reader

Read Confluence pages, spaces, and blog posts using the `acli` CLI tool.

## What It Does

Answers questions about Confluence content by fetching data via the Atlassian CLI (`acli`). Supports:

- Viewing pages and their content
- Listing spaces (global and personal)
- Browsing and reading blog posts

## Requirements

- [acli](https://github.com/atlassian/acli) installed and authenticated (`acli confluence auth status`)
- Claude Code with skill support

## Installation

```bash
/plugins marketplace add sachchidanandx/ClaudeSkills
/plugins install confluence-reader@sachchidanand-skills
```

## Usage

Ask questions naturally:

- "What does the wiki say about deployment procedures?"
- "Find the confluence page for our API documentation"
- "List all spaces"
- "Show me blog posts in the engineering space"
