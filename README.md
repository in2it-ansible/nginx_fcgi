Nginx FastCGI
=============

[![Build Status](https://travis-ci.org/in2it-ansible/nginx_fcgi.svg?branch=master)](https://travis-ci.org/in2it-ansible/nginx_fcgi)

This role will setup a Nginx web server that passes incoming requests to a remote FastCGI application (using PHP-FPM).

Requirements
------------

No specific requirements needed

Role Variables
--------------

The following variables are used within the role defined in `defaults/main.yml` and overridden by `vars/main.yml`:

- **nginx_timezone:** Sets the timezone the server will be running in (default: UTC)
- **nginx_apt_key:** The official Nginx GPG Public Key (default: https://nginx.org/keys/nginx_signing.key)
- **nginx_apt_keyid:** The official Nginx GPG Public Key ID (default: ABF5BD827BD9BF62)
- **nginx_apt_list:** The Nginx repository (default: "deb http://nginx.org/packages/debian {{ ansible_lsb.codename }} nginx")
- **server_hostname:** Setting the hostname Nginx will listen to (default: {{ inventory_hostname }}.example.com)
- **nginx_docroot:** The document root of the application to display content (default: "/var/www/app")
- **nginx_user_group:** The user group used for the web application (default: webapp)
- **nginx_user_name:** The user name used for the web application (default: webapp)
- **package:** The package to install (default: nginx)

The following variables are used in `templates/nginx_fcgi.conf`:

- **ansible_host:** The hostname or IP address of the hosts used for the web server (see Example Inventory)

Dependencies
------------

No dependencies

Example Inventory
-----------------

    [all]
    web1 ansible_host=192.168.2.1
    web2 ansible_host=192.168.2.2
    
    [web]
    web1
    web2

Example Playbook
----------------

    - name: Provision boxes
      hosts: all
      become: true
      roles:
        - { role: all, tags: [ 'common', 'all' ] }
    
    - name: Set up the web server
      hosts: web
      become: true
      roles: 
        - { role: nginx, tags: [ 'nginx', 'web' ] }

License
-------

MIT

Author Information
------------------

Michelangelo van Dam (michelangelo+github@in2it.be)
