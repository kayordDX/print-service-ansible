# Copilot Instructions for print-service-ansible

## Project Overview

- This repository manages the setup and configuration of a Print Service using Ansible.
- The architecture is organized around Ansible playbooks and roles, with a focus on modular, reusable automation for Raspberry Pi and related infrastructure.
- Major playbooks are in `playbooks/`, with roles and templates nested under each playbook directory.

## Key Components

- `playbooks/print-service/print-service.yml`: Main playbook for deploying the print service.
- `playbooks/setup/setup.yml`: Initial setup tasks (e.g., SSH, base config).
- `roles/`: Contains Ansible roles for modular tasks (e.g., `wifi`, `compose`, `tailscale`).
- `templates/`: Jinja2 templates for configuration files (e.g., NetworkManager `.nmconnection` files).
- `inventory/`: Hosts and group variables, including secrets (encrypted with Ansible Vault).

## Developer Workflows

- **Install dependencies:** `ansible-galaxy install -r requirements.yml`
- **Run playbooks:**
  - `ansible-playbook playbooks/setup/setup.yml -K --ask-pass`
  - `ansible-playbook playbooks/print-service/print-service.yml -K`
- **Vault operations:**
  - Encrypt: `ansible-vault encrypt inventory/group_vars/all.yml`
  - Decrypt: `ansible-vault decrypt inventory/group_vars/all.yml`
- **Tailscale setup:** `sudo tailscale up` (run manually after playbook)

## Project Conventions

- All sensitive variables are stored in `inventory/group_vars/all.yml` and encrypted with Ansible Vault.
- NetworkManager WiFi profiles are managed via Jinja2 templates in `roles/wifi/templates/`.
- Role variables are defined in `roles/<role>/vars/main.yml`.
- Use `-K` to prompt for sudo password when running playbooks.
- Playbooks and roles are structured for clarity and minimal duplication.

## Integration Points

- Relies on Tailscale for secure networking (manual step after playbook run).
- Uses Ansible Galaxy for role dependencies (`requirements.yml`).
- Designed for headless Raspberry Pi setups, especially for WiFi and SSH provisioning.

## Examples

- To add a new WiFi network, create a new Jinja2 template in `roles/wifi/templates/` and reference it in the role's tasks.
- To update secrets, edit and re-encrypt `inventory/group_vars/all.yml`.

## References

- See `README.md` for quickstart and essential commands.
- Review playbook and role structure for best practices in modular Ansible automation.
