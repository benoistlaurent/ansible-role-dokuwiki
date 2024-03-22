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


## Dependencies

- geerlingguy.apache
- geerlingguy.php

## Example Playbook


## TODO

- Support dokuwiki configuration (a.k.a. wiki name, admin password, etc.)
- Support plugin installation

## License

MIT / BSD


