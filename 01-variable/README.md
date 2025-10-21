# 03-variable

Simple Ansible variables demonstration.

## What it does

Shows how to use variables in Ansible:
- Playbook variables (`vars:`)
- External variables (`vars_files:`)
- Ansible facts (system info)

## Files

- `main.yml` - Main playbook
- `vars/app_config.yml` - External variables

## Run

```bash
ansible-playbook -i inventory/inv.ini main.yml
```

## Variables

**Playbook variables:**
- `app_name: "MyApp"`
- `app_port: 8080` 

**External variables:**
- `db_host: "localhost"`

**Ansible facts:**
- `{{ inventory_hostname }}`
- `{{ ansible_distribution }}`

## Tasks

1. Shows variable values
2. Creates `/opt/MyApp/` directory
3. Creates config file with variables

## Variable syntax

```yaml
{{ variable_name }}
```

## Override variables

```bash
ansible-playbook -i inventory/inv.ini main.yml -e "app_name=NewApp"
```
