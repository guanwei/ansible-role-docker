# Ansible Role: Docker

Installs Docker on Debian/Ubuntu.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
docker_apt_arch: amd64
docker_apt_repository: "deb [arch={{ docker_apt_arch }}] https://download.docker.com/linux/{{ ansible_distribution | lower }} {{ ansible_distribution_release }} stable"

# docker_http_proxy: http://proxy.example.com:80
# docker_https_proxy: https://proxy.example.com:443
# docker_no_proxy: localhost,127.0.0.1,docker-registry.example.com,.corp
docker_default_no_proxy: 127.0.0.1,localhost,.local,.internal

docker_add_current_user_to_group: true
```

`docker_apt_arch` must be set same with your system architecture.

`docker_http_proxy`、`docker_https_proxy`、`docker_no_proxy` will be added to `/etc/systemd/system/docker.service.d/http-proxy.conf` file on Linux.

if one of `docker_http_proxy`、`docker_https_proxy`、`docker_no_proxy` set, but `docker_no_proxy` not set, `docker_default_no_proxy` will be used as `docker_no_proxy`.

`docker_add_current_user_to_group` control whether add current user to docker group.

## Dependencies

None.

## Example Playbook

requirements.yml
```
- name: docker
  src: <repo_url>
  version: <branch_name>
  scm: git
```

playbook.yml
```
- hosts: servers
  roles:
    - docker
```
