# Ansible-role-node-exporter

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/willbrid/ansible-role-node-exporter/blob/main/LICENSE) [![CI](https://github.com/willbrid/ansible-role-node-exporter/actions/workflows/ci.yml/badge.svg)](https://github.com/willbrid/ansible-role-node-exporter/actions/workflows/ci.yml)

The **ansible-role-node-exporter** role allows you to install and configure **node_exporter**, a Prometheus agent designed to expose hardware and system metrics of Linux environments.

## Requirements

- **RedHat** or **Debian** distributions using **systemd** as a service manager.

## Description des Variables

|Name|Type|Description|Mandatory|Default value|
|----|----|-----------|---------|-------------|
`node_exporter_version`|str|node_exporter version number. Format: x.y.z|no|`"1.9.0"`
`node_exporter_port`|str|node_exporter listening port|no|`"9100"`
`node_exporter_bin_dir`|str|node_exporter binary installation directory|no|`"/usr/local/bin"`
`node_exporter_user`|str|node_exporter system user|no|`"node_exporter"`
`node_exporter_user_uid`|int|the system user ID of node_exporter. -1 means no value|no|`-1`
`node_exporter_group`|str|node_exporter system user group|no|`"node_exporter"`
`node_exporter_group_gid`|int|GID of the system user node_exporter. -1 means no value|no|`-1`

## Dependencies

None.

## Example Playbook

- Role installation

```bash
mkdir -p $HOME/install-node-exporter
```

```bash
vim $HOME/install-node-exporter/requirements.yml
```

```yaml
- name: ansible-role-node-exporter
  src: git+https://github.com/willbrid/ansible-role-node-exporter.git
  version: v0.1.0
```

```bash
cd $HOME/install-node-exporter && ansible-galaxy install --force -r requirements.yml
```

> Note: It is assumed that a `hosts.ini` file (in the `$HOME/install-repo-installer` directory) is defined, containing the inventory of the `monitoring` group servers, using `Debian` or `RedHat` distributions.

- Using the role in a playbook

```bash
vim $HOME/install-node-exporter/playbook.yml
```

```yaml
---
- hosts: monitoring
  become: true

  vars:
    node_exporter_version: "1.9.0"

  roles:
    - ansible-role-node-exporter
```

```
cd $HOME/install-node-exporter && ansible-playbook -i hosts.ini playbook.yml
```

## License

MIT

## Author Information

William Bridge NGASSAM
