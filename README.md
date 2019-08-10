# Creating multi-site development environment with Docker in Mac

Docker environment for multiple project.
  - vagrant centos 7 with docker to speedup https://www.heyer-it.de/2019/03/11/tuning-for-docker-on-mac/
  - haproxy docker to proxy to other web service

## Getting Started

- With Vagrant and VirtualBox, We are able to have seperarate environment. E.g difference PHP or MySql versions for difference projects. The biggest problem when need to run few project together or micro services project which multiple programmer languages. It consumes a lot of host resource. 
- You know Docker is more lightweight and with docker for mac you can easier to develop multiple project or multiple micro service on time. But Docker for Mac had poor performance compared to use in Linux system. 

==> KEY:
 - I create a Vagrant machine base on Centos7 with latest docker-ce. Use NFS mount to good I/O performance. 
 - I start HAProxy container to handle any sets of project containers. Each project can have web server, database, queue services, Elasticsearch or other when needed, all completely separate between projects.

 **Now, With only one a Virtualbox, I can run multiple docker environments on MAC with good performance.**

 ![alt text](https://github.com/manhtl/mac-docker/blob/master/docker-local.jpeg "")

### Prerequisites

 - Install VirtualBox, Vagrant on MAC https://sourabhbajaj.com/mac-setup/Vagrant/README.html

### Installing

Change vagrantfile to mount your working dir
Setup virtualbox

```
vagrant up
vagrant reload
vagrant ssh

```

Start haproxy

```
cd /vagrant_data/{path_to_docker}
docker-compose up
```
