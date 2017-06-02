[![Build Status](https://travis-ci.org/kso512/install-picocms.svg?branch=master)](https://travis-ci.org/kso512/install-picocms)

# install-picocms

An Ansible Role to install PicoCMS.

http://picocms.org/

## Requirements

Create a TLS certificate and key pair, then assign it to the role.

## Role Variables

| Variable | Description | Default Value |
| -------- | ----------- | ------------- |
| install_picocms_version | Version of PicoCMS to install | `1.0.5` |
| install_picocms_filename | Short filename of the PicoCMS source archive | `pico-release-v{{ install_picocms_version }}.tar.gz` |
| install_picocms_url | URL of PicoCMS source archive to download | `https://github.com/picocms/Pico/releases/download/v{{ install_picocms_version }}/{{ install_picocms_filename }}` |
| install_picocms_dest | Local location of PicoCMS source archive | `/root/{{ install_picocms_filename }}` |
| install_picocms_owner | Owner of local PicoCMS source archive | `root` |
| install_picocms_group | Group of local PicoCMS source archive | `{{ install_picocms_owner }}` |
| install_picocms_httpdocs | HTTPDOCS folder to extract into | `/var/www/html` |

## Dependencies

PicoCMS requires PHP and a web server to run on top of.  

I chose roles from geerlingguy to do that:

- geerlingguy.apache
- geerlingguy.php
- geerlingguy.apache-php-fpm

Overrides passed:

-  apache_remove_default_vhost: true

## Example Playbook

Complete example: 

    - hosts: servers
      roles:
         - { role: kso512.install-picocms, apache_remove_default_vhost: true }

## License

BSD

## Author Information

> Chris Lindbergh
