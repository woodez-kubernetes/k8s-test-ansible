# Kubernetes Testing with Ansible

This repository contains Ansible playbooks and Python scripts for testing Kubernetes clusters.

## Prerequisites

- Python 3.8+
- Ansible 2.15+
- kubectl configured with access to your Kubernetes cluster
- SSH access to cluster nodes (for node-level tests)

## Setup

1. Create and activate a Python virtual environment:
```bash
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. For development, install dev dependencies:
```bash
pip install -r requirements-dev.txt
```

4. Configure your inventory:
   - Edit `inventory/hosts.yml` with your cluster details
   - Update IP addresses, hostnames, and credentials

## Usage

### Running Test Playbooks

Test cluster health:
```bash
ansible-playbook playbooks/test_cluster_health.yml
```

### Running with specific inventory:
```bash
ansible-playbook -i inventory/hosts.yml playbooks/test_cluster_health.yml
```

### Check playbook syntax:
```bash
ansible-playbook --syntax-check playbooks/test_cluster_health.yml
```

### Dry run:
```bash
ansible-playbook --check playbooks/test_cluster_health.yml
```

## Project Structure

```
.
├── playbooks/          # Ansible playbooks for testing
├── roles/              # Reusable Ansible roles
├── inventory/          # Inventory files for different environments
├── library/            # Custom Ansible modules
├── filter_plugins/     # Custom Jinja2 filters
├── tests/              # Python tests
│   ├── integration/    # Integration tests
│   └── unit/           # Unit tests
├── ansible.cfg         # Ansible configuration
└── requirements.txt    # Python dependencies
```

## Testing

Run Python tests:
```bash
pytest tests/
```

Run with coverage:
```bash
pytest --cov=. tests/
```

Lint Ansible playbooks:
```bash
ansible-lint playbooks/
```

## Development

Format Python code:
```bash
black .
```

Lint Python code:
```bash
flake8 .
pylint **/*.py
```

## Environment Variables

You can use a `.env` file for configuration (this file is gitignored):
```bash
KUBECONFIG=/path/to/kubeconfig
K8S_AUTH_KUBECONFIG=/path/to/kubeconfig
```


source .venv/bin/activate
You can now:
Configure your cluster in inventory/hosts.yml
Run the example test playbook: ansible-playbook playbooks/test_cluster_health.yml
Add custom playbooks to the playbooks/ directory
Develop custom roles in the roles/ directory
The environment is ready for Kubernetes testing with Ansible!