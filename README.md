Ansible role: PHP-FPM
===================
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-lukasz--zaroda.php--fpm-000000.svg)](https://galaxy.ansible.com/lukasz-zaroda/php-fpm/)

PHP-FPM installation, configuration, and easy pool management for both PHP 5 and PHP 7 versions.

Requirements
------------

None.

Role Variables
--------------

**php_pools_defaults**

This is a dictionary of settings, which will be added to all pools. For example:

```
php_pools_defaults:
  pm.max_children: 10
  pm.start_servers = 5
```
The above example will make all pools to have maximum number of processes limited to 10,
and 5 processes started from the beginning waiting for requests.

**php_pools**

This is a dictionary of pools. It has two levels, in first level you have to choose
a PHP version (5 or 7), and on second level - a name of the pool and its settings.
For example:

```
php_pools:
  5:
    example1.com:
      user: example1
      group: example1
  7:
    example2.com:
      user: example2
      group: example2
    example3.com:
      user: example3
      group: example3
```
The above example will create three pools, one with PHP 5 and two with PHP 7. Each pool
has indivually set _user_ and _group_ settings.

This role is created mainly for Debian, but you can look into _defaults/main.yml_
for more variables to override, which may allow you to customize this role for other system.

Dependencies
------------

None.

Example Playbook
----------------

```yml

---
- hosts: servers
  become: true
  become_method: sudo
  roles:
  - role: php-fpm
  
    php_pools_defaults:
      pm.max_children: 10
      pm.start_servers = 5
      
    php_pools:
      5:
        example1.com:
          user: example1
          group: example1
      7:
        example2.com:
          user: example2
          group: example2
        example3.com:
          user: example3
          group: example3
      
```

License
-------

MIT

Author Information
------------------

Łukasz Zaroda - https://luken-tech.pl