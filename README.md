[![CircleCI](https://circleci.com/gh/miyuk/ansible_nginx_certificate.svg?style=svg)](https://circleci.com/gh/miyuk/ansible_nginx_certificate)

# NGNIX Certificate

This is an Ansible role to Install Certificate and Private Key for NGNIX server.

## Role Variables

| Variable | Description | Default |
| --- | --- | --- |
| `nginx_src_crt_path` | source certificate path. this file is on server to play this role. | "{{ certificate_directory }}/{{ certificate_crt_filename }}" |
| `nginx_src_key_path` | source private key path. this file is on server to play this role. | "{{ certificate_directory }}/{{ certificate_crt_filename }}" |
| `nginx_dest_crt_force_create` | force create certfiicate if this variable is `yes` | yes |
| `nginx_dest_key_force_create` | force create private key if this variable is `yes` | yes |
| `nginx_dest_crt_path` | destination certificate path. this file is on server to play this role. | /etc/nginx/certs/server.crt |
| `nginx_dest_key_path` | destination private key path. this file is on server to play this role. | /etc/nginx/certs/server.key |
| `nginx_dest_crt_mode` | destination certificate file permission | 0644 |
| `nginx_dest_key_mode` | destination private key file permission | 0600 |
| `nginx_dest_files_owner` | destination certificate owner | root |
| `nginx_dest_files_group` | destination certificate group | root |
| `nginx_restart` | when restart service or docker container if change `upload certificate/private key` status and this variable is `yes` | yes |
| `nginx_docker_dir` | nginx docker compose directory if `nginx_daemon_type` is `docker` | /opt/nginx |
| `nginx_daemon_type` | daemon type for restart service, `service` or `restart` | docker |
| `nginx_docker_name` | nginx docker compose service name if `nginx_daemon_type` is `docker` | nginx |

## Install

this module name is `nginx_certificate`. So, you try to install below command under Ansible Playbook folder.

```bash
cd roles
git clone git@github.com:miyuk/ansible_nginx_certificate.git nginx_certificate
```

## Example Playbook

Install certificate from `<playbook directory>/certs`.

```yaml
---
- hosts: localhost
  connection: local
  vars:
    nginx_src_crt_path: "./certs/{{ certificate_crt_filename }}"
    nginx_src_key_path: "./certs/{{ certificate_crt_filename }}"
    nginx_dest_crt_force_create: yes
    nginx_dest_key_force_create: yes
    nginx_dest_crt_path: /etc/nginx/certs/server.crt
    nginx_dest_key_path: /etc/nginx/certs/server.key
    nginx_dest_crt_mode: 0644
    nginx_dest_key_mode: 0600
    nginx_dest_files_owner: root
    nginx_dest_files_group: root
    nginx_restart: yes
    nginx_docker_dir: /opt/nginx
    nginx_daemon_type: docker
    nginx_docker_name: nginx
  roles:
    - nginx_certificate
```