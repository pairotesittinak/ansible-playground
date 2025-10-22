# Ansible Playground

A collection of Ansible playbooks for learning and testing various automation scenarios.

## Project Structure

```
ansible-playground/
├── 00-httpd/           # Basic HTTP server installation
├── 01-variable/        # Variable usage examples
├── 02-loop-condition/ # Loops and conditions
├── 03-add-user/        # User management
├── 04-template/        # Template usage
├── prep/              # System preparation and setup
├── inventory/          # Inventory files and variables
└── ee/                # Execution Environment
```

## Quick Start

Run example playbooks:
```bash
ansible-playbook -i inventory/inv.ini 00-httpd/main.yml
```

## Playbooks

### 00-httpd
Basic HTTP server installation and configuration.

### 01-variable
Demonstrates variable usage with external variable files.

### 02-loop-condition
Shows loops, conditions, and control structures.

### 03-add-user
User management and password handling.

### 04-template
Template usage for configuration files.


## Inventory

The inventory is organized with:
- **Groups**: `rh-target`, `rh-control-group`
- **Group variables**: `inventory/group_vars/`
- **Host variables**: `inventory/host_vars/`

## Requirements

- Ansible 2.9+
- Red Hat Enterprise Linux target hosts
- SSH access to target hosts
- Sudo privileges on target hosts

## Usage

All playbooks use the inventory file `inventory/inv.ini`. Run any playbook with:

```bash
ansible-playbook -i inventory/inv.ini <playbook-path>
```

### Using Vault

For playbooks with encrypted variables, use vault:

```bash
# With vault password prompt
ansible-playbook -i inventory/inv.ini <playbook-path> --ask-vault-pass

# With vault password file
ansible-playbook -i inventory/inv.ini <playbook-path> --vault-password-file .vault_pass
```

## Key Ansible Concepts

### Register Variables
**Purpose**: Capture task output and metadata for use in subsequent tasks.

**How it works**: The `register` directive stores the result of a task in a variable that you can reference later. This allows you to make decisions based on previous task results, display output, or use data in conditional statements.

**Common use cases**: Checking service status, capturing command output, handling errors, and creating dynamic playbooks that adapt based on system state.

### Become (Privilege Escalation)
**Purpose**: Execute tasks with elevated permissions (like sudo or su).

**How it works**: The `become` directive allows Ansible to run tasks as a different user, typically root, when the current user doesn't have sufficient privileges. It supports multiple methods including sudo, su, and doas.

**Common use cases**: Installing packages, modifying system files, managing services, and performing administrative tasks that require root access.

### Facts
**Purpose**: Automatic system information gathering for dynamic playbook behavior.

**How it works**: Ansible automatically collects system information (hostname, OS, memory, network interfaces, etc.) and makes it available as variables. Facts are gathered at the start of each play unless disabled.

**Common use cases**: Conditional logic based on OS type, dynamic configuration using system information, and creating portable playbooks that adapt to different environments.

## Learning Path

1. Explore numbered directories for different concepts
2. Check `inventory/` for variable examples
3. Review `util/` directory for practical examples
