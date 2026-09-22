# Ansible Static Website Deployment

A simple Ansible Role project to deploy a static website on an Ubuntu EC2 instance using Nginx.

## Architecture

```text
Ansible Controller (EC2)
        |
        | SSH
        ↓
Web Server (EC2)
        |
        ↓
      Nginx
        |
        ↓
 /var/www/html/
 ├── index.html
 ├── service.html
 ├── contact.html
 └── style.css
```

## Technologies

* AWS EC2
* Ubuntu
* Ansible
* Ansible Roles
* Nginx
* HTML
* CSS
* SSH

## Project Structure

```text
ansible-static-site/
├── README.md
├── inventory
├── playbook.yml
└── roles/
    └── static_web/
        ├── tasks/
        │   └── main.yml
        └── files/
            ├── index.html
            ├── service.html
            ├── contact.html
            └── style.css
```

## Setup

### 1. Install Ansible

On the Ansible Controller:

```bash
sudo apt update
sudo apt install ansible -y
```

Check installation:

```bash
ansible --version
```

### 2. Configure Inventory

Edit the `inventory` file:

```ini
[webservers]
web1 ansible_host=WEB_SERVER_PRIVATE_IP ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/mykey.pem
```

Replace the IP address and SSH key path with your actual values.

### 3. Test Connection

```bash
ansible all -i inventory -m ping
```

Expected:

```text
web1 | SUCCESS
```

### 4. Check Playbook

```bash
ansible-playbook -i inventory playbook.yml --syntax-check
```

### 5. Deploy Website

```bash
ansible-playbook -i inventory playbook.yml
```

The Ansible role will:

1. Install Nginx.
2. Start and enable Nginx.
3. Copy the HTML and CSS files.
4. Deploy them to `/var/www/html/`.

## AWS Security Group

For the Web Server EC2 instance, allow:

| Type | Port | Source               |
| ---- | ---: | -------------------- |
| SSH  |   22 | Controller / Your IP |
| HTTP |   80 | `0.0.0.0/0`          |

Port 80 is required to access the website from a browser.

## Verify Deployment

Check Nginx:

```bash
sudo systemctl status nginx
```

Check website files:

```bash
ls -l /var/www/html/
```

Expected:

```text
index.html
service.html
contact.html
style.css
```

Test locally:

```bash
curl http://localhost
```

## Access the Website

Open the Web Server's public IP in a browser:

```text
http://WEB_SERVER_PUBLIC_IP
```

Pages:

```text
http://WEB_SERVER_PUBLIC_IP/
http://WEB_SERVER_PUBLIC_IP/service.html
http://WEB_SERVER_PUBLIC_IP/contact.html
```

## Ansible Role

The `static_web` role contains:

* `tasks/main.yml` — installs Nginx and deploys the website.
* `files/` — contains the static website files.

The website files are copied to:

```text
/var/www/html/
```

Nginx then serves the website over HTTP.

## Learning Objectives

This project demonstrates:

* AWS EC2
* Linux
* SSH
* Ansible Inventory
* Ansible Playbooks
* Ansible Roles
* Nginx
* Static Website Deployment
* Configuration Management
* Basic DevOps Automation
