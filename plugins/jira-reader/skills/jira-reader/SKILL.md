---
name: jira-reader
description: Use this skill whenever the user asks about Jira tickets, issues, stories, bugs, epics, sprints, boards, or projects. This includes questions like "what's the status of PROJ-123", "show me my open tickets", "what's in the current sprint", "list projects", or any request that involves reading information from Jira. Always use this skill when the user mentions Jira, tickets, issues, sprints, boards, or asks about work items and project tracking.
allowed-tools: [Bash(acli jira workitem view*), Bash(acli jira workitem search*), Bash(acli jira workitem comment list*), Bash(acli jira workitem link list*), Bash(acli jira workitem attachment list*), Bash(acli jira workitem watcher list*), Bash(acli jira project list*), Bash(acli jira project view*), Bash(acli jira board search*), Bash(acli jira board get*), Bash(acli jira board list-sprints*), Bash(acli jira board list-projects*), Bash(acli jira sprint view*), Bash(acli jira sprint list-workitems*), Bash(acli jira dashboard search*), Bash(acli jira filter list*), Bash(acli jira filter get*), Bash(acli jira auth status*)]
---

# Jira Reader

Read Jira tickets, projects, boards, and sprints using the `acli` CLI tool. Answer user questions based exclusively on content fetched from Jira.

## Core Principle

Only answer from content retrieved via `acli` commands. Never supplement with outside knowledge. If the information is not found in Jira, say so explicitly.

## Available Commands

### View a Work Item (Ticket)

```bash
acli jira workitem view <KEY> --json
acli jira workitem view <KEY> --fields "*all" --json
acli jira workitem view <KEY> --fields "key,summary,status,assignee,description,priority" --json
```

Use `--fields "*all"` to get every field. Default fields: key, issuetype, summary, status, assignee, description.

### Search Work Items (JQL)

```bash
acli jira workitem search --jql "project = PROJ AND status = 'In Progress'" --json
acli jira workitem search --jql "assignee = currentUser() AND resolution = Unresolved" --json
acli jira workitem search --jql "sprint in openSprints()" --json
acli jira workitem search --filter <FILTER_ID> --json
```

Use `--fields` to control returned columns. Add `--limit` to cap results. Use `--paginate` for all results.

### Comments

```bash
acli jira workitem comment list --key <KEY> --json
acli jira workitem comment list --key <KEY> --order "-created" --json
```

### Links

```bash
acli jira workitem link list --key <KEY> --json
```

### Attachments

```bash
acli jira workitem attachment list --key <KEY> --json
```

### Watchers

```bash
acli jira workitem watcher list --key <KEY> --json
```

### Projects

```bash
acli jira project list --json
acli jira project view --key <PROJECT_KEY> --json
```

### Boards

```bash
acli jira board search --json
acli jira board search --project <PROJECT_KEY> --json
acli jira board search --type scrum --json
acli jira board get --id <BOARD_ID> --json
acli jira board list-sprints --id <BOARD_ID> --state active --json
acli jira board list-projects --id <BOARD_ID> --json
```

### Sprints

```bash
acli jira sprint view --id <SPRINT_ID> --json
acli jira sprint list-workitems --sprint <SPRINT_ID> --board <BOARD_ID> --json
```

### Dashboards and Filters

```bash
acli jira dashboard search --json
acli jira dashboard search --name "my dashboard" --json
acli jira filter list --my --json
acli jira filter list --favourite --json
acli jira filter get --id <FILTER_ID> --json
```

## Workflow

1. **Identify what to fetch**: Determine the ticket key, project, JQL query, or sprint from the user's question.
2. **Direct key lookup**: If the user provides a ticket key (e.g., PROJ-123), use `workitem view` directly.
3. **Search when needed**: If the user asks about multiple tickets or describes criteria, build a JQL query.
4. **Drill down**: After viewing a ticket, offer to fetch comments, links, or related items if relevant.
5. **Answer the question**: Respond based solely on the fetched content.

## Response Guidelines

- Cite the ticket key when answering (e.g., "According to PROJ-123...").
- Present ticket info in a readable format: summary, status, assignee, priority, description.
- For search results, show a concise table or list of key + summary + status.
- If the content is not found, say: "I couldn't find this in Jira. The ticket may not exist, or I may need a different project/query."
- For long descriptions, summarize the relevant parts rather than dumping raw content.

## Tips

- Ticket keys follow the pattern `PROJECT-NUMBER` (e.g., `PROJ-123`, `DEV-456`).
- JQL is case-insensitive for keywords but project keys are uppercase.
- Common JQL fields: `project`, `status`, `assignee`, `reporter`, `priority`, `issuetype`, `sprint`, `labels`, `created`, `updated`.
- Use `currentUser()` in JQL to refer to the authenticated user.
- Use `sprint in openSprints()` to find active sprint items.
- If authentication fails, ask the user to run `acli jira auth status` to check their login state.
