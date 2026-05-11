# OpenStack WebUI

Interact with the OpenStack Horizon dashboard via Playwright browser automation.

## What It Does

Performs cloud infrastructure tasks through the Horizon web interface:

- Instance management (launch, stop, start, delete)
- Networking (networks, routers, floating IPs, security groups)
- Volume management (create, attach, detach, snapshot)
- Image and key pair management

## Requirements

- `playwright@claude-plugins-official` plugin installed and enabled
- Access to an OpenStack Horizon dashboard
- Claude Code with skill support

## Installation

```bash
/plugins marketplace add sachchidanandx/ClaudeSkills
/plugins install openstack-webui@sachchidanand-skills
```

## Usage

Ask to perform OpenStack tasks:

- "List my instances in OpenStack"
- "Launch a new instance with flavor m1.small"
- "Create a security group for web traffic"
- "Attach a volume to my server"

The skill will ask for your Horizon URL and handle authentication (including SSO) before performing any operations.
