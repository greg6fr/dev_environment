# DevOps Environment Setup

This Ansible playbook sets up a complete DevOps environment with Docker, Node.js, Chrome, AWS CLI, and Terraform.

## Usage

### Basic Setup
```bash
ansible-playbook -i inventory.ini playbook.yml -K
```

### AWS CLI Configuration

For security reasons, AWS credentials are not stored in this repository. You have several options to provide them:

#### Option 1: Environment Variables
```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="eu-west-3"
ansible-playbook -i inventory.ini playbook.yml -K
```

#### Option 2: Ansible Extra Variables
```bash
ansible-playbook -i inventory.ini playbook.yml -K \
  -e aws_access_key_id="your-access-key" \
  -e aws_secret_access_key="your-secret-key" \
  -e aws_region="eu-west-3"
```

#### Option 3: Ansible Vault (Recommended for production)
1. Create an encrypted vault file:
```bash
ansible-vault create group_vars/all/vault.yml
```

2. Add your credentials to the vault:
```yaml
vault_aws_access_key_id: "your-access-key"
vault_aws_secret_access_key: "your-secret-key"
```

3. Reference vault variables in your playbook or update the defaults file.

## Components Installed

- **Docker**: Container runtime
- **Node.js 20**: JavaScript runtime
- **Google Chrome**: Web browser
- **AWS CLI v2**: Amazon Web Services command line interface
- **Angular CLI**: Command line interface for Angular development
- **Terraform**: Infrastructure as code tool

## Security Notes

- AWS credentials are never stored in the repository
- Use environment variables or Ansible Vault for sensitive data
- The playbook handles both fresh installations and updates gracefully
