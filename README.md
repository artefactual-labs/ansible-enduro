# ansible-aipscan

Ansible role for deploying [Enduro](https://github.com/artefactual-labs/enduro)

Based on [cloudalchemy.memcached_exporter](https://github.com/cloudalchemy/ansible-memcached-exporter/)

- Installs and configures [Cadence](https://github.com/uber/cadence) and [Cadence-web](https://github.com/uber/cadence-web)

- It requires Artefactual's Nginx and Percona roles, based on the excelent work from [@geerlingguy](https://github.com/geerlingguy). Add this to your requirements.yml file:


```
- src: "https://github.com/artefactual-labs/ansible-percona"
  branch: "master"
  name: artefactual.percona
  
- src: "https://github.com/artefactual-labs/ansible-nginx"
  branch: "master"
  name: "artefactual.nginx"

- src: "https://github.com/artefactual-labs/ansible-enduro"
  branch: "main"
  name: "artefactual.enduro"

```

- Sample playbook, intended to be used against an already installed Archivematica instance:

```
- hosts: all
  become: true
  vars:
    enduro_http_user: "enduro"
    enduro_http_password: "artefactual"
  roles:
    - artefactual.nginx
    - artefactual.percona
    - artefactual.enduro
```

Enduro will be available at port 8090, with user "enduro" and password "artefactual".


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

# Cadence database
cadence_db_user: "cadence"
cadence_db_pass: "cadence123P$"
cadence_db_host: "localhost"
cadence_db_name: "cadence"

# Visibility database
cadence_visibility_db_user: "visibility"
cadence_visibility_db_pass: "visibility123P$"
cadence_visibility_db_host: "localhost"
cadence_visibility_db_name: "visibility"

cadence_web_path: "/usr/share/cadence-web"
cadence_web_version: "3.4.1"

# Internal variables
enduro_system_user: "enduro"
enduro_system_group: "enduro"
cadence_system_user: "cadence"
cadence_system_group: "cadence"

```
