Role Name
=========

Installs php 7.2

Requirements
------------

Needs Apache

Role Variables
--------------

Include extensions in the vars folder
There are two folders one for Debian and one for RedHat

Include the extensions you need to install in these two folders

php_extensions:
  - php
  - php7.2-common
  - php7.2-mysql
  - php7.2-curl
  - php7.2-tidy
  - php7.2-xml
  - php7.2-xmlrpc
  - php7.2-mbstring
  - php7.2-zip

Dependencies
------------

apache


Example Playbook
----------------

    - hosts: webserver
      roles:
         - { role: php }

License
-------

BSD

Author Information
------------------

Soroush Atarod atarod@infinitypp.com