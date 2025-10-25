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
│   └── notifications/          # Email and notification examples
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
│   ├── production/             # Production inventory
│   └── staging/                # Staging inventory
├── group_vars/                 # Group variables
├── host_vars/                  # Host-specific variables
└── utils/                      # Utility scripts and tools
    ├── system/                 # System utilities
    ├── network/                # Network utilities
    ├── security/               # Security utilities
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
ansible-playbook -i inventory/production/inv.ini examples/web-services/httpd/main.yml

# Run with specific host group
ansible-playbook -i inventory/production/inv.ini examples/templates/solution-hello-ansible.yml --limit webservers
```

## 📚 Examples

### Web Services
- **HTTP Server Setup**: `examples/web-services/httpd/main.yml`
- **Template Usage**: `examples/templates/solution-hello-ansible.yml`

### Variables and Loops
- **Variable Management**: `examples/variables/main.yml`
- **Loop Examples**: `examples/loops-conditions/loop.yml`
- **Conditional Logic**: `examples/loops-conditions/diskcheck.yml`

### User Management
- **User Creation**: `examples/user-management/main.yml`
- **Password Management**: `examples/user-management/vars/user_passwords.yml`

### Templates and Handlers
- **Jinja2 Templates**: `examples/templates/templates/`
- **Handler Examples**: `examples/handlers/main.yml`
- **Email Reports**: `examples/notifications/main.yml`

## 🔧 Utilities

### System Utilities
- **Service Checks**: `utils/system/check-service.yml`
- **System Facts**: `utils/system/fact.yml`
- **Privilege Escalation**: `utils/system/become.yml`

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

### Host Variables
- **Host-specific configs**: `inventory/production/host_vars/`

## 🎯 Best Practices

1. **Use descriptive names** instead of numbered folders
2. **Separate examples from production** code
3. **Organize by functionality** rather than chronology
4. **Keep templates centralized** for reusability
5. **Use consistent naming** conventions

## 📖 Learning Path

1. Start with `examples/variables/` to understand Ansible basics
2. Move to `examples/loops-conditions/` for control structures
3. Explore `examples/templates/` for dynamic content
4. Practice with `examples/web-services/` for real-world scenarios
5. Use `utils/` for common tasks and troubleshooting

## 🔒 Security Notes

- Vault files are encrypted and require `ansible-vault` to edit
- Sensitive variables should be stored in vault files
- Use `--ask-vault-pass` when running playbooks with encrypted variables

## 📞 Support

For questions or issues:
1. Check the example playbooks in the `examples/` directory
2. Review the utility scripts in `utils/`
3. Consult the Ansible documentation
4. Check inventory configurations in `inventory/`

---

**Note**: This repository has been restructured for better organization and maintainability. All original content has been preserved and reorganized into logical categories.