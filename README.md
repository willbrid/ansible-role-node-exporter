Ansible-role-node-exporter
=========

Ce rôle Ansible installe et configure **node_exporter**, un agent Prometheus conçu pour exposer les métriques matérielles et système des environnements Linux.

Exigences
------------

Un système Linux utilisant **systemd** comme gestionnaire de services.

Description des Variables
--------------

|Nom|Type|Description|Valeur par défaut|
|---|----|-----------|-----------------|
`node_exporter_version`|string|numéro de version de node_exporter. Format : x.y.z|`"1.9.0"`
`node_exporter_download_url`|string|Url de téléchargement du fichier archive de node_exporter. (par défaut il dépend de deux variables : une variable externe modifiable **node_exporter_version** et une variable interne non modifiable **node_exporter_architecture**)|`"https://github.com/prometheus/node_exporter/releases/download/v{{ node_exporter_version }}/node_exporter-{{ node_exporter_version }}.linux-{{ node_exporter_architecture }}.tar.gz"`
`node_exporter_port`|string|Port d'écoute de node_exporter|`"9100"`
`node_exporter_bin_dir`|string|Répertoire d'installation du binaire de node_exporter|`"/usr/local/bin"`
`node_exporter_user`|string|Utilisateur système de node_exporter|`"node_exporter"`
`node_exporter_group`|string|Groupe de l'utilisateur système de node_exporter|`"node_exporter"`

**NB:** Vous pouvez modifier ces variables en fonction de vos besoins.

Dépendances
------------

Aucune.

Exemple Playbook
----------------

- Installation du rôle

```
mkdir -p $HOME/install-node-exporter/roles
```

```
vim $HOME/install-node-exporter/requirements.yml
```

```
- name: ansible-role-node-exporter
  src: https://github.com/willbrid/ansible-role-node-exporter.git
  version: main
```

```
cd $HOME/install-node-exporter && ansible-galaxy install -r requirements.yml --roles-path roles
```

- Utilisation du rôle dans un playbook

```
vim $HOME/install-node-exporter/playbook.yml
```

```
---
- hosts: monitoring
  become: yes

  vars:
  - node_exporter_version: "1.9.0"

  roles:
  - ansible-role-node-exporter
```

```
vim $HOME/install-node-exporter/hosts.ini
```

```
[monitoring]
192.168.56.4
192.168.56.5
```

```
cd $HOME/install-node-exporter && ansible-playbook -i hosts.ini playbook.yml
```

**NB:** Les adresses IP définies dans le fichier **$HOME/install-node-exporter/hosts.ini** sont fournies à titre d'exemple et doivent être remplacées par les vôtres.

Licence
-------

BSD,MIT

Informations sur l'auteur
------------------

William Bridge NGASSAM