# Ansible Playground

A comprehensive Ansible learning and testing environment with organized examples, utilities, and production-ready playbooks.

## 📁 Repository Structure

```
ansible-playground/
├── examples/                    # Learning examples and tutorials
│   ├── web-services/           # HTTP/Apache/Nginx examples
│   ├── variables/              # Variable usage examples
│   ├── loops-conditions/       # Loops and conditional logic
│   ├── user-management/        # User creation and management
│   ├── templates/              # Jinja2 template examples
│   ├── handlers/               # Handler examples
│   ├── notifications/          # Email and notification examples
│   └── monitoring/             # Monitoring examples (placeholder)
├── playbooks/                  # Production-ready playbooks
│   ├── production/             # Production environment playbooks
│   └── staging/                # Staging environment playbooks
├── roles/                      # Reusable Ansible roles
│   ├── common/                 # Common system tasks
│   ├── web/                    # Web server roles
│   └── monitoring/             # Monitoring and alerting roles
├── templates/                  # Shared Jinja2 templates
│   ├── html/                   # HTML templates
│   ├── config/                 # Configuration file templates
│   └── reports/                # Report templates
├── inventory/                  # Inventory files
│   └── production/             # Production inventory
│       ├── group_vars/         # Group variables
│       ├── host_vars/          # Host variables
│       └── inv.ini            # Inventory file
├── group_vars/                 # Global group variables
├── host_vars/                  # Global host variables
└── utils/                      # Utility scripts and tools
    ├── system/                 # System utilities
    ├── network/                # Network utilities (placeholder)
    ├── security/               # Security utilities (placeholder)
    └── execution-environments/ # Ansible EE configurations
```

## 🚀 Getting Started

### Prerequisites
- Ansible 2.9+
- Python 3.6+
- Access to target hosts

### Quick Start
```bash
# Run a simple example
ansible-playbook -i inventory/production/inv.ini examples/web-services/main.yml

# Run template example
ansible-playbook -i inventory/production/inv.ini examples/templates/solution-hello-ansible.yml

# Run with specific host group
ansible-playbook -i inventory/production/inv.ini examples/templates/solution-hello-ansible.yml --limit webservers
```

## 📚 Examples

### Web Services
- **HTTP Server Setup**: `examples/web-services/main.yml`
- **Template Usage**: `examples/templates/solution-hello-ansible.yml`

### Variables and Loops
- **Variable Management**: `examples/variables/01-variable/main.yml`
- **Loop Examples**: `examples/loops-conditions/02-loop-condition/loop.yml`
- **Conditional Logic**: `examples/loops-conditions/02-loop-condition/diskcheck.yml`
- **Nested Loops**: `examples/loops-conditions/02-loop-condition/nested-loop.yml`

### User Management
- **User Creation**: `examples/user-management/03-add-user/main.yml`
- **Password Management**: `examples/user-management/03-add-user/vars/user_passwords.yml`

### Templates and Handlers
- **Jinja2 Templates**: `examples/templates/templates/`
  - `hello-ansible.txt.j2` - Simple hostname and IP template
  - `index.html.j2` - HTML index page template
  - `hosts-report.html.j2` - Host reporting template
  - `simple.html.j2` - Basic HTML template
- **Handler Examples**: `examples/handlers/05-handler/main.yml`
- **Email Reports**: `examples/notifications/06-email/main.yml`
- **Hello Ansible**: `examples/templates/solution-hello-ansible.yml`

## 🔧 Utilities

### System Utilities
- **Service Checks**: `utils/system/check-service.yml`
- **System Facts**: `utils/system/fact.yml`
- **Privilege Escalation**: `utils/system/become.yml`
- **Ping Tests**: `utils/system/ping.yml`
- **Color Output**: `utils/system/color.yml`
- **System Checks**: `utils/system/check.yml`

### Execution Environments
- **EE Configuration**: `utils/execution-environments/ee.yml`

## 📋 Inventory Management

### Production Inventory
```bash
# Use production inventory
ansible-playbook -i inventory/production/inv.ini playbook.yml
```

### Group Variables
- **All Groups**: `inventory/production/group_vars/all.yml`
- **Web Servers**: `inventory/production/group_vars/webservers.yml`
- **Group1**: `inventory/production/group_vars/group1-og.yml`
- **Group2**: `inventory/production/group_vars/group2-og.yml`
- **Group3**: `inventory/production/group_vars/group3-og.yml`

### Host Variables
- **Host-specific configs**: `inventory/production/host_vars/`
- **Dev GCP**: `inventory/production/host_vars/devgcp.yml`
- **G2 Host**: `inventory/production/host_vars/g2.yml`
- **G3 Host**: `inventory/production/host_vars/g3.yml`

## 🎯 Best Practices

1. **Use descriptive names** instead of numbered folders
2. **Separate examples from production** code
3. **Organize by functionality** rather than chronology
4. **Keep templates centralized** for reusability
5. **Use consistent naming** conventions

## 📖 Learning Path

1. **Start with Variables**: `examples/variables/01-variable/` to understand Ansible basics
2. **Learn Control Structures**: `examples/loops-conditions/02-loop-condition/` for loops and conditions
3. **Explore Templates**: `examples/templates/` for dynamic content generation
4. **Practice Web Services**: `examples/web-services/` for real-world scenarios
5. **User Management**: `examples/user-management/03-add-user/` for system administration
6. **Handlers**: `examples/handlers/05-handler/` for service management
7. **Notifications**: `examples/notifications/06-email/` for reporting
8. **Utilities**: Use `utils/system/` for common tasks and troubleshooting

## 🔒 Security Notes

- Vault files are encrypted and require `ansible-vault` to edit
- Sensitive variables should be stored in vault files
- Use `--ask-vault-pass` when running playbooks with encrypted variables

## 📞 Support

For questions or issues:
1. Check the example playbooks in the `examples/` directory
2. Review the utility scripts in `utils/system/`
3. Consult the Ansible documentation
4. Check inventory configurations in `inventory/production/`
5. Use the learning path above to progress through examples

## 🎯 Available Examples

### Complete Example List
- **Variables**: `examples/variables/01-variable/` - Variable usage, registration, and printing
- **Loops & Conditions**: `examples/loops-conditions/02-loop-condition/` - Loop constructs and conditional logic
- **User Management**: `examples/user-management/03-add-user/` - User creation and password management
- **Templates**: `examples/templates/` - Jinja2 template examples and solutions
- **Handlers**: `examples/handlers/05-handler/` - Service restart and handler patterns
- **Notifications**: `examples/notifications/06-email/` - Email reporting and notifications
- **Web Services**: `examples/web-services/` - HTTP server configuration

### Key Files to Start With
- `examples/templates/solution-hello-ansible.yml` - Simple template example
- `examples/variables/01-variable/main.yml` - Variable basics
- `examples/loops-conditions/02-loop-condition/loop.yml` - Loop examples
- `utils/system/fact.yml` - System information gathering

---

**Note**: This repository has been restructured for better organization and maintainability. All original content has been preserved and reorganized into logical categories with descriptive folder names.