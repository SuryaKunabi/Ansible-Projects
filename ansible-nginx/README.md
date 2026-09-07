# Ansible Nginx Installation

## Description

This project demonstrates how to use **Ansible** to automate the installation and configuration of the **Nginx web server** on a remote Ubuntu server.
Instead of installing Nginx manually, an Ansible playbook is used to perform the installation and start the Nginx service automatically.

## Technologies Used
* Ansible
* Ubuntu Linux
* Nginx
* YAML
* SSH

## Project Structure:
ansible-nginx/
│
├── inventory       # Remote server details
│
├── nginx.yml       # Ansible playbook
│
└── README.md       # Project documentation

## Tasks Performed
The Ansible playbook:
1. Connects to the remote server using SSH.
2. Updates the APT package cache.
3. Installs Nginx.
4. Starts the Nginx service.
5. Enables Nginx to start automatically after reboot.

## How to Run
Check the connection:
ansible all -i inventory -m ping

Run the playbook:
ansible-playbook -i inventory nginx.yml

## Verification
Check the Nginx service:
systemctl status nginx

* Automated software installation and service management.
* Practiced remote server management using Ansible.
