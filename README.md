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

## Learning Path

1. Explore numbered directories for different concepts
2. Check `inventory/` for variable examples
