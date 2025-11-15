# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository provides Ansible playbooks and Python scripts for testing Kubernetes clusters. It includes health checks, node validation, and extensible roles for comprehensive cluster testing.

## Setup Commands

```bash
# Create and activate virtual environment
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies (always activate venv first!)
pip install -r requirements.txt

# Install development dependencies
pip install -r requirements-dev.txt
```

## Common Commands

### Running Tests
```bash
# Test cluster health
ansible-playbook playbooks/test_cluster_health.yml

# Syntax check
ansible-playbook --syntax-check playbooks/test_cluster_health.yml

# Dry run
ansible-playbook --check playbooks/test_cluster_health.yml

# Run with specific inventory
ansible-playbook -i inventory/hosts.yml playbooks/test_cluster_health.yml
```

### Python Testing
```bash
# Run tests
pytest tests/

# Run with coverage
pytest --cov=. tests/
```

### Code Quality
```bash
# Lint Ansible
ansible-lint playbooks/

# Format Python
black .

# Lint Python
flake8 .
pylint **/*.py
```

## Project Structure

- `playbooks/` - Ansible playbooks for various Kubernetes tests
- `roles/` - Reusable Ansible roles (currently: common)
- `inventory/` - Inventory files for different cluster environments
- `library/` - Custom Ansible modules
- `filter_plugins/` - Custom Jinja2 filters
- `tests/integration/` - Integration tests
- `tests/unit/` - Unit tests
- `ansible.cfg` - Ansible configuration (sets inventory path, roles path, etc.)

## Architecture Notes

- Playbooks use `kubernetes.core` collection for K8s resource management
- Tests run against `localhost` with kubectl/kubeconfig access
- Inventory supports both local (kubectl-based) and remote (SSH-based) testing
- Custom modules and filters can be added to `library/` and `filter_plugins/`

## Python Environment

- Always activate the Python virtual environment before installing pip modules
- Virtual environment should be `.venv` (gitignored)
- Python 3.8+ required
