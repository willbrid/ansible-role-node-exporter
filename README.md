# Ansible-role-node-exporter

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/willbrid/ansible-role-node-exporter/blob/main/LICENSE) [![CI](https://github.com/willbrid/ansible-role-node-exporter/actions/workflows/ci.yml/badge.svg)](https://github.com/willbrid/ansible-role-node-exporter/actions/workflows/ci.yml)

Le rôle **ansible-role-node-exporter** permet d'installer et de configurer **node_exporter**, un agent Prometheus conçu pour exposer les métriques matérielles et système des environnements Linux.

## Exigences

Un système Linux utilisant **systemd** comme gestionnaire de services.

## Description des Variables

|Nom|Type|Description|Obligatoire|Valeur par défaut|
|---|----|-----------|-----------|-----------------|
`node_exporter_version`|str|numéro de version de node_exporter. Format : x.y.z|non|`"1.9.0"`
`node_exporter_port`|str|port d'écoute de node_exporter|non|`"9100"`
`node_exporter_bin_dir`|str|répertoire d'installation du binaire de node_exporter|non|`"/usr/local/bin"`
`node_exporter_user`|str|utilisateur système de node_exporter|non|`"node_exporter"`
`node_exporter_user_uid`|int|uid de l'utilisateur système de node_exporter. -1 signifie aucune valeur|non|`-1`
`node_exporter_group`|str|groupe de l'utilisateur système de node_exporter|non|`"node_exporter"`
`node_exporter_group_gid`|int|gid du groupe de l'utilisateur système de node_exporter. -1 signifie aucune valeur|non|`-1`

## Dépendances

Aucune.

## Exemple Playbook

- Installation du rôle

```bash
mkdir -p $HOME/install-node-exporter/roles
```

```bash
vim $HOME/install-node-exporter/requirements.yml
```

```yaml
- name: ansible-role-node-exporter
  src: https://github.com/willbrid/ansible-role-node-exporter.git
  version: v0.1.0
```

```bash
cd $HOME/install-node-exporter && ansible-galaxy install -r requirements.yml --roles-path roles
```

> Note: On suppose qu’un fichier `hosts.ini` (dans le repertoire `$HOME/install-repo-installer`) est défini, contenant l’inventaire des serveurs de groupe `monitoring`, utilisant des distributions `Debian` ou `RedHat`.

- Utilisation du rôle dans un playbook

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

## Licence

MIT

## Informations sur l'auteur

William Bridge NGASSAM
