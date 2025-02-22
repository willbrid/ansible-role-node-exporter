Ansible-role-node-exporter
=========

Ce rôle Ansible installe et configure **Node Exporter**, un agent Prometheus conçu pour exposer les métriques matérielles et système des environnements Linux.

Exigences
------------

Un système Linux utilisant **systemd** comme gestionnaire de services.

Description des Variables
--------------



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
  - 

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