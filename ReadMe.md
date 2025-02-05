
# Linux Server  Configuration 
This project demonstrates the  use of **Ansible** to manage  the configuration  of  a Linux server. The playbook uses four roles to automate the the updates of the server, installation of  some essential utilities,  installs and confiures **Nginx** and uploads a static HTML website and adds a given public key to the server.  The project is found at  https://roadmap.sh/projects/configuration-management as part of DevOps Roadmap.



## Learning Objectives
By the end of this project you should
1. Understand the folder structure of ansible role
2. How to create a task.
3. Understand the use of ansible.builtin collections
3. How to create and use roles in a Playbook

## Prerequisites

Before you begin, make sure you have  the following  setup:

1. Ansible Installed: Ensure that  **Ansible** is Installed  on your local machine. you can follow the [Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html)  to install **Ansible**. 

2. A Remote Linux Server: You need a Linux  server running   either on a cloud provider like **AWS**, **DigitalOcean**, or any other cloud provider.

3. SSH Access: Ensure that you can SSH into the server using the specified username.

4. Website Tarball: You must have a tarball (website.tar.gz) containing your static HTML website to upload.

5. Knowledge of Ansible: You should have some basic knowledge of **Ansible**



## Table of Contents
- [1. Project Structure](#1-project-structure)
- [2. Project Setup](#2-project-setup)
- [3. Roles](#3-roles)
- [4. Running the Playbook](#4-running-the-playbook)
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
    cd Linux-Sever-Config
```


2. Update  the Inventory File: Update  the target hosts in  the  inventory.ini file  with your server details:

```bash    
   [server]
   192.168.1.3 ansible_user=ubuntu
```

3. Create  the Tarball: Create and place your website.tar.gz file in the root of this project or you can specify its location in the playbook.

```bash   
    tar -czvf website.tar.gz website/
```

4. Setup  SSH Connection: Make sure your SSH key is properly set up for Ansible to connect to the target machine.

```bash    
    ssh-copy-id -f "-o IdentityFile <PATH_TO_YOUR_KEY_PAIR>" ubuntu@192.168.1.3 
```

5. Run an initial test to confirm that ansible is able to connect to the remote hosts

```bash  
   ansible -i inventory.ini -m ping
```


## 3. Roles
This section of the project contains all the roles that are used in this project. There are four roles in all which are:

**1. base:** The base role  perform some basic server configuartions including 
- 1. installs utilities like vim, git,curl,wget,vim and htop
- 2. Updates system packages.
- 3. Installs and starts Fail2ban


**2. nginx:** This roles performs the following 
- 1. Installs a specific version of Nginx (default version 1.18.0-0ubuntu1.3)
- 2. Ensures that  Nginx is running and enabled on boot
- 3. Copy the Nginx configuration file  to the hosts


**3. ssh:** Adds the given public key to the host by:
- 1. Ensuring that  the ssh user exists in the host
- 2. That the  .ssh directory exists in the hosts
- 3. Copies the given public key to authorized_keys in the hosts

**4. app:** Uploads the given tarball of a static HTML website to the server and unzips it.
- 1. Creates a  target directory 
- 2. Uploads website tarball to the directory and extracts website tarball
- 3. Deploy Nginx configuration and enable Nginx site


## 4. Running the Playbook
To run  the playbook, run the following command:

Run all the roles
```bash
ansible-playbook -i invenory.ini  setup.yml
```

Run only the app role
```bash
ansible-playbook -i invenory.ini  setup.yml --tags "app"
```




## 5. Conclusion

That's all for today. 