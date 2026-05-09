---
name: openstack-webui
description: Use this skill whenever the user asks about OpenStack, Horizon dashboard, managing cloud instances, creating VMs, configuring networking, managing security groups, attaching volumes, launching instances, or any request involving interaction with the OpenStack Horizon web UI. This includes questions like "open my OpenStack dashboard", "launch an instance in OpenStack", "manage security groups", "create a network in OpenStack", "list my instances", "attach a volume", or "configure OpenStack". Always use this skill when the user mentions OpenStack, Horizon, or asks to perform cloud infrastructure tasks through the OpenStack web interface.
allowed-tools:
  - mcp__plugin_playwright_playwright__browser_navigate
  - mcp__plugin_playwright_playwright__browser_click
  - mcp__plugin_playwright_playwright__browser_snapshot
  - mcp__plugin_playwright_playwright__browser_fill_form
  - mcp__plugin_playwright_playwright__browser_select_option
  - mcp__plugin_playwright_playwright__browser_type
  - mcp__plugin_playwright_playwright__browser_press_key
  - mcp__plugin_playwright_playwright__browser_wait_for
  - mcp__plugin_playwright_playwright__browser_take_screenshot
  - mcp__plugin_playwright_playwright__browser_tabs
  - mcp__plugin_playwright_playwright__browser_hover
  - mcp__plugin_playwright_playwright__browser_close
  - mcp__plugin_playwright_playwright__browser_navigate_back
  - mcp__plugin_playwright_playwright__browser_evaluate
---

# OpenStack WebUI

Interact with the OpenStack Horizon dashboard via Playwright browser automation. Perform cloud infrastructure tasks including instance management, networking, volumes, security groups, and project configuration through the web interface.

## Core Principle

Plan before acting. Before performing any destructive or multi-step action, outline the steps to the user and request explicit confirmation. Never create, delete, or modify resources without user approval.

## Prerequisites

The `playwright@claude-plugins-official` plugin must be installed and enabled in Claude Code settings.

## Workflow

### 1. Obtain the OpenStack URL

Ask the user for their OpenStack Horizon dashboard URL before any browser interaction. Example: "What is the URL of your OpenStack Horizon dashboard?"

### 2. Navigate and Handle Authentication

Navigate to the provided URL using `browser_navigate`. Take a snapshot to assess the page state.

**If SSO/Okta login is detected:**

1. Inform the user that SSO authentication is required.
2. Ask the user to complete authentication manually in the browser window.
3. Instruct: "Please complete the SSO login in the browser. Let me know once you are logged in."
4. After user confirmation, take a snapshot to verify successful login.
5. If still on a login page, ask the user to try again.

**If Keystone login is detected:**

1. Inform the user that OpenStack login is required.
2. Ask the user to complete authentication manually in the browser window.
3. After user confirmation, take a snapshot to verify successful login.

### 3. Verify Project Context

After successful login:

1. Take a snapshot to identify the current project/domain context.
2. If multiple projects are available, ask the user to select the correct project.
3. If the wrong project is selected, navigate to the project switcher and help the user switch.

### 4. Plan Before Acting

For any task beyond simple navigation or viewing:

1. State what actions will be performed.
2. List the specific steps (e.g., "I will navigate to Compute > Instances, click Launch Instance, fill in the form with...").
3. Wait for explicit user confirmation before proceeding.
4. Execute the steps sequentially, verifying each step with `browser_snapshot`.

### 5. Execute and Verify

After each action:

- Take a snapshot to confirm the expected result.
- Report success or failure clearly.
- If an error toast or message appears, capture it and inform the user.

## Supported Operations

### Compute (Instances)

- **List instances**: Navigate to Project > Compute > Instances. Snapshot the table.
- **Launch instance**: Use the Launch Instance wizard (name, source, flavor, network, security groups, key pair).
- **Instance actions**: Start, stop, pause, resume, reboot, rebuild, resize, delete.
- **Console access**: Open the console tab for an instance.
- **View instance details**: Click an instance name to view its overview, interfaces, log, and console.

### Networking

- **List networks**: Navigate to Project > Network > Networks.
- **Create network**: Use the Create Network dialog (name, subnet, DHCP settings).
- **Manage routers**: Create, delete, set gateway, add interface.
- **Floating IPs**: Allocate, associate, disassociate, release.
- **Security groups**: Create groups, add/remove rules (ingress/egress, protocol, port, CIDR).

### Volumes (Block Storage)

- **List volumes**: Navigate to Project > Volumes > Volumes.
- **Create volume**: Specify name, size, type, source.
- **Attach/Detach**: Attach a volume to an instance or detach it.
- **Create snapshot**: Snapshot a volume.
- **Delete volume**: With confirmation.

### Images

- **List images**: Navigate to Project > Compute > Images.
- **Launch from image**: Select an image and launch as instance.
- **View image details**: Click to view metadata and properties.

### Key Pairs

- **List key pairs**: Navigate to Project > Compute > Key Pairs.
- **Create/Import**: Create a new key pair or import a public key.

### Identity (if admin)

- **Projects**: List, create, edit projects.
- **Users**: List, create, edit users and role assignments.

## Horizon Navigation Reference

OpenStack Horizon organizes content in a sidebar menu:

```
Project
├── Compute
│   ├── Overview
│   ├── Instances
│   ├── Images
│   └── Key Pairs
├── Volumes
│   ├── Volumes
│   ├── Backups
│   └── Snapshots
├── Network
│   ├── Networks
│   ├── Routers
│   ├── Security Groups
│   ├── Floating IPs
│   └── Network Topology
└── Orchestration
    ├── Stacks
    └── Template Versions

Admin (if authorized)
├── Compute
│   ├── Hypervisors
│   ├── Host Aggregates
│   ├── Instances
│   ├── Flavors
│   └── Images
├── Volume
│   ├── Volumes
│   └── Volume Types
├── Network
│   ├── Networks
│   ├── Routers
│   └── Floating IPs
└── Identity
    ├── Projects
    ├── Users
    └── Roles
```

## Browser Interaction Patterns

### Navigation

To navigate to a section, use sidebar links. Take a snapshot first to identify the exact element references, then click the appropriate menu item.

1. `browser_snapshot` — identify sidebar elements
2. `browser_click` — click the menu section (e.g., "Compute")
3. `browser_click` — click the submenu item (e.g., "Instances")
4. `browser_snapshot` — verify the page loaded

### Form Filling (Launch Instance Wizard)

The Launch Instance wizard is a multi-step modal:

1. Details (name, description, availability zone, count)
2. Source (boot source, image/volume selection)
3. Flavor (select compute flavor)
4. Networks (select networks)
5. Security Groups (select security groups)
6. Key Pair (select or create)

Navigate through tabs sequentially, filling each section and clicking "Next" or selecting the next tab.

### Table Interactions

Tables in Horizon support:

- Row selection via checkboxes
- Action buttons (per-row dropdown or top-of-table buttons)
- Pagination
- Search/filter

To perform an action on a specific resource, identify the row by name, then use the action dropdown.

### Waiting for Operations

After triggering long-running operations (instance launch, volume create):

- Use `browser_wait_for` to wait for status changes.
- Or periodically snapshot the page to check status.

## Error Handling

- If navigation fails, verify the URL and authentication state.
- If a form submission produces an error, capture the error message via snapshot and report it.
- If a page element cannot be found, take a fresh snapshot to reassess the page structure.
- If the session expires, inform the user and request re-authentication.

## Tips

- Always use `browser_snapshot` (accessibility tree) rather than `browser_take_screenshot` for identifying clickable elements. Screenshots are useful for visual confirmation to the user.
- Horizon uses Angular or Django templates; element references from snapshots are the most reliable way to target elements.
- Multi-step wizards require completing each tab before proceeding.
- Some actions require confirming a modal dialog. Always check for confirmation modals after clicking destructive actions.
- Project and domain dropdowns at the top of Horizon control context. Verify the correct project is selected before performing operations.
- When searching for a resource in a table, use the search/filter input at the top of the table rather than scrolling through pages.
