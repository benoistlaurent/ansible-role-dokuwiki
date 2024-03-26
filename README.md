# Ansible Role: Dokuwiki

Installs Dokuwiki on RedHat/CentOS/Rocky Linux and Debian/Ubuntu servers.

## Requirements


## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    dokuwiki_install_dir: string

The directory where Dokuwiki will be installed.

    dokuwiki_download_url: string

The URL from which the Dokuwiki tarball will be downloaded.

    dokuwiki_user: string

The user that will own the Dokuwiki files.

    dokuwiki_group: string

The group that will own the Dokuwiki files.

    dokuwiki_php_packages: list

The PHP packages that need for Dokwiki to operate properly

    dokuwiki_php_version: string

The PHP version that will be installed.



## Dependencies

- benoistlaurent.ansible-role-php

## Example Playbook

```yaml
---
- hosts: all

  vars_files:
    - vars/main.yml

  roles:
    - role: geerlingguy.apache
      vars:
        apache_vhosts:
          - servername: "{{ fqdn }}"
            documentroot: "{{ server_root }}"
    - role: ansible-role-dokuwiki
      vars:
        dokuwiki_server_name: "{{ server_name }}"
        dokuwiki_install_dir: "{{ server_root }}"
    - role: geerlingguy.firewall
      vars:
        firewall_allowed_tcp_ports:
          - "80"
          - "443"
```

*Inside `vars/main.yml`*:

```yaml
---
server_name: "dokuwiki"
fqdn: "{{ server_name }}.test"
server_root: "/var/www/html/{{ server_name }}"
```


## TODO

- Support dokuwiki configuration (a.k.a. wiki name, admin password, etc.)
- Support plugin installation

## License

MIT / BSD


