# MERN Stack Deployment using Terraform and Ansible (Secure Production Setup)

## Project Overview

This project demonstrates a secure and automated deployment of a MERN (MongoDB, Express, React, Node.js) application on AWS using:

- **Terraform** – Infrastructure as Code (IaC)
- **Ansible** – Configuration Management & Deployment
- **PM2** – Process Management
- **Nginx** – Frontend Hosting
- **Ansible Vault** – Secret Management

The setup follows production-level best practices, including a private database subnet, authentication, least-privilege access, and encrypted secrets.

---

## Architecture Overview

<img width="1536" height="1024" alt="ChatGPT Image Feb 22, 2026, 04_37_04 PM" src="https://github.com/user-attachments/assets/c9e2d7ca-8e2c-487d-b18d-d171e4bdac83" />

---

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

-VPC

<img width="958" height="439" alt="image" src="https://github.com/user-attachments/assets/f450deba-fe33-4c61-bcb1-bd937358f8e0" />

---

- Public Subnet

<img width="940" height="313" alt="image" src="https://github.com/user-attachments/assets/a057c61d-0416-4b7b-b7ab-119e4607d16b" />

---

- Private Subnet

<img width="959" height="334" alt="image" src="https://github.com/user-attachments/assets/722f04f3-86ce-4164-9755-57e43b38aabd" />

---

- Internet Gateway

<img width="958" height="273" alt="image" src="https://github.com/user-attachments/assets/c2244066-ab9d-4dc1-9948-b8eca1e8c0c1" />

---

- NAT Gateway

<img width="959" height="288" alt="Screenshot 2026-02-21 162057" src="https://github.com/user-attachments/assets/1c5ea5c7-bc89-4d94-a093-11896d9272c9" />

---

- Route Tables

<img width="959" height="317" alt="image" src="https://github.com/user-attachments/assets/be3f5726-537d-460e-8937-95e2e216e716" />


<img width="959" height="304" alt="image" src="https://github.com/user-attachments/assets/988dca76-7f3b-4de1-b8c0-9964b1170401" />

---

- Security Groups

<img width="959" height="239" alt="image" src="https://github.com/user-attachments/assets/aca771f0-8963-4e43-93bf-4f0eecf99881" />

---

- 2 EC2 Instances:
  - Web Server (Public)
  - Database Server (Private)
    
<img width="959" height="391" alt="image" src="https://github.com/user-attachments/assets/88601bdf-4e21-4e19-b8b0-5f6142152787" />

---  

- SSH Key Pair

<img width="914" height="387" alt="image" src="https://github.com/user-attachments/assets/78496d63-e3ec-4f35-b467-1c1c7ac5851a" />

---

### Terraform Commands

```bash
terraform init
terraform plan
terraform apply
```

Outputs:

- Public IP of Web Server

- Private IP of Database Server

<img width="956" height="119" alt="image" src="https://github.com/user-attachments/assets/9ffe83bb-c441-4e25-8720-dc989d487d8e" />

---

⚙ Configuration Management (Ansible)
Web Server Automation

Install Node.js

Install PM2

Clone the MERN repository

Install backend dependencies

Generate .env dynamically using a template

Restart backend with updated environment variables

Database Server Automation

Install MongoDB

Configure the MongoDB service

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


