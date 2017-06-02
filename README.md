[![Build Status](https://travis-ci.org/kso512/install-picocms.svg?branch=master)](https://travis-ci.org/kso512/install-picocms)

# install-picocms

An Ansible Role to install PicoCMS.

http://picocms.org/

## Requirements

Create a TLS certificate and key pair, then assign it to the role.

## Role Variables

| Variable | Description | Default Value |
| -------- | ----------- | ------------- |
| install_picocms_x |  | `` |

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
         - { role: kso512.install-picocms, x: 42 }

## License

BSD

## Author Information

> Chris Lindbergh
