Nginx load balancer
=========

Configures Nginx to use upstream to dispatch requests to healty instances only. If it detects a faulty header status such as 500 error codes, it will stop sending request to the same server. It reads the instance IP addresses from the inventory file of the Ansible project. 


Example Playbook
----------------

    - hosts: loadbalancer
      roles:
         - { role: nginx }
         
 create a host file on your local PC to point to the Nginx loadbalancer IP address
 
 192.168.1.0 devops-northeast.com

License
-------

BSD

Author Information
------------------

Soroush Atarod atarod@infinitypp.com
