# Zero Downtime Deployment using Ansible
This project demonstrates how to implement a Zero Downtime deployment using Ansible for an architecture behind a load balancer.

<img src="https://raw.githubusercontent.com/soroushatarod/devops-north-east-ansible/master/ansible-devops-northeast.png">

1) Nginx is used as the load balancer
2) Apache servers which serves a PHP application

our application is in folder newcastle.
to trigger a fail deployment modify the newcastle/files/code/index.php by having a syntax error.
During our continous deployment we check the syntax of the file. If it detects an invalid syntax it will trigger a fail job and will stop deploying to other servers. 

If there are no syntax errors the release will be going to the remaining servers.

<h2>Nginx key confing points</h2>

Nginx is configured to stop sending requests to faulty instances.

if it detects one of these header status it will stop sending the request to that instance using the below line.
this can be found in 

```
provisioning\nginx\templates\nginx.conf.j2
proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
```
