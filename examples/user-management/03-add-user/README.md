# 01-add-user

This Ansible playbook demonstrates how to create users with secure, hashed passwords using Ansible Vault for password encryption.

## Overview

The playbook creates multiple users on target hosts with the following features:
- Secure password storage using Ansible Vault
- Automatic password hashing using SHA-512
- Group membership assignment
- Creates two users:
  - `surote` - member of `wheel` group (admin privileges)
  - `appox` - member of `developers` group

## Directory Structure

```
01-add-user/
├── main.yml                          # Main playbook
├── inventory/
│   ├── inv.ini                       # Inventory file with host definitions
│   └── group_vars/
│       └── webservers.yml            # Encrypted group variables
├── vars/
│   └── user_passwords.yml            # Encrypted user passwords
└── README.md                         # This file
```

## Prerequisites

- Ansible installed on the control node
- SSH access to target hosts
- Sudo privileges on target hosts (for user creation)
- Ansible Vault password (to decrypt the encrypted files)

## Files Explained

### main.yml
The main playbook that:
1. Loads encrypted password variables from `vars/user_passwords.yml`
2. Uses the `ansible.builtin.user` module to create users
3. Hashes passwords using SHA-512 before storing them
4. Assigns users to their respective groups

### vars/user_passwords.yml
Ansible Vault encrypted file containing user passwords in the format:
```yaml
user_passwords:
  surote: "plaintext_password"
  appox: "plaintext_password"
```

### inventory/group_vars/webservers.yml
Encrypted group-specific variables for the webservers group.

## Usage

### Running the Playbook

Basic execution:
```bash
ansible-playbook -i inventory/inv.ini main.yml --ask-vault-pass
```

Or with a vault password file:
```bash
ansible-playbook -i inventory/inv.ini main.yml --vault-password-file ~/.vault_pass
```

### Running with Ansible Navigator

Using ansible-navigator with an execution environment:
```bash
ansible-navigator run main.yml -i inventory/inv.ini -m stdout --vault-password-file .vault-pass --execution-environment-image localhost/minimal-ee:1.0
```

Parameters explained:
- `-m stdout` - Display output in stdout mode (instead of interactive text UI)
- `--vault-password-file .vault-pass` - Path to file containing vault password
- `--execution-environment-image` - Specify the container image to use for execution

### Managing Vault-Encrypted Files

#### View encrypted content:
```bash
ansible-vault view vars/user_passwords.yml
```

#### Edit encrypted files:
```bash
ansible-vault edit vars/user_passwords.yml
```

#### Change vault password:
```bash
ansible-vault rekey vars/user_passwords.yml
```

#### Create new encrypted file:
```bash
ansible-vault create vars/new_file.yml
```

## Adding New Users

1. Edit the encrypted password file:
   ```bash
   ansible-vault edit vars/user_passwords.yml
   ```

2. Add the new user's password to the `user_passwords` dictionary:
   ```yaml
   user_passwords:
     surote: "password1"
     appox: "password2"
     newuser: "password3"  # Add this line
   ```

3. Update the `main.yml` playbook to include the new user in the loop:
   ```yaml
   loop:
     - { name: 'surote', groups: 'wheel' }
     - { name: 'appox', groups: 'developers' }
     - { name: 'newuser', groups: 'users' }  # Add this line
   ```

4. Run the playbook

## Security Best Practices

1. **Never commit unencrypted passwords** to version control
2. **Store vault password securely** - consider using a password manager
3. **Use different vault passwords** for different environments (dev, staging, prod)
4. **Rotate passwords regularly** and update the vault files accordingly
5. **Limit access** to vault passwords based on need-to-know basis

## Inventory

The playbook targets hosts defined in `inventory/inv.ini`:
- `web1` - 192.168.1.10
- `web2` - 192.168.1.11

Modify this file to target your specific hosts.

## Troubleshooting

### "Vault password not provided"
Make sure you're using either `--ask-vault-pass` or `--vault-password-file` when running the playbook.

### "Permission denied" errors
Ensure your SSH user has sudo privileges on the target hosts.

### Users not created
Check that the required groups exist on the target systems, or modify the playbook to create them first.

## Notes

- The `wheel` group typically provides sudo access on RHEL-based systems
- The `developers` group should be created on target hosts or added to the playbook
- Passwords are hashed on the Ansible controller before being sent to target hosts
- The SHA-512 hashing algorithm is used for compatibility and security

