# Ansible Nginx Installation

## Description

This project uses Ansible to automatically install and start Nginx on a remote Ubuntu server.

## Technologies

* Ansible
* Ubuntu
* Nginx
* YAML
* SSH

## Run
bash :
ansible all -i inventory -m ping
ansible-playbook -i inventory nginx.yml

## Result
Nginx is installed and running on the remote server.
