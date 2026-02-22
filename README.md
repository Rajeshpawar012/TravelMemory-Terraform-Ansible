# MERN Stack Deployment using Terraform and Ansible (Secure Production Setup)

## Project Overview

This project demonstrates a secure and automated deployment of a MERN (MongoDB, Express, React, Node.js) application on AWS using:

- **Terraform** – Infrastructure as Code (IaC)
- **Ansible** – Configuration Management & Deployment
- **PM2** – Process Management
- **Nginx** – Frontend Hosting
- **Ansible Vault** – Secret Management

The setup follows production-level best practices including private database subnet, authentication, least privilege access, and encrypted secrets.

---

## Architecture Overview

<img width="1536" height="1024" alt="ChatGPT Image Feb 22, 2026, 04_37_04 PM" src="https://github.com/user-attachments/assets/c9e2d7ca-8e2c-487d-b18d-d171e4bdac83" />


### Infrastructure Layout
            Internet
                │
         ┌─────────────────┐
         │  Public Subnet  │
         │  Web EC2        │
         │  (Node + Nginx) │
         └─────────────────┘
                │
        (Private Communication)
                │
         ┌─────────────────┐
         │ Private Subnet  │
         │  DB EC2         │
         │  MongoDB        │
         └─────────────────┘
         
---

##  AWS Infrastructure (Provisioned via Terraform)

### Components Created

- VPC
- Public Subnet
- Private Subnet
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- 2 EC2 Instances:
  - Web Server (Public)
  - Database Server (Private)
- SSH Key Pair

### Terraform Commands

```bash
terraform init
terraform plan
terraform apply
```

Outputs:
Public IP of Web Server
Private IP of Database Server

⚙ Configuration Management (Ansible)
Web Server Automation

Install Node.js

Install PM2

Clone MERN repository

Install backend dependencies

Generate .env dynamically using template

Restart backend with updated environment variables

Database Server Automation

Install MongoDB

Configure MongoDB service

Enable authentication

Create:

Admin user

Application user (least privilege)

🔐 Security Implementation
Database Security

MongoDB is deployed in a private subnet

No public IP for DB server

MongoDB Authentication Enabled

Role-based access:

admin → root access (admin DB only)

traveluser → readWrite access (application DB only)

Secret Management

Sensitive credentials stored using Ansible Vault

No passwords committed to Git

.env and Terraform state files excluded via .gitignore

Network Security

SSH access restricted

MongoDB is not publicly accessible

Security Groups configured for minimal exposure

🔄 Deployment Workflow
1️⃣ Provision Infrastructure

cd terraform
terraform init
terraform apply

cd ansible

ansible-playbook -i inventory.ini db.yml --ask-vault-pass

ansible-playbook -i inventory.ini web.yml --ask-vault-pass

🌐 Application Access

Frontend: (http://3.8.6.116/addexperience)

Backend API: (http://3.8.6.116:5000/hello)

MERN-DevOps-Assignment/
│
├── terraform/
│   ├── vpc.tf
│   ├── ec2.tf
│   ├── subnet.tf
│   ├── route.tf
│   ├── outputs.tf
│   └── ...
│
├── ansible/
│   ├── inventory.ini
│   ├── web.yml
│   ├── db.yml
│   ├── templates/
│   └── vault.yml (encrypted, not committed)
│
├── backend/
├── frontend/
└── README.md


## Key DevOps Concepts Demonstrated

Infrastructure as Code (Terraform)

Configuration as Code (Ansible)

Idempotent Playbooks

Secret Encryption (Ansible Vault)

Private Networking Architecture

Bastion-based SSH Access

Production-level MongoDB Security

Process Management using PM2

## Resume Highlight

Designed and automated secure MERN stack deployment on AWS using Terraform and Ansible with private MongoDB, dynamic environment templating, and encrypted secret management via Ansible Vault.

## Notes

Vault password is not committed for security reasons.

MongoDB is deployed in a private subnet and cannot be accessed publicly.

Secrets are encrypted using AES256 via Ansible Vault.

Deployment is fully automated and reproducible.

✅ Project Status

1 Infrastructure Provisioned

2 Web Server Configured

3 MongoDB Secured

4 Secrets Encrypted

5 Application Successfully Deployed


