# Lima - Linux Virtual Machines Made Simple

## What is Lima?

Lima (Linux Machines) is a lightweight tool that launches Linux virtual machines
with automatic file sharing and port forwarding, similar to WSL2 but available
on macOS and Linux hosts. It provides a simple, free way to run Linux VMs for
development and testing.

## Features

- **Automatic file sharing** between host and VM
- **Port forwarding** for seamless networking
- **Multiple Linux distributions** supported
- **Lightweight** and resource-efficient
- **Simple command-line interface**

## Quick Installation on macOS

```sh
# Install Lima using Homebrew
brew install lima

# Create a new VM named 'default' based on Debian 12
# View all available templates: https://lima-vm.io/docs/templates/
limactl create --name=default template://debian-12

# Start the VM
limactl start default

# Verify the VM is running
limactl list

# Open a shell in the VM
lima
```

## Basic Commands

| Command                     | Description                     |
| --------------------------- | ------------------------------- |
| `limactl create <template>` | Create a new VM from a template |
| `limactl start <vm-name>`   | Start a VM                      |
| `limactl stop <vm-name>`    | Stop a VM                       |
| `limactl delete <vm-name>`  | Delete a VM                     |
| `limactl list`              | List all VMs and their status   |
| `lima`                      | Open shell in default VM        |
| `lima <vm-name>`            | Open shell in specific VM       |

## File Sharing and Mount Points

### Default Mount Points

Lima automatically mounts the following directories:

- **Home directory**: `$HOME` → mounted as **read-only** at the same path
- **Temporary directory**: `/tmp/lima` → mounted as **read-write** at the same
  path

### Custom Mount Configuration

For development workflows, you may want to mount your project directories as
read-write.

Here is how to configure a custom mount point for the `default` VM I am using:

1. **Edit the VM configuration file**:

   ```sh
   # For the default VM
   vim ~/.lima/default/lima.yml
   ```

2. **Add custom mount points** in the `mounts` section:

   ```yaml
   mounts:
     - location: "~/Development"
       mountPoint: /Development
       writable: true
   ```

3. **Restart the VM** to apply changes:

   ```sh
   limactl stop default
   limactl start default
   ```

### Mount Configuration Options

- `location`: Path on the host system
- `mountPoint`: Path inside the VM
- `writable`: Set to `true` for read-write access, `false` for read-only

## Common Use Cases

- **Development environment**: Run Linux tools and commands on macOS
- **Container development**: Test Docker containers in a Linux environment
- **Cross-platform testing**: Test applications across different Linux
  distributions
- **Learning Linux**: Practice Linux commands and administration

## Troubleshooting

### VM Won't Start

```sh
# Check VM status and logs
limactl list
limactl show-log default
```

### File Permission Issues

Ensure your user has proper permissions on mounted directories and consider the
`writable` flag in mount configuration.

### Network Issues

Lima handles port forwarding automatically, but you can check the configuration
in the VM's YAML file under the `networks` section.

## Additional Resources

- **Official Documentation**: <https://lima-vm.io/>
- **Template Repository**: <https://lima-vm.io/docs/templates/>
- **GitHub Repository**: <https://github.com/lima-vm/lima>
