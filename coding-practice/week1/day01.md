## Day 01 - Basic

Ansible Task - Install Nginx on Pathnex Server

Rewrite the YAML maually: 
    

```yaml

   -name: Install Nginx on Pathnex server
    hosts: all
    become: yes

    tasks: 
      
      -name: Install nginx
      yum:
        name: nginx
        state: present

    

    Docker

    # Docker installation & first container
    
    docker --version
    docker run ubuntu echo "Hello user"

    # Docker File
    FROM ubuntu:22.04
    CMD ["echo", "Hello Pathnex"]
