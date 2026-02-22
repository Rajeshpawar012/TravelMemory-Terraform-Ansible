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

<img width="955" height="464" alt="Screenshot 2026-02-22 000622" src="https://github.com/user-attachments/assets/373d9e8c-1622-4603-9495-163b3e451143" />

---

Install Node.js

<img width="943" height="523" alt="Screenshot 2026-02-22 000714" src="https://github.com/user-attachments/assets/7e62b0bd-850c-4354-aca8-604749a14eef" />

---

Install PM2

<img width="959" height="516" alt="Screenshot 2026-02-22 000913" src="https://github.com/user-attachments/assets/b02a7bd3-b928-4a40-8996-9718dc3ba471" />

---

Clone the MERN repository

<img width="954" height="478" alt="Screenshot 2026-02-22 001037" src="https://github.com/user-attachments/assets/73028e9e-2dc3-497d-a98a-7d32197f2585" />

---

Install backend dependencies

<img width="955" height="472" alt="Screenshot 2026-02-22 001322" src="https://github.com/user-attachments/assets/35474c41-ee23-410a-b7c7-2f809e004e8d" />

---

Generate .env dynamically using a template

<img width="956" height="494" alt="Screenshot 2026-02-22 001748" src="https://github.com/user-attachments/assets/d9f1b39b-384d-4374-8f24-93a48dbfd765" />

---

Restart backend with updated environment variables

Database Server Automation

Install MongoDB

Configure the MongoDB service

<img width="941" height="445" alt="Screenshot 2026-02-22 152032" src="https://github.com/user-attachments/assets/f6ccbff8-71f4-48cf-b3e1-de20d6cb700b" />

---

Enable authentication

<img width="950" height="325" alt="image" src="https://github.com/user-attachments/assets/7e5db72b-767c-4dd8-ac8f-d021f59381f2" />

---

Create:

Admin user

<img width="959" height="413" alt="image" src="https://github.com/user-attachments/assets/19e60253-b1f2-4c11-98d2-ecc577ec1c72" />

---

Application user (least privilege)

🔐 Security Implementation
Database Security

MongoDB is deployed in a private subnet

No public IP for DB server

MongoDB Authentication Enabled

Role-based access:

admin → root access (admin DB only)

traveluser → readWrite access (application DB only)

<img width="930" height="460" alt="image" src="https://github.com/user-attachments/assets/c74822af-e0a0-465e-881e-b208535abf32" />

<img width="949" height="512" alt="Screenshot 2026-02-22 155552" src="https://github.com/user-attachments/assets/df880407-d3e2-44c4-a2fc-074f08825b15" />

Secret Management

Sensitive credentials stored using Ansible Vault

<img width="957" height="476" alt="image" src="https://github.com/user-attachments/assets/08d3866a-f4ec-4bd9-8276-12b318c0a997" />

No passwords committed to Git

.env and Terraform state files excluded via .gitignore

<img width="956" height="478" alt="image" src="https://github.com/user-attachments/assets/266331ea-50bc-4973-93c0-08983b9d1975" />


Network Security

SSH access restricted

MongoDB is not publicly accessible

<img width="958" height="520" alt="image" src="https://github.com/user-attachments/assets/5038104d-15e7-405f-b7a5-1b6e2ec22b51" />

Security Groups configured for minimal exposure

- Deployment Workflow
- Provision Infrastructure
```
cd terraform
terraform init
terraform apply
```
cd ansible

ansible-playbook -i inventory.ini db.yml --ask-vault-pass

<img width="918" height="116" alt="image" src="https://github.com/user-attachments/assets/582309e3-06c7-4fc8-be88-c094f5e5e990" />

ansible-playbook -i inventory.ini web.yml --ask-vault-pass

<img width="941" height="446" alt="Screenshot 2026-02-22 160425" src="https://github.com/user-attachments/assets/6de3f7d2-40b0-48b9-8824-fa9c124d7af3" />

🌐 Application Access

Frontend: (http://3.8.6.116/addexperience)

<img width="940" height="502" alt="Screenshot 2026-02-22 135227" src="https://github.com/user-attachments/assets/ce623bba-d327-42f1-bac6-e0511f67b3d2" />

---

Backend API: (http://3.8.6.116:5000/hello)

<img width="461" height="156" alt="Screenshot 2026-02-22 152915" src="https://github.com/user-attachments/assets/889c05d7-36be-4a4b-b12f-5ac4a6a3f804" />


<img width="893" height="446" alt="Screenshot 2026-02-22 135244" src="https://github.com/user-attachments/assets/44bffcf0-b691-40b0-a55e-f9304bec3596" />


---
```
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
```

## Key DevOps Concepts Demonstrated

Infrastructure as Code (Terraform)

Configuration as Code (Ansible)

Idempotent Playbooks

Secret Encryption (Ansible Vault)

Private Networking Architecture

Bastion-based SSH Access

Production-level MongoDB Security

Process Management using PM2

## Notes

Vault password is not committed for security reasons.

MongoDB is deployed in a private subnet and cannot be accessed publicly.

Secrets are encrypted with AES-256 using Ansible Vault.

<img width="956" height="481" alt="Screenshot 2026-02-22 155428" src="https://github.com/user-attachments/assets/c73f2d8b-e76a-456e-8ae0-fc732844a241" />


Deployment is fully automated and reproducible.

Project Status

1 Infrastructure Provisioned

2 Web Server Configured

3 MongoDB Secured

4 Secrets Encrypted

5 Application Successfully Deployed

## Resume Highlight

Designed and automated secure MERN stack deployment on AWS using Terraform and Ansible with private MongoDB, dynamic environment templating, and encrypted secret management via Ansible Vault.

Author
```
Rajesh Pawar
DevOps Engineer

```

