# Bootstrap

Basic Linux machine configuration role.

## Description

This role performs initial setup and configuration of a fresh Linux server, including:

- System package updates and EPEL repository installation
- Timezone configuration
- Hostname setup
- User creation with Zsh shell
- Zsh configuration setup
- SSH public key deployment
- Passwordless sudo configuration

## Requirements

- Ansible 2.14 or newer
- Target system running RHEL-based distribution
- `username` variable must be provided (mandatory)

## Role Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `timezone` | `Etc/UTC` | System timezone |
| `sudo_nopasswd` | `false` | Whether to configure passwordless sudo for the created user |
| `hostname` | *not set* | System hostname |
| `username` | *required* | Username to create |
| `pubkey` | *not set* | SSH public key to deploy for the user |

## Dependencies

This role does not depend on other roles.

## Tags

The role uses the following tags for selective execution:

- `base` — Core configuration (hostname, timezone, user creation, sudo setup)
- `update` — Package updates with DNF
- `pkgs` — Package installation and EPEL repository

## Example Playbook

```yaml
- hosts: servers
  become: yes
  roles:
    - username.bootstrap
  vars:
    username: "deployuser"
    timezone: "America/New_York"
    sudo_nopasswd: true
    hostname: "server01.example.com"
    pubkey: "ssh-rsa AAAAB3Nza... user@example.com"
```

## License

MIT

## Author Information

AWFX