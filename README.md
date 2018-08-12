# Zero Downtime Deployment using Ansible
This project demonstrates how to implement a Zero Downtime deployment using Ansible for an architecture behind a load balancer.

<img src="https://raw.githubusercontent.com/soroushatarod/devops-north-east-ansible/master/ansible-devops-northeast.png">

1) Nginx is used as the load balancer
2) Apache servers which serves a PHP application

our application is in folder newcastle.
to trigger a fail deployment modify the newcastle/files/code/index.php by having a syntax error.
During our continous deployment we check the syntax of the file. If it detects an invalid syntax it will trigger a fail job and will stop deploying to other servers. 

If there are no syntax errors the release will be going to the remaining servers.

<h2>Nginx key config points</h2>

Nginx is configured to stop sending requests to faulty instances.

if it detects one of these header status it will stop sending the request to that instance using the below line.
this can be found in 

```
provisioning\nginx\templates\nginx.conf.j2
proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
```

<h2>How does the deployment works?</h2>
Ansible by default runs tasks on every single host. example: if there is a task to do git pull and if there are  4 IP's in the inventory. It will run the git pull on each of these 4 servers then move on to the next task.

However, in a continous deployment to provide a fault tolerent architecture. We need to change this behaviour!. This is why we would be using the serial keyword.

```
hosts: webservers
serial: 1
roles:
  - deploy
```

The serial key means to run the role deploy to only one IP and if everything works fine, run it on the rest. By doing this we are providing a fault tolerent deployment.

```
[webservers]
192.168.0.5
192.168.0.6
192.168.0.7
```
This means our job will run on <strong>192.168.0.5</strong>. If it works fine, it will run on the remaining servers.
