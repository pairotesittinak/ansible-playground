# Ansible Email with HTML Attachment

This playbook demonstrates how to send emails with HTML attachments using Ansible.

## Files Structure

```
06-email/
├── main.yml                    # Main playbook
├── vars/
│   └── email_config.yml       # Email configuration variables
├── templates/
│   └── email-report.html.j2   # HTML template for email attachment
└── README.md                  # This file
```

## Prerequisites

1. **SMTP Server Access**: You need access to an SMTP server (Gmail, Outlook, etc.)
2. **Python mail module**: The `mail` module requires Python's `smtplib` and `email` libraries
3. **App Password**: For Gmail, you'll need to generate an App Password

## Configuration

### 1. Update Email Settings

Edit `vars/email_config.yml` with your email settings:

```yaml
smtp_host: "smtp.gmail.com"          # Your SMTP server
smtp_port: 587                       # SMTP port (587 for TLS)
smtp_username: "your-email@gmail.com" # Your email address
smtp_password: "your-app-password"   # Your app password
smtp_secure: "starttls"              # Security method

email_to: "recipient@example.com"    # Recipient email
email_from: "your-email@gmail.com"   # Sender email
email_subject: "System Report"       # Email subject
```

### 2. Gmail Setup (if using Gmail)

1. Enable 2-Factor Authentication on your Google account
2. Generate an App Password:
   - Go to Google Account settings
   - Security → 2-Step Verification → App passwords
   - Generate a password for "Mail"
   - Use this password in `smtp_password`

## Usage

### Run the Playbook

```bash
# Run with default settings
ansible-playbook main.yml

# Run with custom variables
ansible-playbook main.yml -e "email_to=admin@company.com" -e "email_subject=Daily Report"
```

### Customize the HTML Template

The HTML template (`templates/email-report.html.j2`) uses Jinja2 templating and can access Ansible facts:

- `{{ ansible_hostname }}` - System hostname
- `{{ ansible_distribution }}` - OS distribution
- `{{ ansible_date_time.date }}` - Current date
- `{{ ansible_date_time.time }}` - Current time

## Features

- **HTML Email Attachment**: Creates a styled HTML report
- **Template-based**: Uses Jinja2 templates for dynamic content
- **Configurable**: All email settings in variables file
- **Clean-up**: Automatically removes temporary files
- **Responsive Design**: HTML template includes CSS styling

## Troubleshooting

### Common Issues

1. **Authentication Failed**:
   - Check your SMTP credentials
   - Ensure App Password is used (not regular password)
   - Verify SMTP server settings

2. **Connection Timeout**:
   - Check firewall settings
   - Verify SMTP port is correct
   - Try different security method (starttls vs ssl)

3. **Template Not Found**:
   - Ensure template file exists in `templates/` directory
   - Check file permissions

### Testing SMTP Connection

You can test your SMTP settings with a simple playbook:

```yaml
- name: Test SMTP Connection
  hosts: localhost
  tasks:
    - name: Send test email
      mail:
        host: "{{ smtp_host }}"
        port: "{{ smtp_port }}"
        username: "{{ smtp_username }}"
        password: "{{ smtp_password }}"
        to: "{{ email_to }}"
        from: "{{ email_from }}"
        subject: "Test Email"
        body: "This is a test email"
        secure: "{{ smtp_secure }}"
```

## Security Notes

- Never commit email passwords to version control
- Use environment variables for sensitive data
- Consider using Ansible Vault for password encryption
- Use App Passwords instead of regular passwords

## Example with Ansible Vault

1. Create encrypted variables file:
```bash
ansible-vault create vars/secrets.yml
```

2. Add sensitive data:
```yaml
smtp_password: "your-app-password"
email_to: "admin@company.com"
```

3. Update main.yml to include secrets:
```yaml
vars_files:
  - vars/email_config.yml
  - vars/secrets.yml
```

4. Run with vault password:
```bash
ansible-playbook main.yml --ask-vault-pass
```
