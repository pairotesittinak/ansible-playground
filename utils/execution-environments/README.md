# Ansible Execution Environment (EE)

This directory contains the definition file for building a custom Ansible Execution Environment.

## What is an Execution Environment?

An Execution Environment (EE) is a container image that packages Ansible, collections, dependencies, and other requirements into a portable, consistent runtime. It ensures that your automation runs the same way across different systems.

## Prerequisites

Before creating an execution environment, you need:

1. **ansible-builder** - The tool to build execution environments
   ```bash
   pip install ansible-builder
   ```

2. **Container runtime** - Either Podman (recommended) or Docker
   ```bash
   # For RHEL/Rocky/Alma Linux
   sudo dnf install podman
   ```

3. **Access to base image registry** (if using Red Hat images)
   - Red Hat registry credentials for `registry.redhat.io`
   - Login to registry:
     ```bash
     podman login registry.redhat.io
     ```

## Understanding the ee.yml File

The `ee.yml` file defines what goes into your execution environment:

### Version
```yaml
version: 3
```
Specifies the EE definition format version.

### Dependencies

- **Python packages**: Python libraries required by modules
  ```yaml
  python:
    - pymssql      # For MSSQL database connections
    - passlib      # For password hashing
  ```

- **Galaxy collections**: Ansible collections to include
  ```yaml
  galaxy:
    collections:
      - name: community.postgresql
      - name: community.general
      - name: community.docker
  ```

- **System packages**: OS-level packages needed
  ```yaml
  system:
    - gcc                  # C compiler
    - systemd-devel        # Systemd development libraries
    - python3.11-devel     # Python development headers
  ```

### Options
```yaml
options:
  package_manager_path: /usr/bin/microdnf
```
Specifies which package manager to use (microdnf for smaller images).

### Base Image
```yaml
images:
  base_image:
    name: registry.redhat.io/ansible-automation-platform-25/ee-supported-rhel8:latest
```
The base container image to build upon.

## Building the Execution Environment

### Method 1: Using ansible-builder (Recommended)

1. **Navigate to the ee directory**:
   ```bash
   cd /home/swongpai/ansible-playground/ee
   ```

2. **Build the execution environment**:
   ```bash
   ansible-builder build --tag my-custom-ee:latest
   ```

3. **Build with a specific container runtime**:
   ```bash
   # Using Podman (default)
   ansible-builder build --tag my-custom-ee:latest --container-runtime podman
   
   # Using Docker
   ansible-builder build --tag my-custom-ee:latest --container-runtime docker
   ```

4. **Build with verbose output**:
   ```bash
   ansible-builder build --tag my-custom-ee:latest -v 3
   ```

### Method 2: Multi-step Build Process

1. **Create the build context**:
   ```bash
   ansible-builder create
   ```
   This generates a `context` directory with Dockerfiles and dependency files.

2. **Build the image manually**:
   ```bash
   podman build -f context/Containerfile -t my-custom-ee:latest context
   ```

## Verifying the Execution Environment

After building, verify your EE:

1. **List images**:
   ```bash
   podman images | grep my-custom-ee
   ```

2. **Inspect the image**:
   ```bash
   podman inspect my-custom-ee:latest
   ```

3. **Test the EE**:
   ```bash
   podman run --rm -it my-custom-ee:latest ansible --version
   ```

4. **Check installed collections**:
   ```bash
   podman run --rm -it my-custom-ee:latest ansible-galaxy collection list
   ```

5. **Run a playbook using the EE**:
   ```bash
   ansible-navigator run playbook.yml --execution-environment-image my-custom-ee:latest
   ```

## Using the Execution Environment

### With ansible-navigator

```bash
ansible-navigator run playbook.yml \
  --execution-environment-image my-custom-ee:latest \
  --mode interactive
```

## Customizing the EE

To add more dependencies, edit `ee.yml`:

```yaml
dependencies:
  python:
    - your-python-package
  galaxy:
    collections:
      - name: namespace.collection
  system:
    - your-system-package
```

Then rebuild:
```bash
ansible-builder build --tag my-custom-ee:v2
```

## Troubleshooting

### Build fails with permission errors
- Make sure you're logged into the registry: `podman login registry.redhat.io`
- Use sudo if needed: `sudo ansible-builder build ...`

### Collection installation fails
- Ensure you have proper Galaxy credentials
- Check network connectivity

### System package installation fails
- Verify package names are correct for the base OS
- Check that the base image repository is accessible

### Image size is too large
- Use a minimal base image
- Remove unnecessary dependencies
- Use multi-stage builds

## References

- [Ansible Builder Documentation](https://ansible-builder.readthedocs.io/)
- [Execution Environments Guide](https://docs.ansible.com/ansible/latest/getting_started_ee/index.html)

## Notes

- The base image uses RHEL 8 which requires valid Red Hat subscriptions
- System packages (gcc, systemd-devel, python3.11-devel) are needed for Python packages that compile C extensions
- The collections specified will be pre-installed in the EE for offline use

