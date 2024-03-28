# Ansible Role: Dokuwiki

Installs Dokuwiki on RedHat/CentOS/Rocky Linux and Debian/Ubuntu servers.


## Role Variables

### Configuration

    dokuwiki_title: string

The title of the Dokuwiki instance.


    dokuwiki_license: string

The license of the Dokuwiki instance.


     dokuwiki_url_rewrite: string

The URL rewrite setting for the Dokuwiki instance (0: none, 1: web server, 2: dokuwiki).


    dokuwiki_disable_actions: list

A list of actions to disable.


#### Access Control List

Parameters for groups `ALL` and `user`.
Values are to be chosen from the following list:

- `0`: no access
- `1`: read access
- `2`: edit access
- `4`: create access
- `8`: upload access
- `16`: delete access
- `255`: admin access


    dokuwiki_acl_all: "1"
    dokuwiki_acl_users: "4"

### Features


    dokuwiki_remove_plugins: list

A list of Dokuwiki plugins to remove.

    dokuwiki_plugins: list

A list of dictionaries, each containing the name and source URL of a Dokuwiki plugin to install.

    dokuwiki_templates: list

A list of dictionaries, each containing the name and source URL of a Dokuwiki template to install.



### Server Configuration

    dokuwiki_server_name: string

The server name for the Dokuwiki instance.

    dokuwiki_install_dir: string

The directory where Dokuwiki will be installed.

    dokuwiki_download_url: string

The URL from which the Dokuwiki tarball will be downloaded.

    dokuwiki_download_dir: string

The directory where the Dokuwiki tarball will be downloaded.

    dokuwiki_download_dest: string

#### Apache configuration

In addition to `geerlingguy.apache` role variables, the following variables are available:

    dokuwiki_apache_vhost: string

Actual name of the Dokuwiki tarball.

    dokuwiki_user: string

The user that will own the Dokuwiki files.

    dokuwiki_group: string

The group that will own the Dokuwiki files.


#### PHP Configuration

In addition to `benoistlaurent.ansible-role-php` role variables, the following variables are available:

    dokuwiki_php_packages: list

The PHP packages the Dokuwiki instance needs to operate properly.

    dokuwiki_php_version: string

The PHP version that will be installed. 



## Dependencies

- https://github.com/benoistlaurent/ansible-role-php


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
 
  tasks:
    - name: Properly setup firewall
      firewalld:
        service: http
        permanent: yes
        state: enabled
        immediate: yes
```

*Inside `vars/main.yml`*:

```yaml
---
dokuwiki_title: "The Wiki"
dokuwiki_plugins:
  - name: "note"
    src: "https://github.com/lpaulsen93/dokuwiki_note/archive/refs/tags/2020-06-28.tar.gz"

server_name: "dokuwiki"
fqdn: "{{ server_name }}.test"
server_root: "/var/www/html/{{ server_name }}"
```


## TODO

- Support dokuwiki configuration (a.k.a. wiki name, admin password, etc.)
- Support plugin installation

## License

MIT / BSD


