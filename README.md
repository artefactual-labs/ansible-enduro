# ansible-enduro

Ansible role for deploying [Enduro](https://github.com/artefactual-labs/enduro)

Based on [cloudalchemy.memcached_exporter](https://github.com/cloudalchemy/ansible-memcached-exporter/)


- It requires Artefactual's Nginx, Percona and Temporal roles, based on the excelent work from [@geerlingguy](https://github.com/geerlingguy). Add this to your requirements.yml file:


```
- src: "https://github.com/artefactual-labs/ansible-percona"
  branch: "master"
  name: artefactual.percona
  
- src: "https://github.com/artefactual-labs/ansible-nginx"
  branch: "master"
  name: "artefactual.nginx"

- src: "https://github.com/artefactual-labs/ansible-temporal"
  branch: "master"
  name: "artefactual.nginx"

- src: "https://github.com/artefactual-labs/ansible-enduro"
  branch: "main"
  name: "artefactual.enduro"

```

- Sample playbook, intended to be used against an already installed Archivematica instance:

```
- hosts: "all"
  become: true
  roles:
    - role: "artefactual.percona"
      mysql_users: "{{ enduro_mysql_users }}"
      mysql_databases: "{{ enduro_mysql_databases }}"
      mysql_timezone_info: "true"
    - role: "artefactual.nginx"
      nginx_sites: "{{ enduro_nginx_sites }}"
    - role: "artefactual.enduro"
```

Enduro will be available at port 8020


Default variables:
```
enduro_version: "latest"
enduro_binary_local_dir: ""
enduro_listen_address: "127.0.0.1:9001"
enduro_listen_api_address: "127.0.0.1:9000"

# Enduro database
enduro_db_user: "enduro"
enduro_db_pass: "enduro%123"
enduro_db_host: "localhost"
enduro_db_name: "enduro"

# Internal variables
enduro_system_user: "enduro"
enduro_system_group: "enduro"
```
