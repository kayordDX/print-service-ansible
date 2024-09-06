# Setup Print Service

Ansible playbook to setup Print Service

## Run

```bash
# Make sure vault password file exists in `~/.ansible/.vault_password.txt`
ansible-galaxy install -r requirements.yml

ansible-playbook playbooks/setup/setup.yml -K --ask-pass
ansible-playbook playbooks/print-service/print-service.yml -K

sudo tailscale up
```

## Vault

```bash
ansible-vault encrypt inventory/group_vars/all.yml
ansible-vault decrypt inventory/group_vars/all.yml
```
