# acli - Atlassian CLI Command Tree

**Version:** 1.3.18-stable
**Binary:** /opt/homebrew/bin/acli
**Description:** Work seamlessly with Atlassian from the command line.

```
acli [command]
├── -h, --help      # Show help for command
├── -v, --version   # Display version (1.3.18-stable)
```

---

## acli auth

> Authenticate globally with OAuth across all Atlassian products.

```
acli auth
├── login       # Authenticate globally with OAuth (opens browser)
│   └── (no flags)
│
├── logout      # Logout globally from all active OAuth accounts
│   └── (no flags)
│
├── status      # Show global account status (site, email, auth type)
│   └── (no flags)
│
└── switch      # Switch globally between accounts for all products
    ├── -s, --site <string>    # Atlassian account site (e.g. mysite.atlassian.net)
    └── -e, --email <string>   # Atlassian account email
```

---

## acli admin

> Organization-level admin commands for user management.

### acli admin auth

> Authenticate for organization admin-specific tasks (requires API key).

```
acli admin auth
├── login       # Authenticate for admin tasks using API key
│   ├── -e, --email <string>   # Admin email (required)
│   └── --token                # Read API key from stdin (create at admin.atlassian.com → Settings → API Keys)
│
├── logout      # Remove admin authentication
│   └── (no flags)
│
├── status      # Show admin account status
│   └── (no flags)
│
└── switch      # Switch between organization admin accounts
    └── -o, --org <string>   # Org name to switch to
```

### acli admin user

> Manage users in the Atlassian organization.

```
acli admin user
├── activate        # Activate one or more users
│   ├── -e, --email <string>       # Comma-separated emails to activate
│   ├── --id <string>              # Comma-separated Atlassian account IDs
│   ├── -f, --from-file <string>   # Read emails/IDs from file
│   ├── --ignore-errors            # Continue on errors
│   └── --json                     # Output in JSON
│
├── deactivate      # Deactivate one or more users
│   ├── -e, --email <string>       # Comma-separated emails to deactivate
│   ├── --id <string>              # Comma-separated Atlassian account IDs
│   ├── -f, --from-file <string>   # Read emails/IDs from file
│   ├── --ignore-errors            # Continue on errors
│   └── --json                     # Output in JSON
│
├── delete          # Permanently delete a managed account
│   ├── --email <string>           # Emails to delete
│   ├── --id <string>              # Atlassian account IDs to delete
│   ├── --from-file <string>       # Read emails/IDs from file
│   ├── --ignore-errors            # Continue on errors
│   └── --json                     # Output in JSON
│
└── cancel-delete   # Cancel pending deletion of a managed account
    ├── --email <string>           # Emails to cancel deletion
    ├── --id <string>              # Account IDs to cancel deletion
    ├── --from-file <string>       # Read emails/IDs from file
    ├── --ignore-errors            # Continue on errors
    └── --json                     # Output in JSON
```

---

## acli jira

> Jira Cloud commands for managing projects, boards, sprints, and work items.

### acli jira auth

> Authenticate with Jira Cloud.

```
acli jira auth
├── login       # Authenticate with Jira host
│   ├── -w, --web              # Authenticate via web browser (OAuth)
│   ├── -s, --site <string>    # Atlassian site (e.g. mysite.atlassian.net)
│   ├── -e, --email <string>   # User email
│   └── --token                # Read API token from stdin
│
├── logout      # Logout from Jira account
│   └── (no flags)
│
├── status      # Show Jira account status
│   └── (no flags)
│
└── switch      # Switch between Jira accounts
    ├── -s, --site <string>    # Site to switch to
    └── -e, --email <string>   # Email to switch to
```

### acli jira board

> Manage Jira boards (scrum, kanban).

```
acli jira board
├── create          # Create a new Jira board
│   ├── --name <string>            # Board name (< 255 chars)
│   ├── --type <string>            # Board type: scrum, kanban
│   ├── --filter-id <int>          # Filter ID the board is based on
│   ├── --location-type <string>   # Container type: project, user
│   ├── --project <string>         # Project key/ID (required if location-type=project)
│   └── --json                     # Output in JSON
│
├── delete          # Delete one or more boards
│   ├── --id <string>   # Comma-separated board IDs (required)
│   └── --yes           # Skip confirmation prompt
│
├── get             # Get board details by ID
│   ├── --id <string>   # Board ID
│   └── --json          # Output in JSON
│
├── list-projects   # List all projects associated with a board
│   ├── --id <string>   # Board ID (required)
│   ├── --limit <int>   # Max results per page (default 50)
│   ├── --paginate      # Fetch all results
│   ├── --json          # Output in JSON
│   └── --csv           # Output in CSV
│
├── list-sprints    # List all sprints on a board
│   ├── --id <string>      # Board ID (required)
│   ├── --state <string>   # Filter: future, active, closed (comma-separated)
│   ├── --limit <int>      # Max results (default 50)
│   ├── --paginate         # Fetch all results
│   ├── --json             # Output in JSON
│   └── --csv              # Output in CSV
│
└── search          # Search through all boards
    ├── --name <string>       # Partial name match filter
    ├── --type <string>       # Filter: scrum, kanban, simple
    ├── --project <string>    # Filter by project key
    ├── --filter <string>     # Filter by filter ID
    ├── --order-by <string>   # Sort: name, -name, +name
    ├── --limit <int>         # Max results (default 50)
    ├── --paginate            # Fetch all results
    ├── --private             # Include private boards
    ├── --json                # Output in JSON
    └── --csv                 # Output in CSV
```

### acli jira dashboard

> Search Jira dashboards.

```
acli jira dashboard
└── search      # Search for Jira dashboards
    ├── -n, --name <string>    # Case-insensitive partial name match
    ├── -e, --owner <string>   # Filter by owner email
    ├── -l, --limit <int>      # Max results (default 30)
    ├── --paginate             # Fetch all results
    ├── --json                 # Output in JSON
    └── --csv                  # Output in CSV
```

### acli jira field

> Manage Jira custom fields.

```
acli jira field
├── create          # Create a custom field
│   ├── --name <string>           # Field name
│   ├── --type <string>           # Field type (plugin type key)
│   ├── --description <string>    # Field description
│   ├── --searcher-key <string>   # Searcher key for the field
│   └── --json                    # Output in JSON
│
├── delete          # Move a custom field to trash
│   └── --id <string>   # Custom field ID (e.g. customfield_12345)
│
├── cancel-delete   # Restore a field from trash
│   └── --id <string>   # Custom field ID to restore
│
└── update          # Update a custom field
    ├── --id <string>             # Field ID to update (required)
    ├── --name <string>           # New field name
    ├── --description <string>    # New description
    ├── --searcher-key <string>   # New searcher key
    ├── --from-json <string>      # Read update payload from JSON file
    └── --json                    # Output in JSON
```

### acli jira filter

> Manage Jira saved filters (JQL queries).

```
acli jira filter
├── add-favourite   # Add a filter as favourite
│   └── --filter-id <string>   # Filter ID
│
├── change-owner    # Change ownership of filters
│   ├── --id <string>              # Comma-separated filter IDs
│   ├── --owner <string>           # New owner email
│   ├── -f, --from-file <string>   # Read filter IDs from file
│   ├── --ignore-errors            # Continue on errors
│   └── --json                     # Output in JSON
│
├── get             # Retrieve a filter by ID
│   ├── --id <string>   # Filter ID
│   ├── --json          # Output in JSON
│   └── --web           # Open in browser
│
├── get-columns     # Get configured columns for a filter
│   ├── --key <string>   # Filter ID/key
│   └── --json           # Output in JSON
│
├── list            # List your own or favourite filters
│   ├── --my          # List my filters
│   ├── --favourite   # List favourite filters
│   └── --json        # Output in JSON
│
├── reset-columns   # Reset configured columns to defaults
│   └── --id <string>   # Filter ID
│
├── search          # Search for filters across the instance
│   ├── -n, --name <string>    # Partial name match
│   ├── -e, --owner <string>   # Owner email filter
│   ├── -l, --limit <int>      # Max results (default 30)
│   ├── --paginate             # Fetch all results
│   ├── --json                 # Output in JSON
│   └── --csv                  # Output in CSV
│
└── update          # Update an existing filter
    ├── --id <string>                  # Filter ID (required)
    ├── --name <string>                # New name
    ├── --description <string>         # New description
    ├── --jql <string>                 # New JQL query
    ├── --share-permissions <string>   # JSON array of SharePermission objects
    ├── --edit-permissions <string>    # JSON array of edit permission objects
    └── --json                         # Output in JSON
```

### acli jira project

> Manage Jira projects (collections of work items).

```
acli jira project
├── create      # Create a Jira project (from existing project or JSON)
│   ├── -f, --from-project <string>   # Clone from existing project key
│   ├── -k, --key <string>            # New project key
│   ├── -n, --name <string>           # Project name
│   ├── -d, --description <string>    # Project description
│   ├── -u, --url <string>            # Project URL
│   ├── -l, --lead-email <string>     # Lead user email
│   ├── -j, --from-json <string>      # Read project from JSON file
│   └── -g, --generate-json           # Generate template JSON file
│
├── delete      # Delete a project permanently
│   └── --key <string>   # Project key
│
├── list        # List visible projects
│   ├── -l, --limit <int>   # Max results (default 30)
│   ├── --paginate          # Fetch all results
│   ├── --recent            # Show up to 20 recently viewed
│   └── --json              # Output in JSON
│
├── update      # Update project details
│   ├── -p, --project-key <string>   # Current project key (required)
│   ├── -k, --key <string>           # New project key
│   ├── -n, --name <string>          # New name
│   ├── -d, --description <string>   # New description
│   ├── -u, --url <string>           # New URL
│   ├── -l, --lead-email <string>    # New lead email
│   ├── -j, --from-json <string>     # Read from JSON file
│   └── -g, --generate-json          # Generate template JSON
│
├── view        # Fetch project details
│   ├── --key <string>   # Project key
│   └── -j, --json       # Output in JSON
│
├── archive     # Archive a project (hides without deleting)
│   └── --key <string>   # Project key
│
└── restore     # Restore an archived/deleted project
    └── --key <string>   # Project key
```

### acli jira sprint

> Manage Jira sprints.

```
acli jira sprint
├── create          # Create a new sprint on a board
│   ├── --name <string>    # Sprint name (required)
│   ├── --board <int>      # Origin board ID (required)
│   ├── --start <string>   # Start date (ISO 8601)
│   ├── --end <string>     # End date (ISO 8601)
│   ├── --goal <string>    # Sprint goal text
│   └── --json             # Output in JSON
│
├── delete          # Delete one or more sprints
│   ├── --id <string>   # Comma-separated sprint IDs (required)
│   └── --yes           # Skip confirmation prompt
│
├── list-workitems  # List work items in a sprint
│   ├── --sprint <int>      # Sprint ID (required)
│   ├── --board <int>       # Board ID (required)
│   ├── --fields <string>   # Comma-separated fields (default: key,issuetype,summary,assignee,priority,status)
│   ├── --jql <string>      # JQL to filter within sprint
│   ├── --limit <int>       # Max results per page (default 50)
│   ├── --paginate          # Fetch all pages
│   ├── --json              # Output in JSON
│   └── --csv               # Output in CSV
│
├── update          # Update sprint details
│   ├── --id <string>               # Sprint ID (required)
│   ├── --name <string>             # New sprint name
│   ├── --goal <string>             # New goal text
│   ├── --state <string>            # New state: future, active, closed
│   ├── --start <string>            # New start date (ISO 8601)
│   ├── --end <string>              # New end date (ISO 8601)
│   ├── --complete-date <string>    # Completion date (ISO 8601)
│   ├── --board <int>               # Board ID
│   └── --json                      # Output in JSON
│
└── view            # View sprint details
    ├── --id <string>   # Sprint ID (required)
    └── --json          # Output in JSON
```

### acli jira workitem

> Manage Jira work items (issues: epics, stories, tasks, bugs).

#### acli jira workitem create

> Create a Jira work item to track individual pieces of work.

```
acli jira workitem create
├── -s, --summary <string>            # Work item summary/title
├── -p, --project <string>            # Project key
├── -t, --type <string>               # Type: Epic, Story, Task, Bug
├── -a, --assignee <string>           # Assignee email, '@me', or 'default'
├── -d, --description <string>        # Description (plain text or ADF)
├── --description-file <string>       # Read description from file
├── -l, --label <strings>             # Comma-separated labels
├── --parent <string>                 # Parent work item ID
├── -e, --editor                      # Open text editor for summary/description
├── -f, --from-file <string>          # Read summary/description from file
├── --from-json <string>              # Read full definition from JSON file
├── --generate-json                   # Generate template JSON file
└── --json                            # Output in JSON
```

#### acli jira workitem create-bulk

> Bulk create Jira issues from CSV or JSON files.

```
acli jira workitem create-bulk
├── --from-json <string>     # Read issues from JSON array file
├── --from-csv <string>      # Read issues from CSV (columns: summary, projectKey, issueType, description, label, parentIssueId, assignee)
├── --generate-json          # Print example JSON structure
├── --ignore-errors          # Continue on errors
└── --yes                    # Skip confirmation prompt
```

#### acli jira workitem edit

> Edit one or more existing work items.

```
acli jira workitem edit
├── -k, --key <string>                # Comma-separated work item keys
├── --jql <string>                    # JQL query to select items to edit
├── --filter <string>                 # Filter ID to select items
├── -s, --summary <string>            # New summary
├── -d, --description <string>        # New description (plain text or ADF)
├── --description-file <string>       # Read description from file
├── -a, --assignee <string>           # New assignee (email, '@me', 'default')
├── --remove-assignee                 # Remove the assignee
├── -t, --type <string>               # Change work item type
├── -l, --labels <string>             # Set labels
├── --remove-labels <string>          # Remove specified labels
├── --from-json <string>              # Read definition from JSON
├── --generate-json                   # Generate template JSON
├── --ignore-errors                   # Continue on errors
├── -y, --yes                         # Skip confirmation
└── --json                            # Output in JSON
```

#### acli jira workitem search

> Search for work items using JQL or saved filters.

```
acli jira workitem search
├── -j, --jql <string>      # JQL query string
├── --filter <string>       # Saved filter ID
├── -f, --fields <string>   # Comma-separated fields (default: issuetype,key,assignee,priority,status,summary)
├── -l, --limit <int>       # Max results to fetch
├── --paginate              # Fetch all results via pagination
├── --count                 # Return count only
├── -w, --web               # Open search in browser
├── --json                  # Output in JSON
└── --csv                   # Output in CSV
```

#### acli jira workitem view

> Retrieve detailed information about a work item.

```
acli jira workitem view [key]
├── -f, --fields <string>   # Fields to return (default: key,issuetype,summary,status,assignee,description)
│                            #   '*all' = all fields, '*navigable' = navigable fields
│                            #   prefix with '-' to exclude (e.g. '-description')
├── -w, --web               # Open in browser
└── --json                  # Output in JSON
```

#### acli jira workitem assign

> Assign work items to users.

```
acli jira workitem assign
├── -k, --key <string>         # Comma-separated work item keys
├── --jql <string>             # JQL query to select items
├── --filter <string>          # Filter ID to select items
├── -f, --from-file <string>   # Read keys from file
├── -a, --assignee <string>    # Assignee (email, '@me', 'default')
├── --remove-assignee          # Remove assignee instead
├── --ignore-errors            # Continue on errors
├── -y, --yes                  # Skip confirmation
└── --json                     # Output in JSON
```

#### acli jira workitem clone

> Create duplicate work items (copies summary, description, etc).

```
acli jira workitem clone
├── -k, --key <string>          # Comma-separated work item keys to clone
├── --jql <string>              # JQL to select items
├── --filter <string>           # Filter ID to select items
├── -f, --from-file <string>    # Read keys from file
├── --to-project <string>       # Target project key for clones
├── --to-site <string>          # Target site (default: current site)
├── --ignore-errors             # Continue on errors
├── -y, --yes                   # Skip confirmation
└── --json                      # Output in JSON
```

#### acli jira workitem delete

> Delete one or more work items permanently.

```
acli jira workitem delete
├── -k, --key <string>         # Comma-separated work item keys
├── --jql <string>             # JQL to select items
├── --filter <string>          # Filter ID to select items
├── -f, --from-file <string>   # Read keys from file
├── --ignore-errors            # Continue on errors
├── -y, --yes                  # Skip confirmation
└── --json                     # Output in JSON
```

#### acli jira workitem archive

> Archive work items (removes from project without deleting; restorable).

```
acli jira workitem archive
├── -k, --key <string>         # Comma-separated keys
├── --jql <string>             # JQL to select items
├── --filter <string>          # Filter ID
├── -f, --from-file <string>   # Read keys from file
├── --ignore-errors            # Continue on errors
├── -y, --yes                  # Skip confirmation
└── --json                     # Output in JSON
```

#### acli jira workitem unarchive

> Restore archived work items.

```
acli jira workitem unarchive
├── -k, --key <string>         # Comma-separated keys
├── -f, --from-file <string>   # Read keys from file
├── --ignore-errors            # Continue on errors
├── -y, --yes                  # Skip confirmation
└── --json                     # Output in JSON
```

#### acli jira workitem transition

> Move work items to a different workflow status.

```
acli jira workitem transition
├── -k, --key <string>      # Comma-separated keys
├── --jql <string>          # JQL to select items
├── --filter <string>       # Filter ID
├── -s, --status <string>   # Target status (e.g. "Done", "In Progress", "To Do")
├── --ignore-errors         # Continue on errors
├── -y, --yes               # Skip confirmation
└── --json                  # Output in JSON
```

#### acli jira workitem link

> Manage links between work items.

```
acli jira workitem link
├── create      # Create links between work items
│   ├── --out <string>           # Outward work item ID
│   ├── --in <string>            # Inward work item ID
│   ├── --type <string>          # Link type (outward description, e.g. "Blocks")
│   ├── --from-json <string>     # Read mappings from JSON
│   ├── --from-csv <string>      # Read from CSV (outward, inward, type columns)
│   ├── --generate-json          # Print example JSON structure
│   ├── --ignore-errors          # Continue on errors
│   └── --yes                    # Skip confirmation
│
├── delete      # Delete links between work items
│   ├── --id <string>            # Link IDs to delete
│   ├── --from-json <string>     # Read link IDs from JSON
│   ├── --from-csv <string>      # Read link IDs from CSV
│   ├── --ignore-errors          # Continue on errors
│   └── --yes                    # Skip confirmation
│
├── list        # List all links of a work item
│   ├── --key <string>   # Work item key
│   └── --json           # Output in JSON
│
└── type        # Get available link types for the instance
    └── --json   # Output in JSON
```

#### acli jira workitem watcher

> Manage work item watchers.

```
acli jira workitem watcher
├── list        # List watchers of an issue
│   ├── --key <string>   # Issue key
│   └── --json           # Output in JSON
│
└── remove      # Remove a watcher from an issue
    ├── --key <string>    # Issue key
    └── --user <string>   # Account ID of user to remove
```

#### acli jira workitem comment

> Manage comments on work items.

```
acli jira workitem comment
├── create      # Add a comment to one or more work items
│   ├── -k, --key <string>        # Work item keys
│   ├── --jql <string>            # JQL to select items
│   ├── --filter <string>         # Filter ID
│   ├── -b, --body <string>       # Comment body (plain text or ADF)
│   ├── -F, --body-file <string>  # Read body from file
│   ├── -e, --edit-last           # Edit last comment from same author instead
│   ├── --editor                  # Open text editor for body
│   ├── --ignore-errors           # Continue on errors
│   └── --json                    # Output in JSON
│
├── delete      # Delete a specific comment
│   ├── --key <string>   # Work item key
│   └── --id <string>    # Comment ID
│
├── list        # List comments on a work item
│   ├── --key <string>      # Work item key
│   ├── --limit <int>       # Max per page (default 50)
│   ├── --order <string>    # Sort: +created, -created, +updated, -updated (default "+created")
│   ├── --paginate          # Fetch all pages
│   └── --json              # Output in JSON
│
├── update      # Update an existing comment
│   ├── --key <string>                # Work item key
│   ├── --id <string>                 # Comment ID
│   ├── -b, --body <string>           # New body text
│   ├── -F, --body-file <string>      # Read body from file
│   ├── --body-adf <string>           # Body in ADF format (JSON file)
│   ├── --visibility-role <string>    # Restrict to role (e.g. "Administrators")
│   ├── --visibility-group <string>   # Restrict to group (e.g. "dev-team")
│   └── --notify                      # Notify users about change
│
└── visibility  # Get available visibility options for comments
    ├── --role                 # Get project roles for visibility
    ├── --group                # List available groups
    └── --project <string>     # Project key (required with --role)
```

#### acli jira workitem attachment

> Manage work item attachments.

```
acli jira workitem attachment
├── list        # List all attachments of a work item
│   ├── --key <string>   # Work item key
│   └── --json           # Output in JSON
│
└── delete      # Delete an attachment by ID
    └── --id <string>   # Attachment ID
```

---

## acli confluence

> Confluence Cloud commands for managing spaces, pages, and blog posts.

### acli confluence auth

> Authenticate with Confluence Cloud.

```
acli confluence auth
├── login       # Authenticate with Confluence
│   ├── -w, --web              # Authenticate via browser (OAuth)
│   ├── -s, --site <string>    # Atlassian site
│   ├── -e, --email <string>   # User email
│   └── --token                # Read API token from stdin
│
├── logout      # Logout from Confluence
│   └── (no flags)
│
├── status      # Show Confluence account status
│   └── (no flags)
│
└── switch      # Switch between Confluence accounts
    ├── -s, --site <string>    # Site to switch to
    └── -e, --email <string>   # Email to switch to
```

### acli confluence blog

> Manage Confluence blog posts.

```
acli confluence blog
├── create      # Create a new blog post
│   ├── --space-id <string>      # Space ID (required)
│   ├── --title <string>         # Blog post title
│   ├── --body <string>          # Content in Confluence storage format (XHTML)
│   ├── --from-file <string>     # Read content from file (text or HTML)
│   ├── --from-json <string>     # Read full payload from JSON file
│   ├── --generate-json          # Generate example JSON structure
│   ├── --status <string>        # Status: current (published) or draft (default: current)
│   ├── --private                # Create as private blog post
│   ├── --created-at <string>    # Custom creation timestamp (ISO 8601)
│   └── -j, --json               # Output in JSON
│
├── list        # List blog posts with filtering
│   ├── --space-id <string>      # Filter by space ID(s) (comma-separated)
│   ├── --id <string>            # Filter by blog post IDs (comma-separated)
│   ├── --title <string>         # Filter by title
│   ├── --status <string>        # Filter: current, deleted, trashed (comma-separated)
│   ├── --body-format <string>   # Body format: storage, atlas_doc_format
│   ├── --sort <string>          # Sort order
│   ├── --cursor <string>        # Pagination cursor for next page
│   ├── -l, --limit <int>        # Max results (default 25)
│   ├── -j, --json               # Output in JSON
│   └── --csv                    # Output in CSV
│
└── view        # View details of a specific blog post
    ├── --id <string>            # Blog post ID (required)
    ├── --body-format <string>   # Body format: view, storage, atlas_doc_format (default: view)
    ├── --version <int>          # Retrieve specific version
    ├── --draft                  # Retrieve draft version
    ├── --status <string>        # Filter: current, trashed, deleted, historical, draft
    ├── --include <string>       # Include extra data: labels, properties, operations, likes, versions, version, favorited, webresources, collaborators, all
    └── -j, --json               # Output in JSON
```

### acli confluence page

> View Confluence pages (read-only).

```
acli confluence page
└── view        # View page details
    ├── --id <string>                                  # Page ID (required)
    ├── --body-format <string>                         # Body format: storage, atlas_doc_format, view
    ├── --version <int>                                # Specific version number
    ├── --get-draft                                    # Retrieve draft version
    ├── --status <string>                              # Filter: current, draft, archived (comma-separated)
    ├── --include-labels                               # Include page labels
    ├── --include-likes                                # Include likes/reactions
    ├── --include-collaborators                        # Include collaborator info
    ├── --include-version                              # Include detailed version object
    ├── --include-versions                             # Include versions list
    ├── --include-operations                           # Include allowed operations
    ├── --include-properties                           # Include content properties
    ├── --include-direct-children                      # Include direct child pages
    ├── --include-webresources                         # Include webresource metadata
    ├── --include-favorited-by-current-user-status     # Include favorite status
    └── --json                                         # Output in JSON
```

### acli confluence space

> Manage Confluence spaces.

```
acli confluence space
├── create      # Create a new Confluence space
│   ├── --key <string>             # Space key (required)
│   ├── --name <string>            # Space name (required)
│   ├── --description <string>     # Space description
│   ├── --alias <string>           # URL-friendly identifier
│   ├── --template-key <string>    # Template to use
│   ├── --private                  # Create as private space
│   └── --json                     # Output in JSON
│
├── list        # List Confluence spaces
│   ├── --type <string>      # Filter: global, personal
│   ├── --status <string>    # Filter: current, archived (default: current)
│   ├── --keys <string>      # Filter by comma-separated space keys
│   ├── --expand <string>    # Expand: description, homepage, permissions
│   ├── -l, --limit <int>    # Max results (default 50)
│   └── --json               # Output in JSON
│
├── view        # View space details
│   ├── --id <string>            # Space ID (required)
│   ├── --desc-format <string>   # Description format: plain, view
│   ├── --icon                   # Include space icon
│   ├── --labels                 # Include space labels
│   ├── --operations             # Include operations
│   ├── --permissions            # Include permissions
│   ├── --properties             # Include space properties
│   ├── --role-assignments       # Include role assignments (EAP only)
│   ├── --include-all            # Include all of the above
│   └── --json                   # Output in JSON
│
├── update      # Update space details
│   ├── --key <string>            # Space key (required)
│   ├── --name <string>           # New name
│   ├── --description <string>    # New description
│   ├── --status <string>         # New status
│   ├── --type <string>           # New type
│   └── --json                    # Output in JSON
│
├── archive     # Archive a space
│   ├── --key <string>   # Space key (required)
│   └── --json           # Output in JSON
│
└── restore     # Restore a space from trash/archive
    ├── --key <string>   # Space key (required)
    └── --json           # Output in JSON
```

---

## acli rovodev

> Atlassian's AI coding agent: Rovo Dev (Beta). Requires a separate scoped API token.

```
acli rovodev
├── auth
│   └── login   # Authenticate for Rovo Dev tasks
│       ├── -e, --email <string>   # User email (required)
│       └── --token                # Read scoped API token from stdin
│                                  # (create at: https://go.atlassian.com/rovo-dev-api-token)
│
└── run         # Start a Rovo Dev coding agent session
    └── (requires auth; details unavailable without authentication)
```

---

## acli config

> Configuration settings.

```
acli config
└── gov-cloud   # Toggle Atlassian Government Cloud environment
    ├── --enable    # Enable GovCloud (default: true when flag present)
    ├── --status    # Display current GovCloud status
    └── -h, --help
```

---

## acli completion

> Generate shell autocompletion scripts.

```
acli completion [bash|zsh|fish|powershell]
```

---

## acli feedback

> Submit a request or report a problem to the acli team.

---

## Global Flags (available on all commands)

```
-h, --help      # Show help for any command
-v, --version   # Show acli version
```

---

## Limitations

1. **Confluence pages are read-only** — no create, edit, or delete for pages (only view)
2. **No Bitbucket integration** — despite being an Atlassian tool
3. **No Jira filter creation** — can only update existing filters
4. **Dashboard management is search-only** — no create/edit/delete
5. **No attachment upload** — can only list and delete existing attachments
6. **No watcher add** — can only list and remove watchers
7. **Rovo Dev is Beta** — requires separate token, limited docs
8. **No export/import** — no bulk export to CSV/JSON (search --csv is output-only, not round-trippable)
9. **No webhook/automation management**
10. **No offline mode** — all commands require network access
11. **Interactive auth required** — initial OAuth login requires a browser
12. **No man page** — documentation only via `--help` flags
