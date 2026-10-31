#  Ansible & AWS EC2 Automation

# DevOps Configuration Management using Ansible & AWS EC2

## 📌 Project Overview
This repository contains the configuration management and automation solution for deploying a multi-tier web server infrastructure on AWS EC2 using **Ansible**. 

The playbook automates system updates, Nginx web server installation, service state verification, and web application code deployment across multiple EC2 target instances from a single Ansible Control Node.

---

## 🏗️ Architecture & Workflow

```text
               +----------------------------------+
               |      Ansible Control Node        |
               |      (WSL / Local Machine)       |
               +----------------+-----------------+
                                |
                   SSH (Port 22) | Private Key (.pem)
                                |
               +----------------+-----------------+
               |                                  |
    +----------v----------+            +----------v----------+
    |  AWS EC2 Instance 1 |            |  AWS EC2 Instance 2 |
    |   (Target Web01)    |            |   (Target Web02)    |
    |    Nginx Server     |            |    Nginx Server     |
    +---------------------+            +---------------------+
🛠️ Tech Stack & Prerequisites
Cloud Provider: AWS EC2 (Ubuntu 24.04 LTS / 22.04 LTS)

Configuration Management: Ansible 2.19+

Control Node Environment: WSL (Ubuntu) / Linux / macOS

Text Editor & IDE: Visual Studio Code

Remote Access: SSH key pair (ansible-key.pem)

📁 Repository Structure
Plaintext
devops-ansible-project/
├── ansible.cfg              # Ansible global default configurations
├── inventory/
│   └── aws_hosts.ini        # Target EC2 public IPs and SSH variables
├── site.yml                 # Playbook for installing Nginx & deploying site
├── index.html               # Custom HTML web application landing page
└── README.md                # Project documentation
🚀 Execution Guide
1. Configure Inventory
Update inventory/aws_hosts.ini with your active AWS EC2 Public IPv4 addresses:

Ini, TOML
[webservers]
web01 ansible_host=51.20.115.127
web02 ansible_host=16.171.242.90

[webservers:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/ansible-key.pem
ansible_python_interpreter=/usr/bin/python3
2. Verify SSH Connectivity (Ping Test)
Run the Ansible ping module to verify connectivity to both target servers:

Bash
ANSIBLE_HOST_KEY_CHECKING=False ansible webservers -i inventory/aws_hosts.ini -m ping
3. Run the Ansible Playbook
Execute the playbook to automate web server configuration:

Bash
ANSIBLE_CONFIG=./ansible.cfg ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory/aws_hosts.ini site.yml

Web Verification: Navigate to http://<EC2_PUBLIC_IP_1> and http://<EC2_PUBLIC_IP_2> in a web browser to confirm the deployed application landing page.

Author: Sarvesh Pandey (PRN: 202301100037)
