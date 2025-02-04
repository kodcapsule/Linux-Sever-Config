
# Linux Server  Configuration 
This project demonstrates the  use of **Ansible** to manage  the configuration  of  a Linux server. The playbook uses four roles to automate the the updates of the server, install some essential utilities,  installs and confiures **Nginx** uploads a static HTML website and adds a given public key to the server.   



## Learning Objectives

## Prerequisites

Before you begin, make sure you have  the following  setup:

1. Ansible Installed: Ensure that  **Ansible** is Installed  on your local machine. you can follow the [Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html)  to install **Ansible**. 

2. A Remote Linux Server: You need a server running Linux server  either on a cloud provider like AWS, DigitalOcean, or any other cloud provider.

3. SSH Access: Ensure that you can SSH into the server using the specified username.

4. Website Tarball: You must have a tarball (website.tar.gz) containing your static HTML website to upload.
5. Knowledge of Ansible: You should have some basic knowledge of **Ansible**



## Table of Contents
- [1. Project Structure](#1-project-structure)
- [2. Project Setup](#2-project-setup)
- [3. Roles](#3-roles)
- [4. Playbook](#4-playbook)
- [5. Conclusion](#5-conclusion)



## 1. Project Structure

```bash
        Linux-Sever-Config/
            ├── roles
            ├── .gitignore
            ├── inventory.ini
            ├── Readme.md
            ├── setup.yml
            └── website.tar.giz
```



## 2. Project Setup
Steps to set up the project, including dependencies and installation.
1. Clone the repository:
```bash
    git clone https://github.com/kodcapsule/Linux-Sever-Config
```
change directory into Linux-Sever-Config

```bash    
    git Linux-Sever-Config
```


2. Update  the Inventory File: Update  the target hosts in  the  inventory.ini file  with your server details:

```bash    
   [server]
   192.168.1.3 ansible_user=ubuntu
```
3. Create  the Tarball: Create and place your website.tar.gz file in the root of this project or you can specify its location in the playbook.

4. Setup  SSH Connection: Make sure your SSH key is properly set up for Ansible to connect to the target machine.


## 3. Roles
This section of the project contains all the roles that are used in this project. There are four roles in all which are:
**1. base:** The base role  perform some basic server configuartions including 
- 1. installs utilities like vim, git,curl,wget,vim,htop
- 2. Updates system packages.
- 3. Installs and starts Fail2ban


**2. nginx:** Installs and configures nginx
- 1. Installs a specific version of Nginx (default version 1.18.0-0ubuntu1.3)
- 2. Ensures that  Nginx is running and enabled on boot
- 3. Copy the Nginx configuration file and other files  to the host


**3. ssh:** adds the given public key to the server
- 1. Ensures the ssh user exists in the host
- 2. Ensures that the  .ssh directory exists in the hosts
- 3. Copies the given public key to authorized_keys in the hosts

**4. app:** uploads the given tarball of a static HTML website to the server and unzips it.
- 1. Creates a  target directory 
- 2. Uploads website tarball to the directory and extracts website tarball
- 3. Deploy Nginx configuration and enable Nginx site


## 4. Playbook
The playbook is uses all the executes all the roles on target servers  



## 5. Conclusion

