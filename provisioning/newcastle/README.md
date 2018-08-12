Newcastle
=========

Installs the Newcastle application

Requirements
------------

Needs Apache

Role Variables
--------------

# the application release number
release_version_number: 4
# the path to install the application
install_path : '/var/www/html'


Dependencies
------------

apache


Example Playbook
----------------

    - hosts: webserver
      roles:
         - { role: newcastle }

License
-------

BSD

Author Information
------------------

Soroush Atarod atarod@infinitypp.com
