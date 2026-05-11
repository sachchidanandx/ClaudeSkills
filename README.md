# ClaudeSkills Marketplace

Custom Claude Code plugins, skills, and agents by Sachchidanand Kumar.

## Installation

```bash
/plugins marketplace add sachchidanandx/ClaudeSkills
```

Then install individual plugins:

```bash
/plugins install <plugin-name>@sachchidanand-skills
```

## Available Plugins

| Plugin                | Type  | Description                                                              |
| --------------------- | ----- | ------------------------------------------------------------------------ |
| **codebase-explorer** | Agent | Socratic mentor that guides interactive learning of unfamiliar codebases |
| **jira-reader**       | Skill | Read Jira tickets, projects, boards, and sprints via acli CLI            |
| **confluence-reader** | Skill | Read Confluence pages, spaces, and blog posts via acli CLI               |
| **openstack-webui**   | Skill | Interact with OpenStack Horizon dashboard via browser automation         |

## Plugin Details

### codebase-explorer

An agent that teaches you to navigate codebases through Socratic questioning. Instead of dumping documentation, it asks what you think, validates your mental model, and corrects incrementally. Supports Go, Python, and JavaScript/TypeScript.

### jira-reader

A read-only skill for querying Jira. Supports ticket lookup, JQL search, sprint/board browsing, and more. Requires the `acli` CLI tool.

### confluence-reader

A read-only skill for fetching Confluence content. Browse spaces, read pages, and search blog posts. Requires the `acli` CLI tool.

### openstack-webui

A skill that automates the OpenStack Horizon dashboard via Playwright. Launch instances, manage networking, configure security groups, and more through natural language. Requires the `playwright` plugin.
