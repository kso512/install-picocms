[![Build Status](https://travis-ci.org/kso512/install-picocms.svg?branch=master)](https://travis-ci.org/kso512/install-picocms)

# install-picocms

An [Ansible](https://www.ansible.com/) [Role](http://docs.ansible.com/ansible/playbooks_roles.html#roles) to install [PicoCMS](http://docs.ansible.com/ansible/playbooks_roles.html#roles).

PicoCMS is a "stupidly simple & blazing fast, flat file CMS."

## Requirements

For TLS, create a TLS certificate and key pair, then assign it to the role.

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
| install_picocms_content_src | Source content folder | `{{ install_picocms_httpdocs }}/content-sample` |

## Dependencies

PicoCMS requires PHP and a web server to run on top of.  

I chose roles from [geerlingguy](https://github.com/geerlingguy) to do that:

- [geerlingguy.apache](https://github.com/geerlingguy/ansible-role-apache)
- [geerlingguy.php](https://github.com/geerlingguy/ansible-role-php)
- [geerlingguy.apache-php-fpm](https://github.com/geerlingguy/ansible-role-apache-php-fpm)

### Overrides

    apache_remove_default_vhost: true
    apache_global_vhost_settings: |
      DirectoryIndex index.php index.html
    apache_vhosts:
      - servername: "{{ ansible_fqdn }}"
        documentroot: "/var/www/html"
        extra_parameters: |
              ProxyPassMatch ^/(.*\.php(/.*)?)$ "fcgi://127.0.0.1:9000/var/www/html"
    php_enable_php_fpm: true
    php_packages_extra:
      - libapache2-mod-fastcgi

## Example Playbook

Complete example: 

    - hosts: servers
      roles:
         - { role: kso512.install-picocms, apache_remove_default_vhost: true }

## License

BSD

## Author Information

> Chris Lindbergh
