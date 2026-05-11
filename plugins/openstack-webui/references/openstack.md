# openstack - OpenStack CLI Command Tree

**Version:** openstack 9.0.0 (openstackclient 9.0.0)
**Binary:** /opt/homebrew/bin/openstack
**Description:** Unified command-line client for OpenStack cloud services.

**Installed Plugins:**

- barbicanclient 7.3.0 (Key Manager / Barbican)
- cinderclient 9.9.0 (Block Storage / Cinder)
- cloudkittyclient 6.1.0 (Rating / CloudKitty)
- designateclient 6.4.0 (DNS / Designate)
- heatclient 5.1.0 (Orchestration / Heat)
- ironicclient 6.0.0 (Baremetal / Ironic)
- keystoneclient 5.8.0 (Identity / Keystone)
- magnumclient 4.10.0 (Container Infrastructure / Magnum)
- manilaclient 6.0.0 (Shared File System / Manila)
- mistralclient 6.2.0 (Workflow / Mistral)
- octaviaclient 3.13.0 (Load Balancer / Octavia)
- swiftclient 4.10.0 (Object Storage / Swift)

```
openstack [command]
├── -h, --help         # Show help for command
├── --version          # Display version (9.0.0)
├── --debug            # Show debug logging
├── -v, --verbose      # Increase verbosity (repeat for more)
├── -q, --quiet        # Suppress output except warnings/errors
└── --timing           # Print API call timing info
```

---

## Authentication & Configuration

> Configure credentials via clouds.yaml, environment variables, or CLI flags.

### clouds.yaml

```
# Searched in order:
#   1. ./clouds.yaml (current directory)
#   2. ~/.config/openstack/clouds.yaml
#   3. /etc/openstack/clouds.yaml

clouds:
  mycloud:
    auth:
      auth_url: https://keystone.example.com:5000/v3
      username: admin
      password: secret
      project_name: admin
      user_domain_name: Default
      project_domain_name: Default
    region_name: RegionOne
    interface: public
```

### Environment Variables

```
OS_AUTH_URL             # Keystone endpoint URL
OS_USERNAME             # Username
OS_PASSWORD             # Password
OS_PROJECT_NAME         # Project/tenant name
OS_PROJECT_ID           # Project/tenant ID
OS_USER_DOMAIN_NAME     # User domain (default: Default)
OS_PROJECT_DOMAIN_NAME  # Project domain (default: Default)
OS_REGION_NAME          # Region name
OS_INTERFACE            # Interface: public, internal, admin
OS_IDENTITY_API_VERSION # Identity API version (default: 3)
OS_AUTH_TYPE            # Auth plugin type (e.g. password, token, v3applicationcredential)
OS_CACERT               # CA certificate bundle file path
OS_CERT                 # Client certificate file
OS_KEY                  # Client certificate key file
OS_CLOUD                # Named cloud from clouds.yaml
```

---

## openstack server

> Compute instances (Nova). Create, manage, and control virtual machines.

```
openstack server
├── create                                     # Create a new server
│   ├── <server-name>                          # (positional) New server name
│   ├── --flavor <flavor>                      # Flavor (name or ID) (required)
│   ├── --image <image>                        # Boot from image (name or ID)
│   ├── --image-property <key=value>           # Boot from image matching property
│   ├── --volume <volume>                      # Boot from volume (name or ID)
│   ├── --snapshot <snapshot>                  # Boot from snapshot (name or ID)
│   ├── --boot-from-volume <size-gb>           # Create boot volume from image
│   ├── --block-device <block-device>          # Block device mapping (JSON or CSV)
│   ├── --block-device-mapping <dev=mapping>   # (deprecated) Block device mapping
│   ├── --swap <size-mb>                       # Attach local swap device
│   ├── --ephemeral <size=N[,format=F]>        # Attach ephemeral disk
│   ├── --network <network>                    # Attach to network (repeat for multiple)
│   ├── --port <port>                          # Attach to port (repeat for multiple)
│   ├── --nic <net-id=N,port-id=P,...>         # Advanced NIC configuration
│   ├── --no-network                           # Do not attach any network
│   ├── --auto-network                         # Auto-allocate network (default)
│   ├── --security-group <group>               # Security group (repeat for multiple)
│   ├── --no-security-group                    # No security group on ports
│   ├── --key-name <key-name>                  # Keypair to inject
│   ├── --property <key=value>                 # Server metadata (repeat for multiple)
│   ├── --file <dest=source>                   # Inject file into image (repeat)
│   ├── --user-data <file>                     # User data file for metadata server
│   ├── --description <desc>                   # Server description (v2.19+)
│   ├── --availability-zone <zone>             # Availability zone
│   ├── --host <host>                          # Target host (admin, v2.74+)
│   ├── --hypervisor-hostname <name>           # Target hypervisor (admin, v2.74+)
│   ├── --server-group <group>                 # Server group
│   ├── --hint <key=value>                     # Scheduler hint (repeat)
│   ├── --use-config-drive                     # Enable config drive
│   ├── --no-config-drive                      # Disable config drive
│   ├── --min <count>                          # Minimum servers to launch (default 1)
│   ├── --max <count>                          # Maximum servers to launch (default 1)
│   ├── --tag <tag>                            # Server tag (repeat, v2.52+)
│   ├── --hostname <hostname>                  # Metadata hostname (v2.90+)
│   ├── --password <password>                  # Set server password
│   ├── --trusted-image-cert <cert-id>         # Trusted image cert (repeat, v2.63+)
│   └── --wait                                 # Wait for build to complete
│
├── list                                       # List servers
│   ├── --reservation-id <id>                  # Filter by reservation
│   ├── --ip <regex>                           # Filter by IP address regex
│   ├── --ip6 <regex>                          # Filter by IPv6 address regex
│   ├── --name <regex>                         # Filter by name regex
│   ├── --instance-name <regex>                # Filter by instance name (admin)
│   ├── --status <status>                      # Filter by status
│   ├── --flavor <flavor>                      # Filter by flavor (name or ID)
│   ├── --image <image>                        # Filter by image (name or ID)
│   ├── --host <hostname>                      # Filter by host
│   ├── --all-projects                         # Include all projects (admin)
│   ├── --project <project>                    # Filter by project (admin)
│   ├── --project-domain <domain>              # Project domain (name or ID)
│   ├── --user <user>                          # Filter by user (name or ID)
│   ├── --user-domain <domain>                 # User domain (name or ID)
│   ├── --deleted                              # Show deleted servers (admin)
│   ├── --availability-zone <zone>             # Filter by AZ
│   ├── --key-name <key>                       # Filter by keypair
│   ├── --config-drive                         # Only with config drive
│   ├── --no-config-drive                      # Only without config drive
│   ├── --progress <pct>                       # Filter by progress (admin)
│   ├── --vm-state <state>                     # Filter by VM state (admin)
│   ├── --task-state <state>                   # Filter by task state (admin)
│   ├── --power-state <state>                  # Filter by power state (admin)
│   ├── --long                                 # List additional fields
│   ├── -n, --no-name-lookup                   # Skip flavor/image name lookup
│   ├── --name-lookup-one-by-one               # Look up names individually
│   ├── --limit <limit>                        # Max entries to return
│   ├── --marker <marker>                      # Pagination marker
│   ├── --changes-before <time>                # Changed before (ISO 8601, v2.66+)
│   ├── --changes-since <time>                 # Changed after (ISO 8601)
│   ├── --locked                               # Only locked (v2.73+)
│   ├── --unlocked                             # Only unlocked (v2.73+)
│   ├── --tags <tag>                           # Filter by tag (repeat, v2.26+)
│   └── --not-tags <tag>                       # Exclude by tag (repeat, v2.26+)
│
├── show                                       # Show server details
│   ├── <server>                               # (positional) Server name or ID
│   ├── --diagnostics                          # Show diagnostics
│   └── --topology                             # Show topology (v2.78+)
│
├── delete                                     # Delete server(s)
│   ├── <server> [<server> ...]                # (positional) Server(s) name or ID
│   ├── --force                                # Force delete
│   ├── --all-projects                         # By name in other projects (admin)
│   └── --wait                                 # Wait for delete to complete
│
├── set                                        # Set server properties
│   ├── <server>                               # (positional) Server name or ID
│   ├── --name <new-name>                      # Rename server
│   ├── --password <password>                  # Set password
│   ├── --no-password                          # Clear admin password from metadata
│   ├── --property <key=value>                 # Set metadata (repeat)
│   ├── --state <state>                        # Override state (admin, WARNING)
│   ├── --auto-approve                         # Skip state override confirmation
│   ├── --description <desc>                   # New description (v2.19+)
│   ├── --tag <tag>                            # Add tag (repeat, v2.26+)
│   └── --hostname <hostname>                  # Set metadata hostname (v2.90+)
│
├── unset                                      # Unset server properties
│   ├── <server>                               # (positional) Server name or ID
│   ├── --property <key>                       # Remove metadata key (repeat)
│   ├── --description                          # Clear description (v2.19+)
│   └── --tag <tag>                            # Remove tag (repeat, v2.26+)
│
├── start                                      # Start server(s)
│   └── <server> [<server> ...]                # (positional) Server(s)
│
├── stop                                       # Stop server(s)
│   └── <server> [<server> ...]                # (positional) Server(s)
│
├── reboot                                     # Reboot server
│   ├── <server>                               # (positional) Server name or ID
│   ├── --hard                                 # Hard reboot
│   ├── --soft                                 # Soft reboot
│   └── --wait                                 # Wait for reboot to complete
│
├── pause                                      # Pause server (freeze in memory)
│   └── <server>                               # (positional) Server name or ID
│
├── unpause                                    # Unpause server
│   └── <server>                               # (positional) Server name or ID
│
├── suspend                                    # Suspend server (save to disk)
│   └── <server>                               # (positional) Server name or ID
│
├── resume                                     # Resume suspended server
│   └── <server>                               # (positional) Server name or ID
│
├── shelve                                     # Shelve server (snapshot + shutdown)
│   ├── <server>                               # (positional) Server name or ID
│   └── --wait                                 # Wait for shelve
│
├── unshelve                                   # Unshelve server
│   ├── <server>                               # (positional) Server name or ID
│   ├── --availability-zone <zone>             # Target AZ (v2.77+)
│   ├── --host <host>                          # Target host (v2.91+)
│   ├── --no-availability-zone                 # Unpin from AZ (v2.91+)
│   └── --wait                                 # Wait for unshelve
│
├── lock                                       # Lock server (prevent actions by non-admin)
│   ├── <server>                               # (positional) Server name or ID
│   └── --reason <reason>                      # Lock reason (v2.73+)
│
├── unlock                                     # Unlock server
│   └── <server>                               # (positional) Server name or ID
│
├── rescue                                     # Put server in rescue mode
│   ├── <server>                               # (positional) Server name or ID
│   ├── --image <image>                        # Rescue image
│   └── --password <password>                  # Rescue password
│
├── unrescue                                   # Exit rescue mode
│   └── <server>                               # (positional) Server name or ID
│
├── resize                                     # Resize server to new flavor
│   ├── <server>                               # (positional) Server name or ID
│   ├── --flavor <flavor>                      # Target flavor
│   ├── --confirm                              # (deprecated) Confirm resize
│   ├── --revert                               # (deprecated) Revert resize
│   └── --wait                                 # Wait for resize
│
├── resize confirm                             # Confirm resize is complete
│   └── <server>                               # (positional) Server name or ID
│
├── resize revert                              # Revert resize
│   └── <server>                               # (positional) Server name or ID
│
├── migrate                                    # Migrate server to different host
│   ├── <server>                               # (positional) Server name or ID
│   ├── --live-migration                       # Live migrate
│   ├── --host <hostname>                      # Target host (v2.30+ with live, v2.56+ cold)
│   ├── --shared-migration                     # Shared storage live migration
│   ├── --block-migration                      # Block live migration
│   ├── --disk-overcommit                      # Allow disk overcommit (v2.24-)
│   ├── --no-disk-overcommit                   # No disk overcommit (v2.24-)
│   └── --wait                                 # Wait for migration
│
├── migrate confirm                            # Confirm migration
│   └── <server>                               # (positional) Server name or ID
│
├── migrate revert                             # Revert migration
│   └── <server>                               # (positional) Server name or ID
│
├── rebuild                                    # Rebuild server from image
│   ├── <server>                               # (positional) Server name or ID
│   ├── --image <image>                        # New image (default: current)
│   ├── --name <name>                          # New name
│   ├── --password <password>                  # New password
│   ├── --property <key=value>                 # Set property (repeat)
│   ├── --description <desc>                   # New description (v2.19+)
│   ├── --preserve-ephemeral                   # Keep ephemeral disk
│   ├── --no-preserve-ephemeral                # Don't keep ephemeral disk
│   ├── --key-name <key>                       # New keypair (v2.54+)
│   ├── --no-key-name                          # Remove keypair (v2.54+)
│   ├── --user-data <file>                     # New user data (v2.57+)
│   ├── --no-user-data                         # Remove user data (v2.57+)
│   ├── --trusted-image-cert <id>              # Trusted cert (repeat, v2.63+)
│   ├── --no-trusted-image-certs               # Remove trusted certs (v2.63+)
│   ├── --hostname <hostname>                  # New hostname (v2.90+)
│   ├── --reimage-boot-volume                  # Reimage boot volume (v2.93+)
│   ├── --no-reimage-boot-volume               # Don't reimage boot volume (v2.93+)
│   └── --wait                                 # Wait for rebuild
│
├── evacuate                                   # Evacuate server from failed host
│   ├── <server>                               # (positional) Server name or ID
│   ├── --host <host>                          # Target host
│   ├── --password <password>                  # New admin password
│   └── --wait                                 # Wait for evacuate
│
├── restore                                    # Restore a soft-deleted server
│   └── <server>                               # (positional) Server name or ID
│
├── ssh                                        # SSH to server
│   ├── <server>                               # (positional) Server name or ID
│   ├── --login <login>                        # Login name
│   ├── -l <login>                             # Login name (short)
│   ├── --port <port>                          # SSH port (default 22)
│   ├── --ip-version {4,6}                     # IP version to use
│   ├── --identity <file>                      # Private key file
│   ├── -i <file>                              # Private key (short)
│   ├── --address-type <type>                  # Address type: fixed, floating
│   ├── -4                                     # IPv4
│   ├── -6                                     # IPv6
│   └── -- <ssh-args>                          # Additional SSH arguments
│
├── add floating ip                            # Add floating IP to server
│   ├── <server>                               # (positional) Server name or ID
│   ├── <ip-address>                           # (positional) Floating IP address
│   └── --fixed-ip-address <ip>                # Fixed IP to associate with
│
├── remove floating ip      # Remove floating IP from server
│   ├── <server>                               # (positional) Server name or ID
│   └── <ip-address>                           # (positional) Floating IP address
│
├── add fixed ip            # Add fixed IP to server
│   ├── <server>                               # (positional) Server name or ID
│   └── <network>                              # (positional) Network (name or ID)
│
├── remove fixed ip         # Remove fixed IP from server
│   ├── <server>                               # (positional) Server name or ID
│   └── <ip-address>                           # (positional) Fixed IP address
│
├── add volume              # Attach volume to server
│   ├── <server>                               # (positional) Server name or ID
│   ├── <volume>                               # (positional) Volume (name or ID)
│   ├── --device <device>                      # Device name (e.g. /dev/vdb)
│   ├── --tag <tag>                            # Device tag (v2.49+)
│   ├── --enable-delete-on-termination         # Delete vol when server deleted (v2.79+)
│   └── --disable-delete-on-termination        # Keep vol when server deleted (v2.79+)
│
├── remove volume           # Detach volume from server
│   ├── <server>                               # (positional) Server name or ID
│   └── <volume>                               # (positional) Volume (name or ID)
│
├── add port                # Add port to server
│   ├── <server>                               # (positional) Server name or ID
│   ├── <port>                                 # (positional) Port (name or ID)
│   └── --tag <tag>                            # Interface tag (v2.49+)
│
├── remove port             # Remove port from server
│   ├── <server>                               # (positional) Server name or ID
│   └── <port>                                 # (positional) Port (name or ID)
│
├── add network             # Add network to server
│   ├── <server>                               # (positional) Server name or ID
│   ├── <network>                              # (positional) Network (name or ID)
│   └── --tag <tag>                            # Interface tag (v2.49+)
│
├── remove network          # Remove network from server
│   ├── <server>                               # (positional) Server name or ID
│   └── <network>                              # (positional) Network (name or ID)
│
├── add security group      # Add security group to server
│   ├── <server>                               # (positional) Server name or ID
│   └── <group>                                # (positional) Security group (name or ID)
│
├── remove security group   # Remove security group from server
│   ├── <server>                               # (positional) Server name or ID
│   └── <group>                                # (positional) Security group (name or ID)
│
├── backup create           # Create server backup image
│   ├── <server>                               # (positional) Server name or ID
│   ├── --name <name>                          # Backup image name
│   ├── --type <type>                          # Backup type (daily/weekly)
│   └── --rotate <count>                       # Number of backups to retain
│
├── dump create             # Create server diagnostic dump
│   └── <server> [<server> ...]                # (positional) Server(s)
│
├── image create            # Create image from server
│   ├── <server>                               # (positional) Server name or ID
│   ├── --name <name>                          # Image name
│   ├── --property <key=value>                 # Image property (repeat)
│   └── --wait                                 # Wait for image creation
│
├── event list              # List server events
│   ├── <server>                               # (positional) Server name or ID
│   ├── --long                                 # Additional fields
│   ├── --changes-since <time>                 # Events after (ISO 8601)
│   └── --changes-before <time>                # Events before (ISO 8601, v2.58+)
│
├── event show              # Show server event details
│   ├── <server>                               # (positional) Server name or ID
│   └── <request-id>                           # (positional) Request ID
│
├── group create            # Create server group
│   ├── <name>                                 # (positional) Group name
│   └── --policy <policy>                      # Policy: affinity, anti-affinity, soft-affinity, soft-anti-affinity
│
├── group delete            # Delete server group(s)
│   └── <group> [<group> ...]                  # (positional) Group(s) name or ID
│
├── group list              # List server groups
│   ├── --all-projects                         # All projects (admin)
│   ├── --limit <limit>                        # Max entries
│   └── --offset <offset>                      # Offset
│
├── group show              # Show server group details
│   └── <group>                                # (positional) Group name or ID
│
├── migration list          # List server migrations
│   ├── <server>                               # (positional) Server name or ID
│   └── --limit <limit>                        # Max entries (v2.59+)
│
├── migration show          # Show migration details
│   ├── <server>                               # (positional) Server name or ID
│   └── <migration>                            # (positional) Migration ID
│
├── migration abort         # Abort in-progress migration
│   ├── <server>                               # (positional) Server name or ID
│   └── <migration>                            # (positional) Migration ID
│
├── migration confirm       # Confirm migration
│   └── <server>                               # (positional) Server name or ID
│
├── migration revert        # Revert migration
│   └── <server>                               # (positional) Server name or ID
│
├── migration force complete # Force-complete live migration
│   ├── <server>                               # (positional) Server name or ID
│   └── <migration>                            # (positional) Migration ID
│
├── volume list             # List volumes attached to server
│   ├── <server>                               # (positional) Server name or ID
│   └── --long                                 # Show additional fields
│
├── volume set              # Set properties on attached volume
│   ├── <server>                               # (positional) Server name or ID
│   ├── <volume>                               # (positional) Volume name or ID
│   └── --delete-on-termination                # Delete vol when server deleted (v2.85+)
│
└── volume update           # Update attached volume (swap)
    ├── <server>                               # (positional) Server name or ID
    ├── <volume>                               # (positional) Current volume (name or ID)
    └── --new-volume <volume>                  # Replacement volume (name or ID)
```

---

## openstack flavor

> Compute instance types defining vCPU, RAM, and disk allocations.

```
openstack flavor
├── create              # Create new flavor
│   ├── <flavor-name>                          # (positional) Flavor name
│   ├── --id <id>                              # Custom flavor ID
│   ├── --ram <size-mb>                        # Memory in MB (default 256)
│   ├── --disk <size-gb>                       # Root disk in GB (default 0)
│   ├── --ephemeral <size-gb>                  # Ephemeral disk in GB (default 0)
│   ├── --swap <size-mb>                       # Swap in MB (default 0)
│   ├── --vcpus <vcpus>                        # Number of vCPUs (default 1)
│   ├── --rxtx-factor <factor>                 # RX/TX factor (default 1.0)
│   ├── --public                               # Available to all projects (default)
│   ├── --private                              # Restricted to specific projects
│   ├── --property <key=value>                 # Extra spec (repeat)
│   ├── --project <project>                    # Allow project access (with --private)
│   ├── --description <desc>                   # Description (v2.55+)
│   └── --project-domain <domain>              # Project domain
│
├── delete              # Delete flavor(s)
│   └── <flavor> [<flavor> ...]                # (positional) Flavor(s) name or ID
│
├── list                # List flavors
│   ├── --public                               # Only public flavors
│   ├── --private                              # Only private flavors
│   ├── --all                                  # All flavors (admin)
│   ├── --long                                 # Additional fields
│   ├── --marker <marker>                      # Pagination marker
│   ├── --limit <limit>                        # Max entries
│   └── --min-disk <size-gb>                   # Filter by min disk
│
├── set                 # Set flavor properties
│   ├── <flavor>                               # (positional) Flavor name or ID
│   ├── --property <key=value>                 # Set extra spec (repeat)
│   ├── --project <project>                    # Add project access
│   ├── --project-domain <domain>              # Project domain
│   ├── --description <desc>                   # Set description (v2.55+)
│   └── --no-property                          # Clear all extra specs
│
├── show                # Show flavor details
│   └── <flavor>                               # (positional) Flavor name or ID
│
└── unset               # Unset flavor properties
    ├── <flavor>                               # (positional) Flavor name or ID
    ├── --property <key>                       # Remove extra spec (repeat)
    └── --project <project>                    # Remove project access
```

---

## openstack keypair

> SSH key pairs for server access.

```
openstack keypair
├── create              # Create or import keypair
│   ├── <name>                                 # (positional) Keypair name
│   ├── --public-key <file>                    # Import existing public key file
│   ├── --private-key <file>                   # Save generated private key to file
│   ├── --type <type>                          # Key type: ssh, x509 (v2.2+)
│   ├── --user <user>                          # Owner (admin, v2.10+)
│   └── --user-domain <domain>                 # User domain
│
├── delete              # Delete keypair(s)
│   ├── <name> [<name> ...]                    # (positional) Keypair name(s)
│   ├── --user <user>                          # Owner (admin, v2.10+)
│   └── --user-domain <domain>                 # User domain
│
├── list                # List keypairs
│   ├── --user <user>                          # Filter by user (admin, v2.10+)
│   ├── --user-domain <domain>                 # User domain
│   ├── --limit <limit>                        # Max entries (v2.35+)
│   └── --marker <marker>                      # Pagination marker (v2.35+)
│
└── show                # Show keypair details
    ├── <name>                                 # (positional) Keypair name
    ├── --public-key                           # Show only public key
    ├── --user <user>                          # Owner (admin, v2.10+)
    └── --user-domain <domain>                 # User domain
```

---

## openstack aggregate

> Host aggregates for compute scheduling.

```
openstack aggregate
├── add host            # Add host to aggregate
│   ├── <aggregate>                            # (positional) Aggregate name or ID
│   └── <host>                                 # (positional) Host to add
│
├── cache image         # Request image pre-caching on aggregate hosts
│   ├── <aggregate>                            # (positional) Aggregate name or ID
│   └── <image> [<image> ...]                  # (positional) Image(s) to cache
│
├── create              # Create aggregate
│   ├── <name>                                 # (positional) Aggregate name
│   ├── --zone <zone>                          # Availability zone
│   └── --property <key=value>                 # Metadata (repeat)
│
├── delete              # Delete aggregate(s)
│   └── <aggregate> [<aggregate> ...]          # (positional) Aggregate(s)
│
├── list                # List aggregates
│   └── --long                                 # Additional fields
│
├── remove host         # Remove host from aggregate
│   ├── <aggregate>                            # (positional) Aggregate name or ID
│   └── <host>                                 # (positional) Host to remove
│
├── set                 # Set aggregate properties
│   ├── <aggregate>                            # (positional) Aggregate name or ID
│   ├── --name <name>                          # New name
│   ├── --zone <zone>                          # New AZ
│   ├── --property <key=value>                 # Set metadata (repeat)
│   └── --no-property                          # Clear metadata
│
├── show                # Show aggregate details
│   └── <aggregate>                            # (positional) Aggregate name or ID
│
└── unset               # Unset aggregate properties
    ├── <aggregate>                            # (positional) Aggregate name or ID
    └── --property <key>                       # Remove metadata key (repeat)
```

---

## openstack hypervisor

> Hypervisor information (admin only).

```
openstack hypervisor
├── list                # List hypervisors
│   ├── --matching <hostname>                  # Filter by hostname pattern
│   └── --long                                 # Additional fields
│
├── show                # Show hypervisor details
│   └── <hypervisor>                           # (positional) Hypervisor name or ID
│
└── stats show          # Show aggregate hypervisor stats
    └── (no flags)
```

---

## openstack host

> Compute hosts (admin).

```
openstack host
├── list                # List hosts
│   └── --zone <zone>                          # Filter by availability zone
│
├── set                 # Set host properties
│   ├── <host>                                 # (positional) Hostname
│   ├── --enable                               # Enable host
│   ├── --disable                              # Disable host
│   ├── --enable-maintenance                   # Enable maintenance mode
│   └── --disable-maintenance                  # Disable maintenance mode
│
└── show                # Show host resource usage
    └── <host>                                 # (positional) Hostname
```

---

## openstack compute agent

> Compute guest agents (admin, deprecated).

```
openstack compute agent
├── create              # Create compute agent
│   ├── <os>                                   # (positional) OS type
│   ├── <architecture>                         # (positional) Architecture
│   ├── <version>                              # (positional) Agent version
│   ├── <url>                                  # (positional) Download URL
│   ├── <md5hash>                              # (positional) MD5 hash
│   └── <hypervisor>                           # (positional) Hypervisor type
│
├── delete              # Delete compute agent(s)
│   └── <id> [<id> ...]                        # (positional) Agent ID(s)
│
├── list                # List compute agents
│   └── --hypervisor <hypervisor>              # Filter by hypervisor type
│
└── set                 # Update compute agent
    ├── <id>                                   # (positional) Agent ID
    ├── --version <version>                    # New version
    ├── --url <url>                            # New URL
    └── --md5hash <hash>                       # New hash
```

---

## openstack compute service

> Compute services (admin).

```
openstack compute service
├── delete              # Delete compute service
│   └── <service> [<service> ...]              # (positional) Service ID(s)
│
├── list                # List compute services
│   ├── --host <host>                          # Filter by host
│   ├── --service <service>                    # Filter by service binary name
│   └── --long                                 # Additional fields
│
└── set                 # Set compute service properties
    ├── <host>                                 # (positional) Hostname
    ├── <service>                              # (positional) Service binary (e.g. nova-compute)
    ├── --enable                               # Enable service
    ├── --disable                              # Disable service
    ├── --disable-reason <reason>              # Reason for disable
    ├── --up                                   # Force service up
    └── --down                                 # Force service down
```

---

## openstack console

> Server console access.

```
openstack console
├── connection show     # Show console connection info
│   └── <server>                               # (positional) Server name or ID
│
├── log show            # Show server console log
│   ├── <server>                               # (positional) Server name or ID
│   └── --lines <lines>                        # Number of lines (default all)
│
└── url show            # Show console URL
    ├── <server>                               # (positional) Server name or ID
    └── --novnc | --xvpvnc | --spice | --rdp | --serial | --mks
                                               # Console type
```

---

## openstack network

> Virtual networks (Neutron).

```
openstack network
├── create              # Create network
│   ├── <name>                                 # (positional) Network name
│   ├── --share | --no-share                   # Share between projects
│   ├── --enable | --disable                   # Enable/disable network
│   ├── --project <project>                    # Owner project
│   ├── --description <desc>                   # Description
│   ├── --mtu <mtu>                            # MTU value
│   ├── --availability-zone-hint <zone>        # AZ hint (repeat)
│   ├── --enable-port-security                 # Default port security on (default)
│   ├── --disable-port-security                # Default port security off
│   ├── --external | --internal                # External routing facility
│   ├── --default | --no-default               # Default external network
│   ├── --qos-policy <policy>                  # QoS policy (name or ID)
│   ├── --transparent-vlan | --no-transparent-vlan
│   ├── --provider-network-type <type>         # flat, geneve, gre, local, vlan, vxlan
│   ├── --provider-physical-network <net>      # Physical network name
│   ├── --provider-segment <segment>           # VLAN ID or tunnel ID
│   ├── --dns-domain <domain>                  # DNS domain
│   ├── --tag <tag>                            # Tag (repeat)
│   └── --no-tag                               # No tags
│
├── delete              # Delete network(s)
│   └── <network> [<network> ...]              # (positional) Network(s) name or ID
│
├── list                # List networks
│   ├── --external                             # Only external networks
│   ├── --internal                             # Only internal networks
│   ├── --long                                 # Additional fields
│   ├── --name <name>                          # Filter by name
│   ├── --status <status>                      # Filter by status
│   ├── --project <project>                    # Filter by project
│   ├── --project-domain <domain>              # Project domain
│   ├── --share                                # Only shared
│   ├── --no-share                             # Only non-shared
│   ├── --provider-network-type <type>         # Filter by provider type
│   ├── --provider-physical-network <net>      # Filter by physical network
│   ├── --provider-segment <segment>           # Filter by segment
│   ├── --agent <agent-id>                     # Filter by agent
│   ├── --tags <tag>                           # Filter by tags
│   └── --any-tags <tag>                       # Filter by any tag
│
├── set                 # Set network properties
│   ├── <network>                              # (positional) Network name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # New description
│   ├── --share | --no-share                   # Share settings
│   ├── --enable | --disable                   # Enable/disable
│   ├── --enable-port-security | --disable-port-security
│   ├── --external | --internal                # External flag
│   ├── --default | --no-default               # Default external
│   ├── --qos-policy <policy> | --no-qos-policy
│   ├── --mtu <mtu>                            # MTU
│   ├── --dns-domain <domain>                  # DNS domain
│   ├── --tag <tag>                            # Add tag (repeat)
│   └── --no-tag                               # Clear tags
│
├── show                # Show network details
│   └── <network>                              # (positional) Network name or ID
│
├── unset               # Unset network properties
│   ├── <network>                              # (positional) Network name or ID
│   ├── --tag <tag>                            # Remove tag (repeat)
│   └── --qos-policy                           # Remove QoS policy
│
├── agent add network   # Bind network to DHCP agent
│   ├── <agent>                                # (positional) Agent ID
│   └── <network>                              # (positional) Network
│
├── agent add router    # Bind router to L3 agent
│   ├── <agent>                                # (positional) Agent ID
│   └── <router>                               # (positional) Router
│
├── agent delete        # Delete network agent
│   └── <agent> [<agent> ...]                  # (positional) Agent ID(s)
│
├── agent list          # List network agents
│   ├── --agent-type <type>                    # Filter by type
│   ├── --host <host>                          # Filter by host
│   ├── --network <network>                    # Agents hosting network
│   ├── --router <router>                      # Agents hosting router
│   └── --long                                 # Additional fields
│
├── agent remove network  # Unbind network from DHCP agent
│   ├── <agent>                                # (positional) Agent ID
│   └── <network>                              # (positional) Network
│
├── agent remove router  # Unbind router from L3 agent
│   ├── <agent>                                # (positional) Agent ID
│   └── <router>                               # (positional) Router
│
├── agent set           # Set network agent properties
│   ├── <agent>                                # (positional) Agent ID
│   ├── --description <desc>                   # Description
│   └── --enable | --disable                   # Admin state
│
├── agent show          # Show network agent details
│   └── <agent>                                # (positional) Agent ID
│
├── auto allocated topology create  # Get or create auto-allocated topology
│   └── --project <project>                    # Project (admin)
│
├── auto allocated topology delete  # Delete auto-allocated topology
│   └── --project <project>                    # Project (admin)
│
├── flavor add profile  # Add service profile to network flavor
│   ├── <flavor>                               # (positional) Flavor name or ID
│   └── <profile>                              # (positional) Service profile ID
│
├── flavor create       # Create network flavor
│   ├── <name>                                 # (positional) Flavor name
│   ├── --service-type <type>                  # Service type
│   ├── --description <desc>                   # Description
│   └── --enable | --disable                   # Enable/disable
│
├── flavor delete       # Delete network flavor(s)
│   └── <flavor> [<flavor> ...]                # (positional) Flavor(s)
│
├── flavor list         # List network flavors
│   └── (no additional flags)
│
├── flavor profile create  # Create network flavor profile
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Enable/disable
│   ├── --driver <driver>                      # Driver path
│   └── --metainfo <metainfo>                  # Metainfo string
│
├── flavor profile delete  # Delete flavor profile(s)
│   └── <profile> [<profile> ...]              # (positional) Profile ID(s)
│
├── flavor profile list  # List flavor profiles
│   └── (no additional flags)
│
├── flavor profile set  # Set flavor profile properties
│   ├── <profile>                              # (positional) Profile ID
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Enable/disable
│   ├── --driver <driver>                      # Driver
│   └── --metainfo <metainfo>                  # Metainfo
│
├── flavor profile show  # Show flavor profile
│   └── <profile>                              # (positional) Profile ID
│
├── flavor remove profile  # Remove profile from flavor
│   ├── <flavor>                               # (positional) Flavor
│   └── <profile>                              # (positional) Profile ID
│
├── flavor set          # Set network flavor properties
│   ├── <flavor>                               # (positional) Flavor name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   └── --enable | --disable                   # Enable/disable
│
├── flavor show         # Show network flavor
│   └── <flavor>                               # (positional) Flavor name or ID
│
├── l3 conntrack helper create  # Create L3 conntrack helper
│   ├── --helper <helper>                      # Helper name (e.g. ftp, tftp)
│   ├── --protocol <protocol>                  # Protocol (tcp, udp)
│   ├── --port <port>                          # Port number
│   └── <router>                               # (positional) Router ID
│
├── l3 conntrack helper delete  # Delete L3 conntrack helper
│   ├── <conntrack-helper-id>                  # (positional) Helper ID
│   └── <router>                               # (positional) Router ID
│
├── l3 conntrack helper list  # List L3 conntrack helpers
│   └── <router>                               # (positional) Router ID
│
├── l3 conntrack helper set  # Set conntrack helper properties
│   ├── <conntrack-helper-id>                  # (positional) Helper ID
│   ├── <router>                               # (positional) Router ID
│   ├── --helper <helper>                      # Helper name
│   ├── --protocol <protocol>                  # Protocol
│   └── --port <port>                          # Port
│
├── l3 conntrack helper show  # Show conntrack helper
│   ├── <conntrack-helper-id>                  # (positional) Helper ID
│   └── <router>                               # (positional) Router ID
│
├── log create          # Create network packet log
│   ├── <name>                                 # (positional) Log name
│   ├── --enable | --disable                   # Enable/disable
│   ├── --project <project>                    # Project
│   ├── --description <desc>                   # Description
│   ├── --event <event>                        # Event: ALL, ACCEPT, DROP
│   ├── --resource <resource>                  # Security group (name or ID)
│   └── --target <target>                      # Port (name or ID)
│
├── log delete          # Delete network log(s)
│   └── <log> [<log> ...]                      # (positional) Log name or ID
│
├── log list            # List network logs
│   └── --long                                 # Additional fields
│
├── log set             # Set network log properties
│   ├── <log>                                  # (positional) Log name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   └── --enable | --disable                   # Enable/disable
│
├── log show            # Show network log
│   └── <log>                                  # (positional) Log name or ID
│
├── loggable resources list  # List loggable resource types
│   └── (no additional flags)
│
├── meter create        # Create network metering label
│   ├── <name>                                 # (positional) Label name
│   ├── --description <desc>                   # Description
│   ├── --project <project>                    # Project
│   └── --share | --no-share                   # Share between projects
│
├── meter delete        # Delete metering label(s)
│   └── <meter> [<meter> ...]                  # (positional) Label(s)
│
├── meter list          # List metering labels
│   └── (no additional flags)
│
├── meter rule create   # Create metering label rule
│   ├── <meter>                                # (positional) Metering label
│   ├── --remote-ip-prefix <cidr>              # Remote IP prefix (CIDR)
│   ├── --direction <dir>                      # ingress or egress
│   └── --exclude                              # Exclude matching traffic
│
├── meter rule delete   # Delete metering rule(s)
│   └── <rule> [<rule> ...]                    # (positional) Rule ID(s)
│
├── meter rule list     # List metering rules
│   └── (no additional flags)
│
├── meter rule show     # Show metering rule
│   └── <rule>                                 # (positional) Rule ID
│
├── meter show          # Show metering label
│   └── <meter>                                # (positional) Label name or ID
│
├── onboard subnets     # Onboard subnets to a subnet pool
│   ├── <network>                              # (positional) Network
│   └── --subnet-pool <pool>                   # Subnet pool
│
├── qos policy create   # Create QoS policy
│   ├── <name>                                 # (positional) Policy name
│   ├── --description <desc>                   # Description
│   ├── --share | --no-share                   # Share between projects
│   ├── --project <project>                    # Project
│   ├── --default | --no-default               # Default policy
│   └── --tag <tag>                            # Tag (repeat)
│
├── qos policy delete   # Delete QoS policy(s)
│   └── <policy> [<policy> ...]                # (positional) Policy(s)
│
├── qos policy list     # List QoS policies
│   ├── --share | --no-share                   # Filter shared
│   └── --project <project>                    # Filter by project
│
├── qos policy set      # Set QoS policy properties
│   ├── <policy>                               # (positional) Policy name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --share | --no-share                   # Share
│   ├── --default | --no-default               # Default
│   └── --tag <tag>                            # Add tag (repeat)
│
├── qos policy show     # Show QoS policy
│   └── <policy>                               # (positional) Policy name or ID
│
├── qos rule create     # Create QoS rule
│   ├── <policy>                               # (positional) QoS policy
│   ├── --type <type>                          # Rule type: bandwidth-limit, dscp-marking, minimum-bandwidth, minimum-packet-rate
│   ├── --max-kbps <rate>                      # Max bandwidth (kbps)
│   ├── --max-burst-kbits <burst>              # Max burst (kbits)
│   ├── --dscp-mark <mark>                     # DSCP mark value
│   ├── --min-kbps <rate>                      # Min bandwidth (kbps)
│   ├── --min-kpps <rate>                      # Min packet rate (kpps)
│   ├── --direction <dir>                      # egress or ingress
│   └── --ingress | --egress                   # Direction shortcut
│
├── qos rule delete     # Delete QoS rule
│   ├── <rule>                                 # (positional) Rule ID
│   └── <policy>                               # (positional) QoS policy
│
├── qos rule list       # List QoS rules in policy
│   └── <policy>                               # (positional) QoS policy
│
├── qos rule set        # Set QoS rule properties
│   ├── <rule>                                 # (positional) Rule ID
│   ├── <policy>                               # (positional) QoS policy
│   ├── --max-kbps <rate>                      # Max bandwidth
│   ├── --max-burst-kbits <burst>              # Max burst
│   ├── --dscp-mark <mark>                     # DSCP mark
│   ├── --min-kbps <rate>                      # Min bandwidth
│   ├── --min-kpps <rate>                      # Min packet rate
│   └── --direction <dir>                      # Direction
│
├── qos rule show       # Show QoS rule
│   ├── <rule>                                 # (positional) Rule ID
│   └── <policy>                               # (positional) QoS policy
│
├── qos rule type list  # List QoS rule types
│   ├── --all-supported                        # Show all supported
│   └── --all-rules                            # Show all rules
│
├── qos rule type show  # Show QoS rule type details
│   └── <type>                                 # (positional) Rule type
│
├── rbac create         # Create RBAC policy
│   ├── <object>                               # (positional) Object UUID
│   ├── --type <type>                          # Object type: network, qos_policy, security_group, subnetpool, address_scope, address_group
│   ├── --action <action>                      # access_as_shared or access_as_external
│   ├── --target-project <project>             # Target project
│   └── --target-all-projects                  # All projects
│
├── rbac delete         # Delete RBAC policy(s)
│   └── <rbac> [<rbac> ...]                    # (positional) RBAC ID(s)
│
├── rbac list           # List RBAC policies
│   └── --type <type>                          # Filter by object type
│
├── rbac set            # Set RBAC policy properties
│   ├── <rbac>                                 # (positional) RBAC ID
│   ├── --target-project <project>             # New target project
│   └── --target-all-projects                  # All projects
│
├── rbac show           # Show RBAC policy
│   └── <rbac>                                 # (positional) RBAC ID
│
├── segment create      # Create network segment
│   ├── <name>                                 # (positional) Segment name
│   ├── --network <network>                    # Parent network
│   ├── --network-type <type>                  # Segment type
│   ├── --physical-network <net>               # Physical network
│   ├── --segment <segment>                    # Segment ID
│   └── --description <desc>                   # Description
│
├── segment delete      # Delete segment(s)
│   └── <segment> [<segment> ...]              # (positional) Segment(s)
│
├── segment list        # List segments
│   ├── --network <network>                    # Filter by network
│   └── --long                                 # Additional fields
│
├── segment range create  # Create segment range
│   ├── <name>                                 # (positional) Range name
│   ├── --network-type <type>                  # Network type
│   ├── --physical-network <net>               # Physical network
│   ├── --minimum <min>                        # Minimum segment value
│   ├── --maximum <max>                        # Maximum segment value
│   ├── --private | --shared                   # Access level
│   └── --project <project>                    # Project (for private)
│
├── segment range delete  # Delete segment range(s)
│   └── <range> [<range> ...]                  # (positional) Range(s)
│
├── segment range list  # List segment ranges
│   └── --long                                 # Additional fields
│
├── segment range set   # Set segment range properties
│   ├── <range>                                # (positional) Range name or ID
│   ├── --name <name>                          # New name
│   ├── --minimum <min>                        # Min value
│   ├── --maximum <max>                        # Max value
│   └── --description <desc>                   # Description
│
├── segment range show  # Show segment range
│   └── <range>                                # (positional) Range name or ID
│
├── segment set         # Set segment properties
│   ├── <segment>                              # (positional) Segment name or ID
│   ├── --name <name>                          # New name
│   └── --description <desc>                   # Description
│
├── segment show        # Show segment details
│   └── <segment>                              # (positional) Segment name or ID
│
├── service provider list  # List network service providers
│   └── (no additional flags)
│
├── subport list        # List trunk subports
│   └── --trunk <trunk>                        # Trunk name or ID
│
├── trunk create        # Create trunk port
│   ├── <name>                                 # (positional) Trunk name
│   ├── --parent-port <port>                   # Parent port (name or ID)
│   ├── --subport port=<port>,segmentation-type=<type>,segmentation-id=<id>
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Admin state
│   └── --tag <tag>                            # Tag (repeat)
│
├── trunk delete        # Delete trunk(s)
│   └── <trunk> [<trunk> ...]                  # (positional) Trunk(s)
│
├── trunk list          # List trunks
│   └── --long                                 # Additional fields
│
├── trunk set           # Set trunk properties
│   ├── <trunk>                                # (positional) Trunk name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --subport port=<port>,segmentation-type=<type>,segmentation-id=<id>
│   ├── --enable | --disable                   # Admin state
│   └── --tag <tag>                            # Add tag (repeat)
│
├── trunk show          # Show trunk details
│   └── <trunk>                                # (positional) Trunk name or ID
│
└── trunk unset         # Unset trunk properties
    ├── <trunk>                                # (positional) Trunk name or ID
    ├── --subport <port>                       # Remove subport (repeat)
    └── --tag <tag>                            # Remove tag (repeat)
```

---

## openstack subnet

> IP address allocation for networks.

```
openstack subnet
├── create              # Create subnet
│   ├── <name>                                 # (positional) Subnet name
│   ├── --network <network>                    # Parent network (required)
│   ├── --subnet-range <cidr>                  # CIDR notation (required without pool)
│   ├── --subnet-pool <pool>                   # Subnet pool (name or ID)
│   ├── --use-prefix-delegation                # IPv6 prefix delegation
│   ├── --use-default-subnet-pool             # Use default subnet pool
│   ├── --prefix-length <len>                  # Prefix length (with pool)
│   ├── --dhcp | --no-dhcp                     # Enable/disable DHCP
│   ├── --dns-publish-fixed-ip                 # Publish fixed IPs in DNS
│   ├── --gateway <gateway>                    # Gateway: IP, 'auto', or 'none'
│   ├── --ip-version {4,6}                     # IP version (default 4)
│   ├── --ipv6-ra-mode <mode>                  # RA mode: dhcpv6-stateful, dhcpv6-stateless, slaac
│   ├── --ipv6-address-mode <mode>             # Addr mode: dhcpv6-stateful, dhcpv6-stateless, slaac
│   ├── --allocation-pool start=<ip>,end=<ip>  # IP pool range (repeat)
│   ├── --dns-nameserver <ip>                  # DNS server (repeat)
│   ├── --host-route destination=<cidr>,gateway=<ip>  # Host route (repeat)
│   ├── --service-type <type>                  # Service type (repeat)
│   ├── --description <desc>                   # Description
│   ├── --network-segment <segment>            # Network segment
│   ├── --project <project>                    # Owner project
│   ├── --tag <tag>                            # Tag (repeat)
│   └── --no-tag                               # No tags
│
├── delete              # Delete subnet(s)
│   └── <subnet> [<subnet> ...]                # (positional) Subnet(s)
│
├── list                # List subnets
│   ├── --long                                 # Additional fields
│   ├── --ip-version {4,6}                     # Filter by IP version
│   ├── --dhcp | --no-dhcp                     # Filter by DHCP
│   ├── --network <network>                    # Filter by network
│   ├── --project <project>                    # Filter by project
│   ├── --gateway <ip>                         # Filter by gateway
│   ├── --name <name>                          # Filter by name
│   ├── --subnet-range <cidr>                  # Filter by CIDR
│   ├── --subnet-pool <pool>                   # Filter by pool
│   ├── --tags <tag>                           # Filter by tags
│   └── --any-tags <tag>                       # Filter any tag
│
├── set                 # Set subnet properties
│   ├── <subnet>                               # (positional) Subnet name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --dhcp | --no-dhcp                     # DHCP
│   ├── --gateway <gateway>                    # Gateway
│   ├── --allocation-pool start=<ip>,end=<ip>  # Add pool (repeat)
│   ├── --no-allocation-pool                   # Clear pools
│   ├── --dns-nameserver <ip>                  # Add DNS (repeat)
│   ├── --no-dns-nameserver                    # Clear DNS
│   ├── --host-route destination=<cidr>,gateway=<ip>
│   ├── --no-host-route                        # Clear routes
│   ├── --service-type <type>                  # Add service type
│   ├── --tag <tag>                            # Add tag (repeat)
│   └── --no-tag                               # Clear tags
│
├── show                # Show subnet details
│   └── <subnet>                               # (positional) Subnet name or ID
│
└── unset               # Unset subnet properties
    ├── <subnet>                               # (positional) Subnet name or ID
    ├── --allocation-pool start=<ip>,end=<ip>  # Remove pool
    ├── --dns-nameserver <ip>                  # Remove DNS
    ├── --host-route destination=<cidr>,gateway=<ip>
    ├── --service-type <type>                  # Remove service type
    └── --tag <tag>                            # Remove tag (repeat)
```

---

## openstack subnet pool

> Subnet pools for CIDR allocation.

```
openstack subnet pool
├── create              # Create subnet pool
│   ├── <name>                                 # (positional) Pool name
│   ├── --pool-prefix <prefix>                 # Pool prefix (CIDR, repeat)
│   ├── --default-prefix-length <len>          # Default prefix length
│   ├── --min-prefix-length <len>              # Min prefix length
│   ├── --max-prefix-length <len>              # Max prefix length
│   ├── --project <project>                    # Owner project
│   ├── --address-scope <scope>                # Address scope
│   ├── --default | --no-default               # Default subnet pool
│   ├── --share | --no-share                   # Share
│   ├── --description <desc>                   # Description
│   └── --tag <tag>                            # Tag (repeat)
│
├── delete              # Delete subnet pool(s)
│   └── <pool> [<pool> ...]                    # (positional) Pool(s)
│
├── list                # List subnet pools
│   ├── --long                                 # Additional fields
│   ├── --share | --no-share                   # Filter shared
│   ├── --default | --no-default               # Filter default
│   ├── --project <project>                    # Filter by project
│   ├── --name <name>                          # Filter by name
│   ├── --address-scope <scope>                # Filter by scope
│   └── --tags <tag>                           # Filter by tags
│
├── set                 # Set subnet pool properties
│   ├── <pool>                                 # (positional) Pool name or ID
│   ├── --name <name>                          # New name
│   ├── --pool-prefix <prefix>                 # Add prefix (repeat)
│   ├── --default-prefix-length <len>          # Default length
│   ├── --min-prefix-length <len>              # Min length
│   ├── --max-prefix-length <len>              # Max length
│   ├── --address-scope <scope>                # Address scope
│   ├── --no-address-scope                     # Clear scope
│   ├── --default | --no-default               # Default pool
│   ├── --description <desc>                   # Description
│   └── --tag <tag>                            # Add tag (repeat)
│
├── show                # Show subnet pool details
│   └── <pool>                                 # (positional) Pool name or ID
│
└── unset               # Unset subnet pool properties
    ├── <pool>                                 # (positional) Pool name or ID
    ├── --pool-prefix <prefix>                 # Remove prefix (repeat)
    └── --tag <tag>                            # Remove tag (repeat)
```

---

## openstack router

> Virtual routers for L3 networking.

```
openstack router
├── create              # Create router
│   ├── <name>                                 # (positional) Router name
│   ├── --enable | --disable                   # Admin state
│   ├── --distributed | --centralized          # Router mode
│   ├── --ha | --no-ha                         # High availability
│   ├── --description <desc>                   # Description
│   ├── --project <project>                    # Owner project
│   ├── --availability-zone-hint <zone>        # AZ hint (repeat)
│   ├── --external-gateway <network>           # External gateway network (repeat)
│   ├── --fixed-ip subnet=<s>,ip-address=<ip>  # Fixed IP on gateway (repeat)
│   ├── --enable-snat | --disable-snat         # Source NAT
│   ├── --enable-ndp-proxy | --disable-ndp-proxy
│   ├── --flavor <flavor-id>                   # Router flavor
│   ├── --enable-default-route-bfd             # BFD for default routes
│   ├── --disable-default-route-bfd
│   ├── --enable-default-route-ecmp            # ECMP default routes
│   ├── --disable-default-route-ecmp
│   ├── --qos-policy <policy>                  # QoS on gateway
│   ├── --tag <tag>                            # Tag (repeat)
│   └── --no-tag                               # No tags
│
├── delete              # Delete router(s)
│   └── <router> [<router> ...]                # (positional) Router(s)
│
├── list                # List routers
│   ├── --long                                 # Additional fields
│   ├── --name <name>                          # Filter by name
│   ├── --enable | --disable                   # Filter by state
│   ├── --project <project>                    # Filter by project
│   ├── --tags <tag>                           # Filter by tags
│   └── --any-tags <tag>                       # Filter any tag
│
├── set                 # Set router properties
│   ├── <router>                               # (positional) Router name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Admin state
│   ├── --distributed | --centralized          # Mode (disabled only)
│   ├── --ha | --no-ha                         # HA (disabled only)
│   ├── --external-gateway <network>           # External gateway (repeat)
│   ├── --fixed-ip subnet=<s>,ip-address=<ip>  # Fixed IP (repeat)
│   ├── --enable-snat | --disable-snat         # SNAT
│   ├── --enable-ndp-proxy | --disable-ndp-proxy
│   ├── --route destination=<cidr>,gateway=<ip>  # Add route (repeat, deprecated)
│   ├── --no-route                             # Clear routes
│   ├── --qos-policy <policy> | --no-qos-policy
│   ├── --tag <tag>                            # Add tag (repeat)
│   ├── --no-tag                               # Clear tags
│   ├── --enable-default-route-bfd | --disable-default-route-bfd
│   └── --enable-default-route-ecmp | --disable-default-route-ecmp
│
├── show                # Show router details
│   └── <router>                               # (positional) Router name or ID
│
├── unset               # Unset router properties
│   ├── <router>                               # (positional) Router name or ID
│   ├── --route destination=<cidr>,gateway=<ip>  # Remove route
│   ├── --external-gateway                     # Remove gateway
│   ├── --qos-policy                           # Remove QoS
│   └── --tag <tag>                            # Remove tag (repeat)
│
├── add subnet          # Add subnet interface to router
│   ├── <router>                               # (positional) Router name or ID
│   └── <subnet>                               # (positional) Subnet name or ID
│
├── remove subnet       # Remove subnet interface from router
│   ├── <router>                               # (positional) Router name or ID
│   └── <subnet>                               # (positional) Subnet name or ID
│
├── add port            # Add port interface to router
│   ├── <router>                               # (positional) Router name or ID
│   └── <port>                                 # (positional) Port name or ID
│
├── remove port         # Remove port interface from router
│   ├── <router>                               # (positional) Router name or ID
│   └── <port>                                 # (positional) Port name or ID
│
├── add route           # Add static route to router
│   ├── <router>                               # (positional) Router name or ID
│   └── --route destination=<cidr>,gateway=<ip>  # Route (repeat)
│
├── remove route        # Remove static route from router
│   ├── <router>                               # (positional) Router name or ID
│   └── --route destination=<cidr>,gateway=<ip>  # Route (repeat)
│
├── add gateway         # Add external gateway to router
│   ├── <router>                               # (positional) Router name or ID
│   ├── <network>                              # (positional) External network
│   ├── --fixed-ip subnet=<s>,ip-address=<ip>  # Fixed IP (repeat)
│   └── --enable-snat | --disable-snat         # SNAT
│
├── remove gateway      # Remove external gateway from router
│   ├── <router>                               # (positional) Router name or ID
│   └── <network>                              # (positional) External network
│
├── ndp proxy create    # Create NDP proxy entry
│   ├── <router>                               # (positional) Router
│   ├── --port <port>                          # Internal port
│   ├── --ip-address <ip>                      # IPv6 address
│   └── --name <name>                          # Name
│
├── ndp proxy delete    # Delete NDP proxy entry
│   └── <ndp-proxy>                            # (positional) NDP proxy ID
│
├── ndp proxy list      # List NDP proxy entries
│   └── --router <router>                      # Filter by router
│
├── ndp proxy set       # Set NDP proxy properties
│   ├── <ndp-proxy>                            # (positional) NDP proxy ID
│   └── --name <name>                          # New name
│
└── ndp proxy show      # Show NDP proxy entry
    └── <ndp-proxy>                            # (positional) NDP proxy ID
```

---

## openstack port

> Virtual switch ports on networks.

```
openstack port
├── create              # Create port
│   ├── <name>                                 # (positional) Port name
│   ├── --network <network>                    # Network (required)
│   ├── --description <desc>                   # Description
│   ├── --device <device-id>                   # Device ID
│   ├── --mac-address <mac>                    # MAC address
│   ├── --device-owner <owner>                 # Device owner
│   ├── --vnic-type <type>                     # VNIC type: direct, macvtap, normal, baremetal, vdpa
│   ├── --host <host-id>                       # Bind to host
│   ├── --dns-domain <domain>                  # DNS domain
│   ├── --dns-name <name>                      # DNS name
│   ├── --fixed-ip subnet=<s>,ip-address=<ip>  # Fixed IP (repeat)
│   ├── --no-fixed-ip                          # No IP assigned
│   ├── --binding-profile <profile>            # Binding profile (key=val or JSON)
│   ├── --enable | --disable                   # Admin state
│   ├── --project <project>                    # Owner project
│   ├── --security-group <group>               # Security group (repeat)
│   ├── --no-security-group                    # No security groups
│   ├── --qos-policy <policy>                  # QoS policy
│   ├── --enable-port-security | --disable-port-security
│   ├── --allowed-address ip-address=<ip>[,mac-address=<mac>]  # (repeat)
│   ├── --extra-dhcp-option name=<n>[,value=<v>,ip-version={4,6}]
│   ├── --numa-policy-required | --numa-policy-preferred | --numa-policy-socket | --numa-policy-legacy
│   ├── --hint <alias=value>                   # Port hint
│   ├── --trusted | --not-trusted              # Trusted port
│   ├── --device-profile <profile>             # Device profile
│   ├── --hardware-offload-type <type>         # Offload type
│   ├── --tag <tag>                            # Tag (repeat)
│   └── --no-tag                               # No tags
│
├── delete              # Delete port(s)
│   └── <port> [<port> ...]                    # (positional) Port(s)
│
├── list                # List ports
│   ├── --long                                 # Additional fields
│   ├── --device-owner <owner>                 # Filter by device owner
│   ├── --network <network>                    # Filter by network
│   ├── --router <router>                      # Filter by router
│   ├── --mac-address <mac>                    # Filter by MAC
│   ├── --fixed-ip subnet=<s>,ip-address=<ip>  # Filter by fixed IP
│   ├── --project <project>                    # Filter by project
│   ├── --name <name>                          # Filter by name
│   ├── --tags <tag>                           # Filter by tags
│   └── --any-tags <tag>                       # Filter any tag
│
├── set                 # Set port properties
│   ├── <port>                                 # (positional) Port name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --device <device-id>                   # Device ID
│   ├── --mac-address <mac>                    # MAC address
│   ├── --device-owner <owner>                 # Device owner
│   ├── --vnic-type <type>                     # VNIC type
│   ├── --host <host>                          # Host
│   ├── --dns-domain <domain>                  # DNS domain
│   ├── --dns-name <name>                      # DNS name
│   ├── --fixed-ip subnet=<s>,ip-address=<ip>  # Add fixed IP (repeat)
│   ├── --no-fixed-ip                          # Clear fixed IPs
│   ├── --binding-profile <profile>            # Binding profile
│   ├── --no-binding-profile                   # Clear binding profile
│   ├── --enable | --disable                   # Admin state
│   ├── --security-group <group>               # Add security group (repeat)
│   ├── --no-security-group                    # Clear security groups
│   ├── --qos-policy <policy> | --no-qos-policy
│   ├── --enable-port-security | --disable-port-security
│   ├── --allowed-address ip-address=<ip>[,mac-address=<mac>]
│   ├── --no-allowed-address                   # Clear allowed addresses
│   ├── --data-plane-status <status>           # Data plane status
│   ├── --tag <tag>                            # Add tag (repeat)
│   └── --no-tag                               # Clear tags
│
├── show                # Show port details
│   └── <port>                                 # (positional) Port name or ID
│
└── unset               # Unset port properties
    ├── <port>                                 # (positional) Port name or ID
    ├── --fixed-ip subnet=<s>,ip-address=<ip>  # Remove fixed IP
    ├── --binding-profile <key>                # Remove binding key
    ├── --security-group <group>               # Remove security group
    ├── --allowed-address ip-address=<ip>[,mac-address=<mac>]
    ├── --qos-policy                           # Remove QoS
    ├── --data-plane-status                    # Clear data plane status
    └── --tag <tag>                            # Remove tag (repeat)
```

---

## openstack floating ip

> Floating IPs for external connectivity.

```
openstack floating ip
├── create              # Allocate floating IP
│   ├── <network>                              # (positional) External network (name or ID)
│   ├── --subnet <subnet>                      # Allocate from subnet
│   ├── --port <port>                          # Associate with port
│   ├── --floating-ip-address <ip>             # Specific IP to allocate
│   ├── --fixed-ip-address <ip>                # Fixed IP to map
│   ├── --qos-policy <policy>                  # QoS policy
│   ├── --description <desc>                   # Description
│   ├── --project <project>                    # Owner project
│   ├── --dns-domain <domain>                  # DNS domain
│   ├── --dns-name <name>                      # DNS name
│   ├── --tag <tag>                            # Tag (repeat)
│   └── --no-tag                               # No tags
│
├── delete              # Release floating IP(s)
│   └── <floating-ip> [<floating-ip> ...]      # (positional) Floating IP(s)
│
├── list                # List floating IPs
│   ├── --network <network>                    # Filter by network
│   ├── --port <port>                          # Filter by port
│   ├── --fixed-ip-address <ip>                # Filter by fixed IP
│   ├── --floating-ip-address <ip>             # Filter by floating IP
│   ├── --long                                 # Additional fields
│   ├── --status <status>                      # Filter by status
│   ├── --project <project>                    # Filter by project
│   ├── --router <router>                      # Filter by router
│   ├── --tags <tag>                           # Filter by tags
│   └── --any-tags <tag>                       # Filter any tag
│
├── set                 # Set floating IP properties
│   ├── <floating-ip>                          # (positional) Floating IP ID
│   ├── --port <port>                          # Associate with port
│   ├── --fixed-ip-address <ip>                # Fixed IP to map
│   ├── --description <desc>                   # Description
│   ├── --qos-policy <policy>                  # QoS policy
│   └── --tag <tag>                            # Add tag (repeat)
│
├── show                # Show floating IP details
│   └── <floating-ip>                          # (positional) Floating IP ID or address
│
├── unset               # Unset floating IP properties
│   ├── <floating-ip>                          # (positional) Floating IP ID
│   ├── --port                                 # Disassociate from port
│   ├── --qos-policy                           # Remove QoS
│   └── --tag <tag>                            # Remove tag (repeat)
│
├── pool list           # List floating IP pools (legacy)
│   └── (no additional flags)
│
├── port forwarding create  # Create port forwarding rule
│   ├── <floating-ip>                          # (positional) Floating IP ID
│   ├── --internal-ip-address <ip>             # Internal IP
│   ├── --internal-port <port>                 # Internal port or range
│   ├── --external-port <port>                 # External port or range
│   ├── --internal-protocol-port <port>        # Internal protocol port
│   ├── --external-protocol-port <port>        # External protocol port
│   ├── --port <port>                          # Internal port ID
│   ├── --protocol <protocol>                  # Protocol: tcp, udp
│   └── --description <desc>                   # Description
│
├── port forwarding delete  # Delete port forwarding rule(s)
│   ├── <floating-ip>                          # (positional) Floating IP ID
│   └── <port-forwarding-id> [...]             # (positional) Rule ID(s)
│
├── port forwarding list  # List port forwarding rules
│   ├── <floating-ip>                          # (positional) Floating IP ID
│   ├── --port <port>                          # Filter by internal port
│   └── --protocol <protocol>                  # Filter by protocol
│
├── port forwarding set  # Set port forwarding properties
│   ├── <floating-ip>                          # (positional) Floating IP ID
│   ├── <port-forwarding-id>                   # (positional) Rule ID
│   ├── --internal-ip-address <ip>             # Internal IP
│   ├── --internal-port <port>                 # Internal port
│   ├── --external-port <port>                 # External port
│   ├── --port <port>                          # Internal port ID
│   ├── --protocol <protocol>                  # Protocol
│   └── --description <desc>                   # Description
│
└── port forwarding show  # Show port forwarding rule
    ├── <floating-ip>                          # (positional) Floating IP ID
    └── <port-forwarding-id>                   # (positional) Rule ID
```

---

## openstack security group

> Network security groups and rules.

```
openstack security group
├── create              # Create security group
│   ├── <name>                                 # (positional) Group name
│   ├── --description <desc>                   # Description
│   ├── --project <project>                    # Owner project
│   ├── --stateful | --stateless               # Stateful or stateless
│   ├── --tag <tag>                            # Tag (repeat)
│   └── --no-tag                               # No tags
│
├── delete              # Delete security group(s)
│   └── <group> [<group> ...]                  # (positional) Group(s)
│
├── list                # List security groups
│   ├── --all-projects                         # All projects
│   ├── --project <project>                    # Filter by project
│   ├── --tags <tag>                           # Filter by tags
│   └── --any-tags <tag>                       # Filter any tag
│
├── set                 # Set security group properties
│   ├── <group>                                # (positional) Group name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --stateful | --stateless               # State tracking
│   └── --tag <tag>                            # Add tag (repeat)
│
├── show                # Show security group details
│   └── <group>                                # (positional) Group name or ID
│
├── unset               # Unset security group properties
│   ├── <group>                                # (positional) Group name or ID
│   └── --tag <tag>                            # Remove tag (repeat)
│
├── rule create         # Create security group rule
│   ├── <group>                                # (positional) Security group (name or ID)
│   ├── --remote-ip <cidr>                     # Remote IP (CIDR)
│   ├── --remote-group <group>                 # Remote security group
│   ├── --remote-address-group <group>         # Remote address group
│   ├── --dst-port <port-range>                # Destination port or range (e.g. 80, 8000:8080)
│   ├── --protocol <protocol>                  # Protocol: tcp, udp, icmp, any, or number
│   ├── --description <desc>                   # Description
│   ├── --icmp-type <type>                     # ICMP type
│   ├── --icmp-code <code>                     # ICMP code
│   ├── --ingress | --egress                   # Direction (default: ingress)
│   ├── --ethertype <type>                     # IPv4 or IPv6
│   └── --project <project>                    # Owner project
│
├── rule delete         # Delete security group rule(s)
│   └── <rule> [<rule> ...]                    # (positional) Rule ID(s)
│
├── rule list           # List security group rules
│   ├── --all-projects                         # All projects
│   ├── --protocol <protocol>                  # Filter by protocol
│   ├── --ethertype <type>                     # Filter by ethertype
│   ├── --ingress | --egress                   # Filter by direction
│   ├── --long                                 # Additional fields
│   └── <group>                                # (positional, optional) Security group
│
└── rule show           # Show security group rule
    └── <rule>                                 # (positional) Rule ID
```

---

## openstack default security group rule

> Default security group rules applied to new security groups.

```
openstack default security group rule
├── create              # Create default rule
│   ├── --protocol <protocol>                  # Protocol
│   ├── --dst-port <port-range>                # Destination port range
│   ├── --icmp-type <type>                     # ICMP type
│   ├── --icmp-code <code>                     # ICMP code
│   ├── --remote-ip <cidr>                     # Remote IP
│   ├── --remote-address-group <group>         # Remote address group
│   ├── --ingress | --egress                   # Direction
│   ├── --ethertype <type>                     # Ethertype
│   ├── --description <desc>                   # Description
│   └── --for-default-sg | --for-custom-sg     # Apply to default or custom SGs
│
├── delete              # Delete default rule(s)
│   └── <rule> [<rule> ...]                    # (positional) Rule ID(s)
│
├── list                # List default rules
│   └── (no additional flags)
│
└── show                # Show default rule
    └── <rule>                                 # (positional) Rule ID
```

---

## openstack address group

> Address groups for security group rules.

```
openstack address group
├── create              # Create address group
│   ├── <name>                                 # (positional) Name
│   ├── --address <ip-or-cidr>                 # Address (repeat)
│   ├── --description <desc>                   # Description
│   └── --project <project>                    # Owner
│
├── delete              # Delete address group(s)
│   └── <group> [<group> ...]                  # (positional) Group(s)
│
├── list                # List address groups
│   ├── --name <name>                          # Filter by name
│   └── --project <project>                    # Filter by project
│
├── set                 # Set address group properties
│   ├── <group>                                # (positional) Group name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   └── --address <ip-or-cidr>                 # Add address (repeat)
│
├── show                # Show address group
│   └── <group>                                # (positional) Group name or ID
│
└── unset               # Unset address group properties
    ├── <group>                                # (positional) Group name or ID
    └── --address <ip-or-cidr>                 # Remove address (repeat)
```

---

## openstack address scope

> Address scopes for subnet pools.

```
openstack address scope
├── create              # Create address scope
│   ├── <name>                                 # (positional) Name
│   ├── --ip-version {4,6}                     # IP version
│   ├── --project <project>                    # Owner
│   ├── --share | --no-share                   # Share
│   └── --description <desc>                   # Description
│
├── delete              # Delete address scope(s)
│   └── <scope> [<scope> ...]                  # (positional) Scope(s)
│
├── list                # List address scopes
│   ├── --name <name>                          # Filter by name
│   ├── --ip-version {4,6}                     # Filter by IP version
│   └── --project <project>                    # Filter by project
│
├── set                 # Set address scope properties
│   ├── <scope>                                # (positional) Scope name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   └── --share | --no-share                   # Share
│
└── show                # Show address scope
    └── <scope>                                # (positional) Scope name or ID
```

---

## openstack firewall group

> Firewall as a Service v2.

```
openstack firewall group
├── create              # Create firewall group
│   ├── <name>                                 # (positional) Name
│   ├── --description <desc>                   # Description
│   ├── --ingress-firewall-policy <policy>     # Ingress policy
│   ├── --egress-firewall-policy <policy>      # Egress policy
│   ├── --port <port>                          # Port (repeat)
│   ├── --no-port                              # No ports
│   ├── --project <project>                    # Owner
│   ├── --enable | --disable                   # Admin state
│   └── --share | --no-share                   # Share
│
├── delete              # Delete firewall group(s)
│   └── <group> [<group> ...]                  # (positional) Group(s)
│
├── list                # List firewall groups
│   └── --long                                 # Additional fields
│
├── set                 # Set firewall group properties
│   ├── <group>                                # (positional) Group name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --ingress-firewall-policy <policy>     # Ingress policy
│   ├── --no-ingress-firewall-policy           # Remove ingress policy
│   ├── --egress-firewall-policy <policy>      # Egress policy
│   ├── --no-egress-firewall-policy            # Remove egress policy
│   ├── --port <port>                          # Add port (repeat)
│   ├── --no-port                              # Remove all ports
│   ├── --enable | --disable                   # Admin state
│   └── --share | --no-share                   # Share
│
├── show                # Show firewall group
│   └── <group>                                # (positional) Group name or ID
│
├── unset               # Unset firewall group properties
│   ├── <group>                                # (positional) Group name or ID
│   ├── --port <port>                          # Remove port (repeat)
│   ├── --ingress-firewall-policy              # Remove ingress policy
│   └── --egress-firewall-policy               # Remove egress policy
│
├── policy create       # Create firewall policy
│   ├── <name>                                 # (positional) Policy name
│   ├── --description <desc>                   # Description
│   ├── --firewall-rule <rule>                 # Rule to add (repeat, ordered)
│   ├── --audited | --no-audited               # Audit flag
│   ├── --project <project>                    # Owner
│   └── --share | --no-share                   # Share
│
├── policy delete       # Delete firewall policy(s)
│   └── <policy> [<policy> ...]                # (positional) Policy(s)
│
├── policy add rule     # Add rule to policy
│   ├── <policy>                               # (positional) Policy
│   ├── <rule>                                 # (positional) Rule to add
│   ├── --insert-before <rule>                 # Insert before rule
│   └── --insert-after <rule>                  # Insert after rule
│
├── policy remove rule  # Remove rule from policy
│   ├── <policy>                               # (positional) Policy
│   └── <rule>                                 # (positional) Rule to remove
│
├── policy list         # List firewall policies
│   └── --long                                 # Additional fields
│
├── policy set          # Set firewall policy properties
│   ├── <policy>                               # (positional) Policy name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --firewall-rule <rule>                 # Add rule (repeat)
│   ├── --no-firewall-rule                     # Clear rules
│   ├── --audited | --no-audited               # Audit flag
│   └── --share | --no-share                   # Share
│
├── policy show         # Show firewall policy
│   └── <policy>                               # (positional) Policy name or ID
│
├── policy unset        # Unset firewall policy properties
│   ├── <policy>                               # (positional) Policy name or ID
│   └── --firewall-rule <rule>                 # Remove rule (repeat)
│
├── rule create         # Create firewall rule
│   ├── <name>                                 # (positional) Rule name
│   ├── --description <desc>                   # Description
│   ├── --protocol <protocol>                  # Protocol: tcp, udp, icmp, any
│   ├── --ip-version {4,6}                     # IP version
│   ├── --source-ip-address <cidr>             # Source IP
│   ├── --destination-ip-address <cidr>        # Destination IP
│   ├── --source-port <port>                   # Source port or range
│   ├── --destination-port <port>              # Destination port or range
│   ├── --action {allow,deny,reject}           # Action
│   ├── --enable | --disable                   # Enable/disable rule
│   ├── --project <project>                    # Owner
│   └── --share | --no-share                   # Share
│
├── rule delete         # Delete firewall rule(s)
│   └── <rule> [<rule> ...]                    # (positional) Rule(s)
│
├── rule list           # List firewall rules
│   └── --long                                 # Additional fields
│
├── rule set            # Set firewall rule properties
│   ├── <rule>                                 # (positional) Rule name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --protocol <protocol>                  # Protocol
│   ├── --ip-version {4,6}                     # IP version
│   ├── --source-ip-address <cidr>             # Source IP
│   ├── --destination-ip-address <cidr>        # Destination IP
│   ├── --source-port <port>                   # Source port
│   ├── --destination-port <port>              # Destination port
│   ├── --action {allow,deny,reject}           # Action
│   ├── --enable | --disable                   # Enable/disable
│   └── --share | --no-share                   # Share
│
├── rule show           # Show firewall rule
│   └── <rule>                                 # (positional) Rule name or ID
│
└── rule unset          # Unset firewall rule properties
    ├── <rule>                                 # (positional) Rule name or ID
    ├── --source-ip-address                    # Clear source IP
    ├── --destination-ip-address               # Clear destination IP
    ├── --source-port                          # Clear source port
    └── --destination-port                     # Clear destination port
```

---

## openstack volume

> Block storage volumes (Cinder).

```
openstack volume
├── create              # Create volume
│   ├── [<name>]                               # (positional, optional) Volume name
│   ├── --size <size-gb>                       # Size in GB (required unless from source)
│   ├── --type <type>                          # Volume type
│   ├── --image <image>                        # Source image (name or ID)
│   ├── --snapshot <snapshot>                  # Source snapshot (name or ID)
│   ├── --source <volume>                      # Clone from volume (name or ID)
│   ├── --backup <backup>                      # Restore from backup (v3.47+)
│   ├── --description <desc>                   # Description
│   ├── --availability-zone <zone>             # Availability zone
│   ├── --consistency-group <group>            # Consistency group
│   ├── --property <key=value>                 # Metadata (repeat)
│   ├── --hint <key=value>                     # Scheduler hint (repeat)
│   ├── --bootable | --non-bootable            # Bootable flag
│   ├── --read-only | --read-write             # Access mode
│   ├── --remote-source <key=value>            # Remote source attributes (admin)
│   ├── --host <host>                          # Host (with --remote-source)
│   └── --cluster <cluster>                    # Cluster (with --remote-source, v3.16+)
│
├── delete              # Delete volume(s)
│   ├── <volume> [<volume> ...]                # (positional) Volume(s) name or ID
│   ├── --force                                # Force delete (admin)
│   └── --purge                                # Remove any snapshots along with volume
│
├── list                # List volumes
│   ├── --all-projects                         # All projects (admin)
│   ├── --project <project>                    # Filter by project
│   ├── --project-domain <domain>              # Project domain
│   ├── --user <user>                          # Filter by user
│   ├── --user-domain <domain>                 # User domain
│   ├── --name <name>                          # Filter by name
│   ├── --status <status>                      # Filter by status
│   ├── --long                                 # Additional fields
│   ├── --limit <limit>                        # Max entries
│   ├── --marker <marker>                      # Pagination marker
│   └── --sort <key>:<dir>                     # Sort by field
│
├── set                 # Set volume properties
│   ├── <volume>                               # (positional) Volume name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --size <size-gb>                       # Extend volume (only increase)
│   ├── --property <key=value>                 # Set metadata (repeat)
│   ├── --no-property                          # Clear all metadata
│   ├── --image-property <key=value>           # Image metadata (repeat)
│   ├── --bootable | --non-bootable            # Bootable flag
│   ├── --read-only | --read-write             # Access mode
│   ├── --type <type>                          # Retype volume
│   └── --state <state>                        # Override state (admin)
│
├── show                # Show volume details
│   └── <volume>                               # (positional) Volume name or ID
│
├── unset               # Unset volume properties
│   ├── <volume>                               # (positional) Volume name or ID
│   ├── --property <key>                       # Remove metadata (repeat)
│   └── --image-property <key>                 # Remove image metadata (repeat)
│
├── migrate             # Migrate volume to new host
│   ├── <volume>                               # (positional) Volume name or ID
│   ├── --host <host>                          # Destination host
│   ├── --force-host-copy                      # Force host copy
│   └── --lock-volume | --unlock-volume        # Lock during migration
│
├── revert              # Revert volume to most recent snapshot
│   └── <volume>                               # (positional) Volume (name or ID)
│
├── summary             # Show volume summary
│   └── --all-projects                         # All projects (admin)
│
├── attachment create   # Create volume attachment
│   ├── <volume>                               # (positional) Volume
│   ├── <server>                               # (positional) Server
│   └── --connect                              # Connect attachment
│
├── attachment delete   # Delete volume attachment(s)
│   └── <attachment> [<attachment> ...]        # (positional) Attachment ID(s)
│
├── attachment list     # List volume attachments
│   ├── --all-projects                         # All projects
│   ├── --project <project>                    # Filter by project
│   ├── --status <status>                      # Filter by status
│   ├── --marker <marker>                      # Pagination marker
│   └── --limit <limit>                        # Max entries
│
├── attachment set      # Set volume attachment properties
│   └── <attachment>                           # (positional) Attachment ID
│
├── attachment show     # Show volume attachment
│   └── <attachment>                           # (positional) Attachment ID
│
├── attachment complete # Mark attachment complete
│   └── <attachment>                           # (positional) Attachment ID
│
├── backend capability show  # Show volume backend capabilities
│   └── <host>                                 # (positional) Backend host
│
├── backend pool list   # List volume backend pools
│   ├── --long                                 # Additional fields
│   └── --detail                               # Show details
│
├── host set            # Set volume host properties
│   ├── <host>                                 # (positional) Host
│   └── --disable | --enable                   # Disable/enable
│
├── message delete      # Delete volume message(s)
│   └── <message> [<message> ...]              # (positional) Message ID(s)
│
├── message list        # List volume messages
│   ├── --all-projects                         # All projects
│   ├── --project <project>                    # Filter by project
│   ├── --marker <marker>                      # Pagination marker
│   └── --limit <limit>                        # Max entries
│
├── message show        # Show volume message
│   └── <message>                              # (positional) Message ID
│
├── service list        # List volume services
│   ├── --host <host>                          # Filter by host
│   └── --service <service>                    # Filter by service binary
│
└── service set         # Set volume service properties
    ├── <host>                                 # (positional) Host
    ├── <service>                              # (positional) Service binary
    ├── --enable | --disable                   # Enable/disable
    └── --disable-reason <reason>              # Reason for disable
```

---

## openstack volume snapshot

> Volume snapshots.

```
openstack volume snapshot
├── create              # Create snapshot
│   ├── <snapshot-name>                        # (positional) Snapshot name
│   ├── --volume <volume>                      # Source volume (default: same as name)
│   ├── --description <desc>                   # Description
│   ├── --force                                # Snapshot attached volume
│   ├── --property <key=value>                 # Metadata (repeat)
│   └── --remote-source <key=value>            # Remote source (admin, repeat)
│
├── delete              # Delete snapshot(s)
│   ├── <snapshot> [<snapshot> ...]            # (positional) Snapshot(s)
│   └── --force                                # Force delete (admin)
│
├── list                # List snapshots
│   ├── --all-projects                         # All projects (admin)
│   ├── --project <project>                    # Filter by project
│   ├── --long                                 # Additional fields
│   ├── --name <name>                          # Filter by name
│   ├── --status <status>                      # Filter by status
│   ├── --volume <volume>                      # Filter by volume
│   ├── --limit <limit>                        # Max entries
│   └── --marker <marker>                      # Pagination marker
│
├── set                 # Set snapshot properties
│   ├── <snapshot>                             # (positional) Snapshot name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --property <key=value>                 # Set metadata (repeat)
│   ├── --no-property                          # Clear metadata
│   └── --state <state>                        # Override state (admin)
│
├── show                # Show snapshot details
│   └── <snapshot>                             # (positional) Snapshot name or ID
│
└── unset               # Unset snapshot properties
    ├── <snapshot>                             # (positional) Snapshot name or ID
    └── --property <key>                       # Remove metadata (repeat)
```

---

## openstack volume backup

> Volume backups.

```
openstack volume backup
├── create              # Create backup
│   ├── <volume>                               # (positional) Volume (name or ID)
│   ├── --name <name>                          # Backup name
│   ├── --description <desc>                   # Description
│   ├── --container <container>                # Backup container name
│   ├── --snapshot <snapshot>                  # Snapshot to backup
│   ├── --force                                # Backup attached volume
│   ├── --incremental                          # Incremental backup
│   ├── --no-incremental                       # Full backup (default)
│   └── --property <key=value>                 # Metadata (repeat)
│
├── delete              # Delete backup(s)
│   ├── <backup> [<backup> ...]                # (positional) Backup(s)
│   └── --force                                # Force delete
│
├── list                # List backups
│   ├── --all-projects                         # All projects
│   ├── --name <name>                          # Filter by name
│   ├── --status <status>                      # Filter by status
│   ├── --volume <volume>                      # Filter by volume
│   ├── --long                                 # Additional fields
│   ├── --limit <limit>                        # Max entries
│   └── --marker <marker>                      # Pagination marker
│
├── restore             # Restore backup to volume
│   ├── <backup>                               # (positional) Backup (name or ID)
│   ├── <volume>                               # (positional) Target volume (name or ID)
│   └── --force                                # Force overwrite existing volume
│
├── set                 # Set backup properties
│   ├── <backup>                               # (positional) Backup name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --state <state>                        # Override state (admin)
│   └── --no-property                          # Clear metadata
│
├── show                # Show backup details
│   └── <backup>                               # (positional) Backup name or ID
│
├── unset               # Unset backup properties
│   ├── <backup>                               # (positional) Backup name or ID
│   └── --property <key>                       # Remove metadata (repeat)
│
├── record export       # Export backup record (admin)
│   └── <backup>                               # (positional) Backup name or ID
│
└── record import       # Import backup record (admin)
    └── <record>                               # (positional) Backup record data
```

---

## openstack volume type

> Volume types.

```
openstack volume type
├── create              # Create volume type
│   ├── <name>                                 # (positional) Type name
│   ├── --description <desc>                   # Description
│   ├── --public | --private                   # Access level
│   ├── --property <key=value>                 # Extra spec (repeat)
│   ├── --project <project>                    # Project (for private)
│   ├── --encryption-provider <provider>       # Encryption provider class
│   ├── --encryption-cipher <cipher>           # Encryption cipher
│   ├── --encryption-key-size <bits>           # Encryption key size
│   └── --encryption-control-location <loc>    # front-end or back-end
│
├── delete              # Delete volume type(s)
│   └── <type> [<type> ...]                    # (positional) Type(s)
│
├── list                # List volume types
│   ├── --long                                 # Additional fields
│   ├── --public | --private                   # Filter by access
│   ├── --default                              # Show default type
│   ├── --encryption-type                      # Show encryption info
│   ├── --limit <limit>                        # Max entries
│   └── --marker <marker>                      # Pagination marker
│
├── set                 # Set volume type properties
│   ├── <type>                                 # (positional) Type name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --property <key=value>                 # Set extra spec (repeat)
│   ├── --project <project>                    # Add project access
│   ├── --encryption-provider <provider>       # Encryption provider
│   ├── --encryption-cipher <cipher>           # Encryption cipher
│   ├── --encryption-key-size <bits>           # Encryption key size
│   └── --encryption-control-location <loc>    # Control location
│
├── show                # Show volume type details
│   ├── <type>                                 # (positional) Type name or ID
│   └── --encryption-type                      # Show encryption info
│
└── unset               # Unset volume type properties
    ├── <type>                                 # (positional) Type name or ID
    ├── --property <key>                       # Remove extra spec (repeat)
    ├── --project <project>                    # Remove project access
    └── --encryption-type                      # Remove encryption
```

---

## openstack volume group

> Volume groups.

```
openstack volume group
├── create              # Create volume group
│   ├── --volume-group-type <type>             # Group type
│   ├── --volume-type <type>                   # Volume type(s) (repeat)
│   ├── --name <name>                          # Group name
│   ├── --description <desc>                   # Description
│   └── --availability-zone <zone>             # AZ
│
├── delete              # Delete volume group(s)
│   ├── <group> [<group> ...]                  # (positional) Group(s)
│   └── --force                                # Force delete with volumes
│
├── failover            # Failover replication group
│   ├── <group>                                # (positional) Group name or ID
│   └── --allow-attached-volume                # Allow attached volumes
│
├── list                # List volume groups
│   └── --all-projects                         # All projects (admin)
│
├── set                 # Set volume group properties
│   ├── <group>                                # (positional) Group name or ID
│   ├── --name <name>                          # New name
│   └── --description <desc>                   # Description
│
├── show                # Show volume group
│   └── <group>                                # (positional) Group name or ID
│
├── snapshot create     # Create group snapshot
│   ├── <group>                                # (positional) Group name or ID
│   ├── --name <name>                          # Snapshot name
│   └── --description <desc>                   # Description
│
├── snapshot delete     # Delete group snapshot(s)
│   └── <snapshot> [<snapshot> ...]            # (positional) Snapshot(s)
│
├── snapshot list       # List group snapshots
│   └── --all-projects                         # All projects (admin)
│
├── snapshot show       # Show group snapshot
│   └── <snapshot>                             # (positional) Snapshot name or ID
│
├── type create         # Create volume group type
│   ├── <name>                                 # (positional) Type name
│   ├── --description <desc>                   # Description
│   └── --group-spec <key=value>               # Group spec (repeat)
│
├── type delete         # Delete volume group type(s)
│   └── <type> [<type> ...]                    # (positional) Type(s)
│
├── type list           # List volume group types
│   └── (no additional flags)
│
├── type set            # Set volume group type properties
│   ├── <type>                                 # (positional) Type name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   └── --group-spec <key=value>               # Set spec (repeat)
│
└── type show           # Show volume group type
    └── <type>                                 # (positional) Type name or ID
```

---

## openstack volume qos

> Volume QoS specifications.

```
openstack volume qos
├── associate           # Associate QoS specs with volume type
│   ├── <qos-spec>                             # (positional) QoS spec name or ID
│   └── <volume-type>                          # (positional) Volume type
│
├── create              # Create QoS specs
│   ├── <name>                                 # (positional) QoS name
│   ├── --consumer <consumer>                  # Consumer: front-end, back-end, both
│   └── --property <key=value>                 # Spec property (repeat)
│
├── delete              # Delete QoS specs
│   ├── <qos-spec> [<qos-spec> ...]           # (positional) QoS spec(s)
│   └── --force                                # Force delete if in use
│
├── disassociate        # Disassociate QoS from volume type
│   ├── <qos-spec>                             # (positional) QoS spec name or ID
│   ├── --volume-type <type>                   # Specific type to disassociate
│   └── --all                                  # Disassociate from all types
│
├── list                # List QoS specs
│   └── (no additional flags)
│
├── set                 # Set QoS properties
│   ├── <qos-spec>                             # (positional) QoS name or ID
│   ├── --property <key=value>                 # Set property (repeat)
│   └── --consumer <consumer>                  # Consumer type
│
├── show                # Show QoS spec
│   └── <qos-spec>                             # (positional) QoS name or ID
│
└── unset               # Unset QoS properties
    ├── <qos-spec>                             # (positional) QoS name or ID
    └── --property <key>                       # Remove property (repeat)
```

---

## openstack volume transfer request

> Transfer volumes between projects.

```
openstack volume transfer request
├── accept              # Accept transfer request
│   ├── <transfer>                             # (positional) Transfer ID
│   └── <auth-key>                             # (positional) Authorization key
│
├── create              # Create transfer request
│   ├── <volume>                               # (positional) Volume (name or ID)
│   └── --name <name>                          # Transfer name
│
├── delete              # Delete transfer request(s)
│   └── <transfer> [<transfer> ...]            # (positional) Transfer(s)
│
├── list                # List transfer requests
│   └── --all-projects                         # All projects (admin)
│
└── show                # Show transfer request
    └── <transfer>                             # (positional) Transfer name or ID
```

---

## openstack image

> Glance images.

```
openstack image
├── create              # Create/upload image
│   ├── <image-name>                           # (positional) Image name
│   ├── --id <id>                              # Reserve specific ID
│   ├── --container-format <fmt>               # Format: ami, ari, aki, bare, docker, ova, ovf
│   ├── --disk-format <fmt>                    # Format: ami, ari, aki, vhd, vmdk, raw, qcow2, vhdx, vdi, iso, ploop
│   ├── --min-disk <gb>                        # Min disk (GB)
│   ├── --min-ram <mb>                         # Min RAM (MB)
│   ├── --file <file>                          # Upload from file
│   ├── --volume <volume>                      # Create from volume
│   ├── --force                                # Force with --volume (if in use)
│   ├── --progress                             # Show upload progress
│   ├── --sign-key-path <path>                 # Sign with private key
│   ├── --sign-cert-id <id>                    # Certificate for signature
│   ├── --protected | --unprotected            # Deletion protection
│   ├── --public | --private | --community | --shared
│   ├── --property <key=value>                 # Image property (repeat)
│   ├── --tag <tag>                            # Tag (repeat)
│   ├── --project <project>                    # Owner project
│   ├── --import                               # Use glance import
│   └── --project-domain <domain>              # Project domain
│
├── delete              # Delete image(s)
│   └── <image> [<image> ...]                  # (positional) Image(s) name or ID
│
├── list                # List images
│   ├── --public | --private | --community | --shared | --all
│   ├── --property <key=value>                 # Filter by property (repeat)
│   ├── --name <name>                          # Filter by name
│   ├── --status <status>                      # Filter by status
│   ├── --member-status <status>               # Filter: accepted, pending, rejected, all
│   ├── --project <project>                    # Filter by project (admin)
│   ├── --tag <tag>                            # Filter by tag (repeat)
│   ├── --hidden                               # Show hidden images
│   ├── --long                                 # Additional fields
│   ├── --sort <key>[:<dir>]                   # Sort order
│   ├── --limit <limit>                        # Max entries
│   └── --marker <marker>                      # Pagination marker
│
├── set                 # Set image properties
│   ├── <image>                                # (positional) Image name or ID
│   ├── --name <name>                          # New name
│   ├── --min-disk <gb>                        # Min disk
│   ├── --min-ram <mb>                         # Min RAM
│   ├── --container-format <fmt>               # Container format
│   ├── --disk-format <fmt>                    # Disk format
│   ├── --protected | --unprotected            # Protection
│   ├── --public | --private | --community | --shared
│   ├── --property <key=value>                 # Set property (repeat)
│   ├── --tag <tag>                            # Add tag (repeat)
│   ├── --architecture <arch>                  # Architecture
│   ├── --instance-id <id>                     # Instance ID
│   ├── --kernel-id <id>                       # Kernel image ID
│   ├── --os-distro <distro>                   # OS distribution
│   ├── --os-version <version>                 # OS version
│   ├── --ramdisk-id <id>                      # Ramdisk image ID
│   ├── --activate | --deactivate              # Activation state
│   ├── --project <project>                    # Owner project
│   └── --hidden | --unhidden                  # Hidden flag
│
├── show                # Show image details
│   ├── <image>                                # (positional) Image name or ID
│   └── --human-readable                       # Human-readable sizes
│
├── unset               # Unset image properties
│   ├── <image>                                # (positional) Image name or ID
│   ├── --property <key>                       # Remove property (repeat)
│   └── --tag <tag>                            # Remove tag (repeat)
│
├── save                # Save image to file
│   ├── <image>                                # (positional) Image name or ID
│   └── --file <file>                          # Output file
│
├── stage               # Stage image data for import
│   ├── <image>                                # (positional) Image ID
│   └── --file <file>                          # File to stage
│
├── import              # Import staged image
│   ├── <image>                                # (positional) Image ID
│   └── --method <method>                      # Import method
│
├── import info         # Show import info
│   └── (no flags)
│
├── add project         # Share image with project
│   ├── <image>                                # (positional) Image name or ID
│   └── <project>                              # (positional) Project (name or ID)
│
├── remove project      # Unshare image from project
│   ├── <image>                                # (positional) Image name or ID
│   └── <project>                              # (positional) Project (name or ID)
│
├── member get          # Get image member details
│   ├── <image>                                # (positional) Image
│   └── <project>                              # (positional) Project
│
├── member list         # List image members
│   └── <image>                                # (positional) Image name or ID
│
├── stores list         # List image stores
│   └── (no flags)
│
├── task list           # List image tasks
│   └── (no flags)
│
├── task show           # Show image task
│   └── <task>                                 # (positional) Task ID
│
├── metadef namespace create  # Create metadef namespace
├── metadef namespace delete  # Delete metadef namespace
├── metadef namespace list    # List metadef namespaces
├── metadef namespace set     # Set metadef namespace properties
├── metadef namespace show    # Show metadef namespace
├── metadef object create     # Create metadef object
├── metadef object delete     # Delete metadef object
├── metadef object list       # List metadef objects
├── metadef object show       # Show metadef object
├── metadef object update     # Update metadef object
├── metadef object property show  # Show metadef object property
├── metadef property create   # Create metadef property
├── metadef property delete   # Delete metadef property
├── metadef property list     # List metadef properties
├── metadef property set      # Set metadef property
├── metadef property show     # Show metadef property
├── metadef resource type list              # List metadef resource types
└── metadef resource type association create/delete/list  # Manage associations
```

---

## openstack cached image

> Image cache management (admin).

```
openstack cached image
├── clear               # Clear all cached images
├── delete              # Delete cached image
│   └── <image>                                # (positional) Image ID
├── list                # List cached images
└── queue               # Queue image for caching
    └── <image>                                # (positional) Image ID
```

---

## openstack user

> Identity users (Keystone).

```
openstack user
├── create              # Create user
│   ├── <name>                                 # (positional) Username
│   ├── --domain <domain>                      # Default domain
│   ├── --project <project>                    # Default project
│   ├── --project-domain <domain>              # Project domain
│   ├── --password <password>                  # Password
│   ├── --password-prompt                      # Prompt for password
│   ├── --email <email>                        # Email address
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Account state
│   ├── --or-show                              # Return existing if exists
│   ├── --ignore-lockout-failure-attempts      # Ignore lockout
│   ├── --ignore-password-expiry               # Ignore password expiry
│   ├── --ignore-change-password-upon-first-use
│   ├── --enable-lock-password                 # Lock password changes
│   ├── --disable-lock-password                # Unlock password changes
│   ├── --enable-multi-factor-auth             # Enable MFA
│   ├── --disable-multi-factor-auth            # Disable MFA
│   └── --multi-factor-auth-rule <rule>        # MFA rules (repeat)
│
├── delete              # Delete user(s)
│   └── <user> [<user> ...]                    # (positional) User(s) name or ID
│
├── list                # List users
│   ├── --domain <domain>                      # Filter by domain
│   ├── --project <project>                    # Filter by project
│   ├── --group <group>                        # Filter by group
│   └── --long                                 # Additional fields
│
├── set                 # Set user properties
│   ├── <user>                                 # (positional) User name or ID
│   ├── --name <name>                          # New name
│   ├── --domain <domain>                      # Domain
│   ├── --project <project>                    # Default project
│   ├── --password <password>                  # New password
│   ├── --password-prompt                      # Prompt for password
│   ├── --email <email>                        # Email
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Account state
│   ├── --ignore-lockout-failure-attempts | --no-ignore-lockout-failure-attempts
│   ├── --ignore-password-expiry | --no-ignore-password-expiry
│   ├── --ignore-change-password-upon-first-use | --no-ignore-change-password-upon-first-use
│   ├── --enable-lock-password | --disable-lock-password
│   ├── --enable-multi-factor-auth | --disable-multi-factor-auth
│   └── --multi-factor-auth-rule <rule>        # MFA rules (repeat)
│
├── show                # Show user details
│   └── <user>                                 # (positional) User name or ID
│
└── password set        # Change own password
    ├── --password <new-password>              # New password
    ├── --original-password <old-password>     # Current password
    └── --password-prompt                      # Prompt for passwords
```

---

## openstack project

> Identity projects/tenants (Keystone).

```
openstack project
├── create              # Create project
│   ├── <project-name>                         # (positional) Name
│   ├── --domain <domain>                      # Owning domain
│   ├── --parent <project>                     # Parent project
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Enable/disable
│   ├── --property <key=value>                 # Property (repeat)
│   ├── --or-show                              # Return existing
│   ├── --immutable | --no-immutable           # Immutable flag
│   └── --tag <tag>                            # Tag (repeat)
│
├── delete              # Delete project(s)
│   └── <project> [<project> ...]              # (positional) Project(s)
│
├── list                # List projects
│   ├── --domain <domain>                      # Filter by domain
│   ├── --parent <project>                     # Filter by parent
│   ├── --long                                 # Additional fields
│   ├── --my-projects                          # Only my projects
│   ├── --sort-column <col>                    # Sort by column
│   └── --tags <tag>                           # Filter by tags
│
├── set                 # Set project properties
│   ├── <project>                              # (positional) Project name or ID
│   ├── --name <name>                          # New name
│   ├── --domain <domain>                      # Domain
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Enable/disable
│   ├── --property <key=value>                 # Set property (repeat)
│   ├── --immutable | --no-immutable           # Immutable flag
│   └── --tag <tag>                            # Add tag (repeat)
│
├── show                # Show project details
│   ├── <project>                              # (positional) Project name or ID
│   └── --parents | --children | --domain      # Include hierarchy
│
└── cleanup             # Clean up project resources
    ├── <project>                              # (positional) Project (admin)
    ├── --dry-run                              # Show what would be deleted
    └── --auth-project                         # Clean current auth project
```

---

## openstack role

> Identity role-based access control (Keystone).

```
openstack role
├── create              # Create role
│   ├── <name>                                 # (positional) Role name
│   ├── --domain <domain>                      # Domain for role
│   ├── --description <desc>                   # Description
│   ├── --immutable | --no-immutable           # Immutable
│   └── --or-show                              # Return existing
│
├── delete              # Delete role(s)
│   └── <role> [<role> ...]                    # (positional) Role(s)
│
├── list                # List roles
│   └── --domain <domain>                      # Filter by domain
│
├── set                 # Set role properties
│   ├── <role>                                 # (positional) Role name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   └── --immutable | --no-immutable           # Immutable
│
├── show                # Show role details
│   └── <role>                                 # (positional) Role name or ID
│
├── add                 # Assign role to user/group on scope
│   ├── <role>                                 # (positional) Role (name or ID)
│   ├── --user <user> | --group <group>        # Target (required)
│   ├── --system <system>                      # System scope: all
│   ├── --domain <domain>                      # Domain scope
│   ├── --project <project>                    # Project scope
│   ├── --user-domain <domain>                 # User domain
│   ├── --group-domain <domain>                # Group domain
│   ├── --project-domain <domain>              # Project domain
│   ├── --inherited                            # Inheritable to sub-projects
│   └── --role-domain <domain>                 # Role domain
│
├── remove              # Remove role assignment
│   ├── <role>                                 # (positional) Role (name or ID)
│   ├── --user <user> | --group <group>        # Target (required)
│   ├── --system <system>                      # System scope
│   ├── --domain <domain>                      # Domain scope
│   ├── --project <project>                    # Project scope
│   ├── --user-domain <domain>                 # User domain
│   ├── --group-domain <domain>                # Group domain
│   ├── --project-domain <domain>              # Project domain
│   ├── --inherited                            # Inheritable flag
│   └── --role-domain <domain>                 # Role domain
│
└── assignment list     # List role assignments
    ├── --role <role>                          # Filter by role
    ├── --user <user>                          # Filter by user
    ├── --group <group>                        # Filter by group
    ├── --project <project>                    # Filter by project
    ├── --domain <domain>                      # Filter by domain
    ├── --system                               # System assignments only
    ├── --effective                            # Include inherited
    ├── --names                                # Show names not IDs
    ├── --role-domain <domain>                 # Role domain
    ├── --user-domain <domain>                 # User domain
    ├── --group-domain <domain>                # Group domain
    └── --project-domain <domain>              # Project domain
```

---

## openstack domain

> Identity domains (Keystone).

```
openstack domain
├── create              # Create domain
│   ├── <name>                                 # (positional) Domain name
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Enable/disable
│   ├── --immutable | --no-immutable           # Immutable
│   └── --or-show                              # Return existing
│
├── delete              # Delete domain(s) (must be disabled first)
│   └── <domain> [<domain> ...]                # (positional) Domain(s)
│
├── list                # List domains
│   ├── --name <name>                          # Filter by name
│   └── --enable | --disable                   # Filter by state
│
├── set                 # Set domain properties
│   ├── <domain>                               # (positional) Domain name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --enable | --disable                   # Enable/disable
│   └── --immutable | --no-immutable           # Immutable
│
└── show                # Show domain details
    └── <domain>                               # (positional) Domain name or ID
```

---

## openstack group

> Identity groups (Keystone).

```
openstack group
├── create              # Create group
│   ├── <name>                                 # (positional) Group name
│   ├── --domain <domain>                      # Domain
│   ├── --description <desc>                   # Description
│   └── --or-show                              # Return existing
│
├── delete              # Delete group(s)
│   └── <group> [<group> ...]                  # (positional) Group(s)
│
├── list                # List groups
│   ├── --domain <domain>                      # Filter by domain
│   ├── --user <user>                          # Groups for user
│   └── --long                                 # Additional fields
│
├── set                 # Set group properties
│   ├── <group>                                # (positional) Group name or ID
│   ├── --name <name>                          # New name
│   ├── --domain <domain>                      # Domain
│   └── --description <desc>                   # Description
│
├── show                # Show group details
│   └── <group>                                # (positional) Group name or ID
│
├── add user            # Add user to group
│   ├── <group>                                # (positional) Group name or ID
│   └── <user>                                 # (positional) User name or ID
│
├── remove user         # Remove user from group
│   ├── <group>                                # (positional) Group name or ID
│   └── <user>                                 # (positional) User name or ID
│
└── contains user       # Check if user is in group
    ├── <group>                                # (positional) Group name or ID
    └── <user>                                 # (positional) User name or ID
```

---

## openstack token

> Identity tokens (Keystone).

```
openstack token
├── issue               # Issue new token (using current credentials)
│   └── (no flags)
│
└── revoke              # Revoke token
    └── <token>                                # (positional) Token ID
```

---

## openstack credential

> Identity credentials (Keystone).

```
openstack credential
├── create              # Create credential
│   ├── <user>                                 # (positional) User
│   ├── <data>                                 # (positional) Credential data (JSON)
│   ├── --type <type>                          # Type: ec2, cert, totp
│   └── --project <project>                    # Project
│
├── delete              # Delete credential(s)
│   └── <credential> [<credential> ...]        # (positional) Credential ID(s)
│
├── list                # List credentials
│   ├── --user <user>                          # Filter by user
│   └── --type <type>                          # Filter by type
│
├── set                 # Set credential properties
│   ├── <credential>                           # (positional) Credential ID
│   ├── --user <user>                          # User
│   ├── --type <type>                          # Type
│   ├── --data <data>                          # Data
│   └── --project <project>                    # Project
│
└── show                # Show credential details
    └── <credential>                           # (positional) Credential ID
```

---

## openstack application credential

> Application credentials for service authentication.

```
openstack application credential
├── create              # Create application credential
│   ├── <name>                                 # (positional) Name
│   ├── --secret <secret>                      # Custom secret
│   ├── --role <role>                          # Role (repeat)
│   ├── --expiration <date>                    # Expiration (ISO 8601)
│   ├── --description <desc>                   # Description
│   ├── --unrestricted                         # Can create trusts/app creds
│   └── --access-rules <rules>                 # JSON access rules
│
├── delete              # Delete application credential(s)
│   └── <credential> [<credential> ...]        # (positional) Name or ID
│
├── list                # List application credentials
│   └── (no additional flags)
│
└── show                # Show application credential
    └── <credential>                           # (positional) Name or ID
```

---

## openstack endpoint

> Identity service endpoints (Keystone).

```
openstack endpoint
├── create              # Create endpoint
│   ├── <service>                              # (positional) Service (name or ID)
│   ├── <interface>                            # (positional) Interface: public, internal, admin
│   ├── <url>                                  # (positional) Endpoint URL
│   ├── --region <region>                      # Region
│   └── --enable | --disable                   # Enable/disable
│
├── delete              # Delete endpoint(s)
│   └── <endpoint> [<endpoint> ...]            # (positional) Endpoint ID(s)
│
├── list                # List endpoints
│   ├── --service <service>                    # Filter by service
│   ├── --interface <interface>                # Filter by interface
│   ├── --region <region>                      # Filter by region
│   └── --endpoint <endpoint>                  # Filter by endpoint
│
├── set                 # Set endpoint properties
│   ├── <endpoint>                             # (positional) Endpoint ID
│   ├── --interface <interface>                # New interface
│   ├── --url <url>                            # New URL
│   ├── --service <service>                    # New service
│   ├── --region <region>                      # Region
│   └── --enable | --disable                   # Enable/disable
│
├── show                # Show endpoint details
│   └── <endpoint>                             # (positional) Endpoint ID
│
├── add project         # Add endpoint to project
│   ├── <endpoint>                             # (positional) Endpoint
│   └── <project>                              # (positional) Project
│
├── remove project      # Remove endpoint from project
│   ├── <endpoint>                             # (positional) Endpoint
│   └── <project>                              # (positional) Project
│
├── group create        # Create endpoint group
│   ├── <name>                                 # (positional) Name
│   ├── --filter <filter>                      # Endpoint filter (JSON)
│   └── --description <desc>                   # Description
│
├── group delete        # Delete endpoint group
│   └── <group>                                # (positional) Group name or ID
│
├── group list          # List endpoint groups
│   └── (no additional flags)
│
├── group set           # Set endpoint group properties
│   ├── <group>                                # (positional) Group name or ID
│   ├── --name <name>                          # New name
│   ├── --filter <filter>                      # New filter
│   └── --description <desc>                   # Description
│
├── group show          # Show endpoint group
│   └── <group>                                # (positional) Group name or ID
│
├── group add project   # Add project to endpoint group
│   ├── <group>                                # (positional) Group
│   └── <project>                              # (positional) Project
│
└── group remove project  # Remove project from endpoint group
    ├── <group>                                # (positional) Group
    └── <project>                              # (positional) Project
```

---

## openstack service

> Identity services (Keystone).

```
openstack service
├── create              # Create service
│   ├── <type>                                 # (positional) Service type
│   ├── --name <name>                          # Service name
│   ├── --description <desc>                   # Description
│   └── --enable | --disable                   # Enable/disable
│
├── delete              # Delete service(s)
│   └── <service> [<service> ...]              # (positional) Service(s) name or ID
│
├── list                # List services
│   └── --long                                 # Additional fields
│
├── set                 # Set service properties
│   ├── <service>                              # (positional) Service name or ID
│   ├── --name <name>                          # New name
│   ├── --type <type>                          # New type
│   ├── --description <desc>                   # Description
│   └── --enable | --disable                   # Enable/disable
│
├── show                # Show service details
│   └── <service>                              # (positional) Service name or ID
│
├── provider create     # Create service provider
│   ├── <name>                                 # (positional) Name
│   ├── --auth-url <url>                       # Auth URL
│   ├── --service-provider-url <url>           # SP URL
│   ├── --description <desc>                   # Description
│   └── --enable | --disable                   # Enable/disable
│
├── provider delete     # Delete service provider(s)
│   └── <provider> [<provider> ...]            # (positional) Provider(s)
│
├── provider list       # List service providers
│   └── (no additional flags)
│
├── provider set        # Set service provider properties
│   ├── <provider>                             # (positional) Provider name or ID
│   ├── --auth-url <url>                       # Auth URL
│   ├── --service-provider-url <url>           # SP URL
│   ├── --description <desc>                   # Description
│   └── --enable | --disable                   # Enable/disable
│
└── provider show       # Show service provider
    └── <provider>                             # (positional) Provider name or ID
```

---

## openstack trust

> Identity trusts (delegated auth).

```
openstack trust
├── create              # Create trust
│   ├── <trustee-user>                         # (positional) Trustee user
│   ├── --project <project>                    # Project to delegate
│   ├── --role <role>                          # Role (repeat)
│   ├── --impersonate                          # Trustee impersonates trustor
│   ├── --expiration <date>                    # Expiration (ISO 8601)
│   ├── --trustor-domain <domain>              # Trustor domain
│   └── --trustee-domain <domain>              # Trustee domain
│
├── delete              # Delete trust(s)
│   └── <trust> [<trust> ...]                  # (positional) Trust ID(s)
│
├── list                # List trusts
│   ├── --trustor-user-id <id>                 # Filter by trustor
│   └── --trustee-user-id <id>                 # Filter by trustee
│
└── show                # Show trust details
    └── <trust>                                # (positional) Trust ID
```

---

## openstack object store

> Swift object storage.

```
openstack container
├── create              # Create container(s)
│   ├── <container-name> [...]                 # (positional) Container name(s)
│   ├── --public                               # Make publicly accessible
│   └── --storage-policy <policy>              # Storage policy
│
├── delete              # Delete container(s)
│   ├── <container> [<container> ...]          # (positional) Container(s)
│   └── --recursive                            # Delete objects within
│
├── list                # List containers
│   ├── --long                                 # Additional fields
│   ├── --prefix <prefix>                      # Filter by prefix
│   ├── --marker <marker>                      # Pagination marker
│   ├── --end-marker <marker>                  # End marker
│   ├── --limit <limit>                        # Max entries
│   └── --all                                  # List all (auto-paginate)
│
├── save                # Save container to local directory
│   └── <container>                            # (positional) Container name
│
├── set                 # Set container properties
│   ├── <container>                            # (positional) Container name
│   └── --property <key=value>                 # Set metadata (repeat)
│
├── show                # Show container details
│   └── <container>                            # (positional) Container name
│
└── unset               # Unset container properties
    ├── <container>                            # (positional) Container name
    └── --property <key>                       # Remove metadata (repeat)

openstack object
├── create              # Upload object(s)
│   ├── <container>                            # (positional) Container name
│   ├── <filename> [<filename> ...]            # (positional) Local file(s)
│   └── --name <name>                          # Custom object name (single file)
│
├── delete              # Delete object(s)
│   ├── <container>                            # (positional) Container name
│   └── <object> [<object> ...]                # (positional) Object name(s)
│
├── list                # List objects
│   ├── <container>                            # (positional) Container name
│   ├── --long                                 # Additional fields
│   ├── --prefix <prefix>                      # Filter by prefix
│   ├── --delimiter <delimiter>                # Delimiter
│   ├── --marker <marker>                      # Pagination marker
│   ├── --end-marker <marker>                  # End marker
│   ├── --limit <limit>                        # Max entries
│   └── --all                                  # List all
│
├── save                # Download object
│   ├── <container>                            # (positional) Container name
│   ├── <object>                               # (positional) Object name
│   └── --file <file>                          # Output file
│
├── set                 # Set object properties
│   ├── <container>                            # (positional) Container name
│   ├── <object>                               # (positional) Object name
│   └── --property <key=value>                 # Metadata (repeat)
│
├── show                # Show object metadata
│   ├── <container>                            # (positional) Container name
│   └── <object>                               # (positional) Object name
│
└── unset               # Unset object properties
    ├── <container>                            # (positional) Container name
    ├── <object>                               # (positional) Object name
    └── --property <key>                       # Remove metadata (repeat)

openstack object store account
├── set                 # Set account properties
│   └── --property <key=value>                 # Account metadata (repeat)
├── show                # Show account details
└── unset               # Unset account properties
    └── --property <key>                       # Remove metadata (repeat)
```

---

## openstack stack

> Heat orchestration stacks.

```
openstack stack
├── create              # Create stack
│   ├── <stack-name>                           # (positional) Stack name
│   ├── -t, --template <template>              # Template file (required)
│   ├── -e, --environment <env>                # Environment file (repeat)
│   ├── --parameter <key=value>                # Parameter (repeat)
│   ├── --parameter-file <key=file>            # Parameter from file (repeat)
│   ├── --timeout <minutes>                    # Creation timeout
│   ├── --enable-rollback                      # Rollback on failure
│   ├── --tags <tag1,tag2>                     # Tags (comma-separated)
│   ├── --dry-run                              # Show what would be created
│   ├── --wait                                 # Wait for completion
│   ├── --poll <seconds>                       # Poll interval (with --wait)
│   ├── --pre-create <resource>                # Pre-create hook (repeat)
│   └── -s, --files-container <container>      # Swift container for files
│
├── delete              # Delete stack(s)
│   ├── <stack> [<stack> ...]                  # (positional) Stack(s) name or ID
│   ├── --yes                                  # Skip confirmation
│   ├── --wait                                 # Wait for deletion
│   └── --poll <seconds>                       # Poll interval
│
├── list                # List stacks
│   ├── --nested                               # Include nested stacks
│   ├── --hidden                               # Include hidden stacks
│   ├── --deleted                              # Include deleted stacks
│   ├── --long                                 # Additional fields
│   ├── --property <key=value>                 # Filter by property
│   ├── --tags <tags>                          # Filter by tags
│   ├── --tag-mode <mode>                      # any, not, not-any
│   ├── --limit <limit>                        # Max entries
│   ├── --marker <marker>                      # Pagination marker
│   └── --sort <key>:<dir>                     # Sort order
│
├── show                # Show stack details
│   └── <stack>                                # (positional) Stack name or ID
│
├── update              # Update stack
│   ├── <stack>                                # (positional) Stack name or ID
│   ├── -t, --template <template>              # New template
│   ├── -e, --environment <env>                # Environment (repeat)
│   ├── --parameter <key=value>                # Parameter (repeat)
│   ├── --existing                             # Reuse existing parameters
│   ├── --clear-parameter <key>                # Clear parameter (repeat)
│   ├── --timeout <minutes>                    # Update timeout
│   ├── --enable-rollback | --disable-rollback
│   ├── --tags <tags>                          # Tags
│   ├── --dry-run                              # Show what would change
│   ├── --wait                                 # Wait for completion
│   └── --converge                             # Force convergence
│
├── abandon             # Abandon stack (remove without deleting resources)
│   ├── <stack>                                # (positional) Stack name or ID
│   └── --output-file <file>                   # Save adopt data to file
│
├── adopt               # Adopt existing resources into stack
│   ├── <stack-name>                           # (positional) Stack name
│   ├── -t, --template <template>              # Template
│   ├── -e, --environment <env>                # Environment (repeat)
│   ├── --adopt-file <file>                    # Adopt data file
│   └── --parameter <key=value>                # Parameter (repeat)
│
├── cancel              # Cancel stack operation
│   └── <stack>                                # (positional) Stack name or ID
│
├── check               # Check stack resources
│   └── <stack>                                # (positional) Stack name or ID
│
├── export              # Export stack data
│   └── <stack>                                # (positional) Stack name or ID
│
├── resume              # Resume suspended stack
│   └── <stack>                                # (positional) Stack name or ID
│
├── suspend             # Suspend stack
│   └── <stack>                                # (positional) Stack name or ID
│
├── template show       # Show stack template
│   └── <stack>                                # (positional) Stack name or ID
│
├── environment show    # Show stack environment
│   └── <stack>                                # (positional) Stack name or ID
│
├── failures list       # List stack failures
│   ├── <stack>                                # (positional) Stack name or ID
│   └── --long                                 # Additional fields
│
├── file list           # List stack files
│   └── <stack>                                # (positional) Stack name or ID
│
├── hook clear          # Clear stack hooks
│   ├── <stack>                                # (positional) Stack name or ID
│   └── <resource> [<resource> ...]            # (positional) Resources
│
├── hook poll           # Poll stack hooks
│   ├── <stack>                                # (positional) Stack name or ID
│   └── --nested-depth <depth>                 # Nested stack depth
│
├── event list          # List stack events
│   ├── <stack>                                # (positional) Stack name or ID
│   ├── --resource <resource>                  # Filter by resource
│   ├── --nested-depth <depth>                 # Include nested
│   ├── --sort <key>:<dir>                     # Sort order
│   ├── --limit <limit>                        # Max entries
│   └── --marker <marker>                      # Marker
│
├── event show          # Show stack event
│   ├── <stack>                                # (positional) Stack name or ID
│   ├── <resource>                             # (positional) Resource name
│   └── <event>                                # (positional) Event ID
│
├── output list         # List stack outputs
│   └── <stack>                                # (positional) Stack name or ID
│
├── output show         # Show stack output value
│   ├── <stack>                                # (positional) Stack name or ID
│   ├── <output>                               # (positional) Output key
│   └── --all                                  # Show all outputs
│
├── resource list       # List stack resources
│   ├── <stack>                                # (positional) Stack name or ID
│   ├── --nested-depth <depth>                 # Include nested
│   ├── --long                                 # Additional fields
│   └── --filter <key=value>                   # Filter (repeat)
│
├── resource show       # Show stack resource
│   ├── <stack>                                # (positional) Stack name or ID
│   └── <resource>                             # (positional) Resource name
│
├── resource mark unhealthy  # Mark resource unhealthy
│   ├── <stack>                                # (positional) Stack
│   ├── <resource>                             # (positional) Resource
│   └── <reason>                               # (positional) Reason
│
├── resource metadata   # Show resource metadata
│   ├── <stack>                                # (positional) Stack
│   └── <resource>                             # (positional) Resource
│
├── resource signal     # Signal a resource
│   ├── <stack>                                # (positional) Stack
│   ├── <resource>                             # (positional) Resource
│   └── --data <data>                          # Signal data (JSON)
│
├── snapshot create     # Create stack snapshot
│   ├── <stack>                                # (positional) Stack name or ID
│   └── --name <name>                          # Snapshot name
│
├── snapshot delete     # Delete stack snapshot
│   ├── <stack>                                # (positional) Stack
│   └── <snapshot>                             # (positional) Snapshot ID
│
├── snapshot list       # List stack snapshots
│   └── <stack>                                # (positional) Stack name or ID
│
├── snapshot restore    # Restore stack snapshot
│   ├── <stack>                                # (positional) Stack
│   └── <snapshot>                             # (positional) Snapshot ID
│
└── snapshot show       # Show stack snapshot
    ├── <stack>                                # (positional) Stack
    └── <snapshot>                             # (positional) Snapshot ID
```

---

## openstack zone

> DNS zones (Designate).

```
openstack zone
├── create              # Create zone
│   ├── <name>                                 # (positional) Zone name (FQDN)
│   ├── --email <email>                        # Admin email (required)
│   ├── --type {PRIMARY,SECONDARY}             # Zone type
│   ├── --ttl <seconds>                        # Default TTL
│   ├── --description <desc>                   # Description
│   └── --masters <masters>                    # Zone masters (for SECONDARY)
│
├── delete              # Delete zone
│   └── <zone>                                 # (positional) Zone name or ID
│
├── list                # List zones
│   ├── --type <type>                          # Filter by type
│   ├── --name <name>                          # Filter by name
│   ├── --status <status>                      # Filter by status
│   └── --all-projects                         # All projects
│
├── set                 # Set zone properties
│   ├── <zone>                                 # (positional) Zone name or ID
│   ├── --email <email>                        # Admin email
│   ├── --ttl <seconds>                        # TTL
│   ├── --description <desc>                   # Description
│   └── --masters <masters>                    # Masters
│
├── show                # Show zone details
│   └── <zone>                                 # (positional) Zone name or ID
│
├── abandon             # Abandon zone (remove from Designate without DNS delete)
│   └── <zone>                                 # (positional) Zone ID
│
├── axfr                # Trigger AXFR for secondary zone
│   └── <zone>                                 # (positional) Zone ID
│
├── move                # Move zone to different project
│   ├── <zone>                                 # (positional) Zone ID
│   └── --project-id <project>                 # Target project
│
├── blacklist create    # Create zone blacklist pattern
│   ├── --pattern <pattern>                    # Regex pattern
│   └── --description <desc>                   # Description
│
├── blacklist delete    # Delete zone blacklist
│   └── <blacklist>                            # (positional) Blacklist ID
│
├── blacklist list      # List zone blacklists
├── blacklist set       # Set zone blacklist properties
│   ├── <blacklist>                            # (positional) Blacklist ID
│   ├── --pattern <pattern>                    # Pattern
│   └── --description <desc>                   # Description
│
├── blacklist show      # Show zone blacklist
│   └── <blacklist>                            # (positional) Blacklist ID
│
├── export create       # Create zone export
│   └── <zone>                                 # (positional) Zone ID
│
├── export delete       # Delete zone export
│   └── <export>                               # (positional) Export ID
│
├── export list         # List zone exports
├── export show         # Show zone export
│   └── <export>                               # (positional) Export ID
│
├── export showfile     # Show exported zone file
│   └── <export>                               # (positional) Export ID
│
├── import create       # Import zone from file
│   └── <file>                                 # (positional) Zone file
│
├── import delete       # Delete zone import
│   └── <import>                               # (positional) Import ID
│
├── import list         # List zone imports
├── import show         # Show zone import
│   └── <import>                               # (positional) Import ID
│
├── share create        # Share zone with project
│   ├── <zone>                                 # (positional) Zone ID
│   └── --target-project-id <project>          # Target project
│
├── share delete        # Delete zone share
│   ├── <zone>                                 # (positional) Zone ID
│   └── <share>                                # (positional) Share ID
│
├── share list          # List zone shares
│   └── <zone>                                 # (positional) Zone ID
│
├── share show          # Show zone share
│   ├── <zone>                                 # (positional) Zone ID
│   └── <share>                                # (positional) Share ID
│
├── transfer request create  # Create zone transfer request
│   ├── <zone>                                 # (positional) Zone ID
│   ├── --target-project-id <project>          # Target project
│   └── --description <desc>                   # Description
│
├── transfer request delete  # Delete transfer request
│   └── <request>                              # (positional) Request ID
│
├── transfer request list    # List transfer requests
├── transfer request set     # Set transfer request properties
│   ├── <request>                              # (positional) Request ID
│   └── --description <desc>                   # Description
│
├── transfer request show    # Show transfer request
│   └── <request>                              # (positional) Request ID
│
├── transfer accept list     # List transfer accepts
├── transfer accept request  # Accept transfer request
│   ├── <request-id>                           # (positional) Request ID
│   └── <key>                                  # (positional) Transfer key
│
└── transfer accept show     # Show transfer accept
    └── <accept>                               # (positional) Accept ID
```

---

## openstack recordset

> DNS records (Designate).

```
openstack recordset
├── create              # Create recordset
│   ├── <zone-id>                              # (positional) Zone ID
│   ├── <name>                                 # (positional) Record name
│   ├── --type <type>                          # Record type: A, AAAA, CNAME, MX, NS, TXT, SRV, etc.
│   ├── --record <record>                      # Record data (repeat for multiple)
│   ├── --ttl <seconds>                        # TTL
│   └── --description <desc>                   # Description
│
├── delete              # Delete recordset
│   ├── <zone-id>                              # (positional) Zone ID
│   └── <recordset>                            # (positional) Recordset ID or name
│
├── list                # List recordsets
│   ├── <zone-id>                              # (positional) Zone ID (optional for all zones)
│   ├── --type <type>                          # Filter by type
│   ├── --name <name>                          # Filter by name
│   ├── --status <status>                      # Filter by status
│   └── --all-projects                         # All projects
│
├── set                 # Set recordset properties
│   ├── <zone-id>                              # (positional) Zone ID
│   ├── <recordset>                            # (positional) Recordset ID
│   ├── --record <record>                      # Record data (repeat, replaces all)
│   ├── --ttl <seconds>                        # TTL
│   └── --description <desc>                   # Description
│
└── show                # Show recordset details
    ├── <zone-id>                              # (positional) Zone ID
    └── <recordset>                            # (positional) Recordset ID or name
```

---

## openstack loadbalancer

> Octavia load balancers.

```
openstack loadbalancer
├── create              # Create load balancer
│   ├── --name <name>                          # LB name
│   ├── --description <desc>                   # Description
│   ├── --vip-address <ip>                     # VIP address
│   ├── --vip-port-id <port>                   # VIP port (name or ID)
│   ├── --vip-subnet-id <subnet>               # VIP subnet (name or ID)
│   ├── --vip-network-id <network>             # VIP network (name or ID)
│   ├── --vip-qos-policy-id <policy>           # QoS policy
│   ├── --additional-vip subnet-id=<s>[,ip-address=<ip>]
│   ├── --vip-sg-id <sg>                       # Security group for VIP (repeat)
│   ├── --project <project>                    # Owner project
│   ├── --provider <provider>                  # Provider name
│   ├── --availability-zone <zone>             # AZ
│   ├── --flavor <flavor>                      # Flavor (name or ID)
│   ├── --enable | --disable                   # Admin state
│   ├── --wait                                 # Wait for active
│   ├── --tag <tag>                            # Tag (repeat)
│   └── --no-tag                               # No tags
│
├── delete              # Delete load balancer
│   ├── <lb>                                   # (positional) LB name or ID
│   ├── --cascade                              # Delete all child objects
│   └── --wait                                 # Wait for deletion
│
├── list                # List load balancers
│   ├── --name <name>                          # Filter by name
│   ├── --enable | --disable                   # Filter by state
│   ├── --project <project>                    # Filter by project
│   ├── --vip-network-id <network>             # Filter by VIP network
│   ├── --vip-subnet-id <subnet>               # Filter by VIP subnet
│   ├── --vip-port-id <port>                   # Filter by VIP port
│   ├── --provisioning-status <status>         # ACTIVE, ERROR, PENDING_*
│   ├── --operating-status <status>            # ONLINE, OFFLINE, DEGRADED, ERROR
│   ├── --provider <provider>                  # Filter by provider
│   ├── --flavor <flavor>                      # Filter by flavor
│   ├── --availability-zone <zone>             # Filter by AZ
│   └── --tags <tag>[,<tag>,...]               # Filter by tags
│
├── set                 # Set LB properties
│   ├── <lb>                                   # (positional) LB name or ID
│   ├── --name <name>                          # New name
│   ├── --description <desc>                   # Description
│   ├── --vip-qos-policy-id <policy>           # QoS policy
│   ├── --enable | --disable                   # Admin state
│   ├── --tag <tag>                            # Add tag (repeat)
│   └── --wait                                 # Wait for active
│
├── show                # Show LB details
│   └── <lb>                                   # (positional) LB name or ID
│
├── unset               # Unset LB properties
│   ├── <lb>                                   # (positional) LB name or ID
│   ├── --vip-qos-policy-id                    # Remove QoS
│   └── --tag <tag>                            # Remove tag (repeat)
│
├── failover            # Failover load balancer
│   ├── <lb>                                   # (positional) LB name or ID
│   └── --wait                                 # Wait for active
│
├── stats show          # Show LB statistics
│   └── <lb>                                   # (positional) LB name or ID
│
├── status show         # Show LB status tree
│   └── <lb>                                   # (positional) LB name or ID
│
├── listener create/delete/list/set/show/unset/stats show
├── pool create/delete/list/set/show/unset
├── member create/delete/list/set/show/unset
├── healthmonitor create/delete/list/set/show/unset
├── l7policy create/delete/list/set/show/unset
├── l7rule create/delete/list/set/show/unset
├── amphora configure/delete/failover/list/show/stats show
├── flavor create/delete/list/set/show/unset
├── flavorprofile create/delete/list/set/show
├── availabilityzone create/delete/list/set/show/unset
├── availabilityzoneprofile create/delete/list/set/show
├── provider list
├── provider capability list
└── quota defaults show/list/reset/set/show/unset
```

---

## openstack baremetal

> Ironic bare metal provisioning (summary).

```
openstack baremetal
├── allocation create/delete/list/set/show/unset
├── chassis create/delete/list/set/show/unset
├── conductor list/show
├── create                                     # Create baremetal node (shortcut)
├── deploy template create/delete/list/set/show/unset
├── driver list/show/passthru call/passthru list/property list/raid property list
├── inspection rule create/delete/list/set/show/unset
├── node
│   ├── abort                                  # Abort provisioning
│   ├── add trait / remove trait               # Manage traits
│   ├── adopt                                  # Adopt existing hardware
│   ├── bios setting list/show                 # BIOS settings
│   ├── boot device set/show                   # Boot device
│   ├── boot mode set                          # Boot mode (UEFI/BIOS)
│   ├── children list                          # List child nodes
│   ├── clean                                  # Initiate cleaning
│   ├── console enable/disable/show            # Serial console
│   ├── create/delete                          # Create/delete node
│   ├── deploy/undeploy                        # Deploy/undeploy instance
│   ├── firmware list                          # List firmware
│   ├── history get/list                       # Provisioning history
│   ├── inject nmi                             # Inject NMI
│   ├── inspect                                # Hardware inspection
│   ├── inventory save                         # Save hardware inventory
│   ├── list                                   # List nodes
│   ├── maintenance set/unset                  # Maintenance mode
│   ├── manage/provide                         # State transitions
│   ├── passthru call/list                     # Vendor passthrough
│   ├── power off/on                           # Power management
│   ├── reboot/rebuild                         # Reboot/rebuild
│   ├── rescue/unrescue                        # Rescue mode
│   ├── secure boot on/off                     # Secure boot
│   ├── service                                # Service mode
│   ├── set/unset/show                         # Properties
│   ├── trait list                             # List traits
│   ├── unhold                                 # Release hold
│   ├── validate                               # Validate interfaces
│   └── vif attach/detach/list                 # Virtual interfaces
├── port create/delete/list/set/show/unset
├── port group create/delete/list/set/show/unset
├── runbook create/delete/list/set/show/unset
├── shard list
├── volume connector create/delete/list/set/show/unset
└── volume target create/delete/list/set/show/unset
```

---

## openstack coe

> Magnum container orchestration engine (Kubernetes clusters).

```
openstack coe
├── ca rotate                                  # Rotate CA certificate
├── ca show                                    # Show CA certificate
├── ca sign                                    # Sign certificate
├── cluster create      # Create cluster
│   ├── --cluster-template <template>          # Template (required)
│   ├── --node-count <n>                       # Worker node count
│   ├── --master-count <n>                     # Master node count
│   ├── --keypair <keypair>                    # SSH keypair
│   ├── --docker-volume-size <gb>              # Docker volume size
│   ├── --labels <key=value>                   # Labels (repeat)
│   ├── --timeout <minutes>                    # Creation timeout
│   └── <name>                                 # (positional) Cluster name
│
├── cluster delete      # Delete cluster(s)
├── cluster list        # List clusters
├── cluster show        # Show cluster details
├── cluster update      # Update cluster
├── cluster resize      # Resize cluster
├── cluster upgrade     # Upgrade cluster
├── cluster config      # Get cluster kubeconfig
│   ├── <cluster>                              # (positional) Cluster
│   └── --dir <directory>                      # Output directory
│
├── cluster template create/delete/list/show/update
├── credential rotate   # Rotate cluster credentials
├── nodegroup create/delete/list/show/update
├── quotas create/delete/list/show/update
├── service list        # List Magnum services
└── stats list          # List cluster stats
```

---

## openstack share

> Manila shared file systems (summary).

```
openstack share
├── create/delete/list/set/show/unset          # Share CRUD
├── adopt/resize/restore/revert                # Lifecycle operations
├── access create/delete/list/set/show/unset   # Access rules
├── availability zone list                     # List AZs
├── backup create/delete/list/restore/set/show/unset
├── export location list/set/show/unset        # Export locations
├── group create/delete/list/set/show/unset    # Share groups
├── group snapshot create/delete/list/members list/set/show/unset
├── group type create/delete/list/set/show/unset
├── group type access create/delete/list
├── instance delete/list/set/show              # Share instances
├── instance export location list/show
├── limits show                                # Service limits
├── lock create/delete/list/set/show/unset     # Share locks
├── message delete/list/show                   # User messages
├── migration cancel/complete/show/start       # Share migration
├── network create/delete/list/set/show/unset  # Share networks
├── network subnet create/delete/set/show/unset
├── pool list                                  # Storage pools
├── properties show                            # Share properties
├── qos type create/delete/list/set/show/unset # QoS types
├── quota delete/set/show                      # Quotas
├── replica create/delete/list/promote/resync/set/show/unset
├── replica export location list/show
├── security service create/delete/list/set/show/unset
├── server abandon/adopt/delete/list/set/show  # Share servers
├── server migration cancel/complete/show/start
├── service ensure shares/list/set             # Manila services
├── snapshot abandon/adopt/create/delete/list/set/show/unset
├── snapshot access create/delete/list
├── snapshot export location list/show
├── snapshot instance export location list/show
├── snapshot instance list/set/show
├── transfer accept/create/delete/list/show    # Transfer ownership
├── type create/delete/list/set/show/unset     # Share types
└── type access create/delete/list             # Type access control
```

---

## openstack workflow

> Mistral workflow engine (summary).

```
openstack workflow
├── create/delete/list/show/update/validate    # Workflow CRUD
├── definition show                            # Show workflow definition
├── execution create/delete/list/show/update   # Workflow executions
│   ├── execution input show                   # Show execution input
│   ├── execution output show                  # Show execution output
│   ├── execution published show               # Show published variables
│   └── execution report show                  # Show execution report
├── env create/delete/list/show/update         # Workflow environments
│
openstack workbook
├── create/delete/list/show/update/validate    # Workbook CRUD
└── definition show                            # Show workbook definition
│
openstack action definition
├── create/delete/list/show/update             # Action definitions
└── definition show                            # Show action definition source
│
openstack action execution
├── delete/list/show/update                    # Action executions
├── input show/output show                     # Input/output
└── run                                        # Run ad-hoc action
│
openstack task execution
├── list/show                                  # Task executions
├── published show                             # Published variables
├── rerun                                      # Re-run failed task
└── result show                                # Task result
│
openstack cron trigger
├── create/delete/list/show                    # Scheduled triggers
│
openstack event trigger
├── create/delete/list/show                    # Event-based triggers
│
openstack code source
├── content show/create/delete/list/show/update  # Code sources
│
openstack dynamic action
├── create/delete/list/show/update             # Dynamic actions
│
openstack resource member
└── create/delete/list/show/update             # Resource sharing
```

---

## openstack rating

> CloudKitty rating/billing (summary).

```
openstack rating
├── collector enable/state get                 # Collector management
├── collector-mapping create/delete/get/list   # Collector mappings
├── dataframes add/get                         # Rating dataframes
├── hashmap field create/delete/get/list       # Hashmap fields
├── hashmap group create/delete/list/mappings get/thresholds get
├── hashmap mapping create/delete/get/list/update
├── hashmap mapping-types list
├── hashmap service create/delete/get/list     # Hashmap services
├── hashmap threshold create/delete/get/list/update
├── info config get/metric get/metric list     # Rating info
├── module disable/enable/get/list/set priority  # Rating modules
├── pyscript create/delete/get/list/update     # Python scripts
├── report tenant list                         # Tenant reports
├── scope patch/state get/state reset          # Scope management
├── summary get                                # Usage summary
└── tasks reprocessing create/get              # Reprocessing tasks
```

---

## openstack secret

> Barbican key manager (summary).

```
openstack secret
├── store               # Store a secret
│   ├── --name <name>                          # Secret name
│   ├── --payload <data>                       # Secret payload
│   ├── --payload-content-type <type>          # Content type
│   ├── --payload-content-encoding <enc>       # Encoding (e.g. base64)
│   ├── --algorithm <algo>                     # Algorithm
│   ├── --bit-length <bits>                    # Key length
│   ├── --mode <mode>                          # Mode (e.g. cbc)
│   ├── --secret-type <type>                   # Type: symmetric, public, private, passphrase, certificate, opaque
│   └── --expiration <date>                    # Expiration (ISO 8601)
│
├── get                 # Get secret metadata
├── list                # List secrets
├── delete              # Delete secret
├── update              # Update secret payload
├── order create        # Create secret generation order
├── order delete/get/list
├── container create/delete/get/list           # Secret containers
├── consumer create/delete/list                # Secret consumers
│
openstack ca
├── get                 # Get CA details
└── list                # List CAs
│
openstack acl
├── delete              # Delete ACL
├── get                 # Get ACL
├── submit              # Submit/create ACL
├── user add            # Add user to ACL
└── user remove         # Remove user from ACL
```

---

## openstack resource provider

> Placement service (summary).

```
openstack resource provider
├── create/delete/list/set/show                # Resource providers
├── aggregate list/set                         # Provider aggregates
├── allocation delete/set/show/unset           # Allocations
├── inventory class set/delete/list/set/show   # Inventories
├── trait delete/list/set                      # Provider traits
└── usage show                                 # Provider usage
│
openstack resource class
├── create/delete/list/set/show                # Resource classes
│
openstack resource usage show                  # Consumer usage
│
openstack allocation candidate list            # Find placement candidates
│
openstack trait
├── create/delete/list/show                    # Custom traits
```

---

## openstack vpn

> VPN as a Service (summary).

```
openstack vpn
├── endpoint group create/delete/list/set/show
├── ike policy create/delete/list/set/show
├── ipsec policy create/delete/list/set/show
├── ipsec site connection create/delete/list/set/show
└── service create/delete/list/set/show
```

---

## openstack bgp

> Dynamic routing (summary).

```
openstack bgp
├── dragent add speaker/list/remove speaker
├── peer create/delete/list/set/show
└── speaker add network/add peer/create/delete/list/list advertised routes/remove network/remove peer/set/show
```

---

## openstack bgpvpn

> BGP VPN interconnection (summary).

```
openstack bgpvpn
├── create/delete/list/set/show/unset
├── network association create/delete/list/show
├── port association create/delete/list/set/show/unset
└── router association create/delete/list/set/show/unset
```

---

## openstack sfc

> Service Function Chaining (summary).

```
openstack sfc
├── flow classifier create/delete/list/set/show
├── port chain create/delete/list/set/show/unset
├── port pair create/delete/list/set/show
├── port pair group create/delete/list/set/show/unset
└── service graph create/delete/list/set/show
```

---

## openstack tap

> Tap as a Service (summary).

```
openstack tap
├── flow create/delete/list/show/update
├── mirror create/delete/list/show/update
└── service create/delete/list/show/update
```

---

## openstack local ip

> Local IP (summary).

```
openstack local ip
├── create/delete/list/set/show
└── association create/delete/list
```

---

## openstack ip availability

> IP address availability.

```
openstack ip availability
├── list                # List network IP availability
└── show                # Show network IP availability
    └── <network>                              # (positional) Network name or ID
```

---

## Common Commands

```
openstack availability zone list               # List availability zones
openstack catalog list                         # List service catalog
openstack catalog show <service>               # Show service endpoints
openstack command list                         # List all available commands
openstack configuration show                   # Show client configuration
openstack extension list                       # List API extensions
openstack extension show <extension>           # Show extension details
openstack limits show                          # Show rate/absolute limits
│   ├── --absolute                             # Absolute limits only
│   ├── --rate                                 # Rate limits only
│   └── --project <project>                    # Project
openstack module list                          # List installed plugins
openstack quota show [<project>]               # Show quotas
openstack quota set <project>                  # Set quotas (many --<resource> flags)
openstack quota list                           # List quotas
openstack quota delete <project>               # Reset quotas to default
openstack usage list                           # List usage for all projects
openstack usage show [<project>]               # Show project usage
openstack versions show                        # Show API versions
```

---

## Global Flags (available on all commands)

```
--os-cloud <cloud-config-name>               # Named cloud from clouds.yaml
--os-region-name <region>                    # Region name
--os-cacert <ca-bundle-file>                 # CA certificate bundle
--os-cert <certificate-file>                 # Client certificate
--os-key <key-file>                          # Client key
--verify | --insecure                        # SSL verification
--os-default-domain <domain>                 # Default domain
--os-interface <interface>                    # public, internal, admin
--os-service-provider <provider>             # Service provider
--os-remote-project-name <name>              # Remote project name
--os-remote-project-id <id>                  # Remote project ID
--os-remote-project-domain-name <name>       # Remote project domain name
--os-remote-project-domain-id <id>           # Remote project domain ID
--os-endpoint-override <url>                 # Override service endpoint
--os-beta-command                            # Enable beta commands

# API Version Overrides
--os-compute-api-version <version>           # Compute (Nova) API version
--os-identity-api-version <version>          # Identity (Keystone) API version
--os-image-api-version <version>             # Image (Glance) API version
--os-network-api-version <version>           # Network (Neutron) API version
--os-object-api-version <version>            # Object Storage (Swift) API version
--os-volume-api-version <version>            # Volume (Cinder) API version
--os-placement-api-version <version>         # Placement API version
--os-workflow-api-version <version>           # Workflow (Mistral) API version
--os-container-infra-api-version <version>   # Container Infra (Magnum) API version
--os-share-api-version <version>             # Shared FS (Manila) API version
--os-orchestration-api-version <version>     # Orchestration (Heat) API version
--os-baremetal-api-version <version>         # Baremetal (Ironic) API version
--rating-api-version <version>               # Rating (CloudKitty) API version

# Output Formatting
-f, --format {table,json,yaml,csv,value,shell}  # Output format (default: table)
-c, --column <column>                        # Column(s) to include (repeat)
--sort-column <column>                       # Sort by column (repeat)
--sort-ascending | --sort-descending         # Sort direction
--noindent                                   # Don't indent JSON output
--max-width <integer>                        # Max table width (0=disable)
--fit-width                                  # Fit table to terminal
--print-empty                                # Print empty table
--prefix <prefix>                            # Prefix for shell format
--quote {all,minimal,none,nonnumeric}        # CSV quoting style

# Debugging
--debug                                      # Full debug output
-v, --verbose                                # Increase verbosity (repeat)
-q, --quiet                                  # Suppress output
--log-file <file>                            # Log to file
--timing                                     # Print API timing
```

---

## Limitations

1. **Authentication required for all commands** — no offline mode; every command hits the API
2. **Plugin availability varies** — commands depend on which client plugins are installed; missing plugins silently hide commands
3. **API microversion sensitivity** — some flags/features only work with specific API versions (noted in help as "v2.XX or above")
4. **No built-in watch/polling** — only some commands support `--wait`; no universal equivalent
5. **Large output not auto-paginated** — must use `--limit` and `--marker` manually for large listings
6. **No bulk create** — most create commands operate on one resource at a time (delete sometimes accepts multiple)
7. **clouds.yaml search order matters** — CWD > ~/.config/openstack/ > /etc/openstack/; easy to use wrong credentials
8. **No resource tagging across all services** — tag support varies by service and API version
9. **No import/export of resource definitions** — no native backup/restore mechanism
10. **JSON output structure varies** — format can differ between API versions and services
11. **No built-in retry logic** — transient API failures require external retry mechanisms
12. **Interactive shell limited** — running `openstack` without arguments starts an interactive shell but with no readline support without gnureadline
13. **No man pages** — documentation only via `--help` and online docs
14. **Service endpoint discovery required** — commands fail if service is not registered in Keystone catalog
