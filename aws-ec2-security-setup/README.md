# 🔐 AWS EC2 Security Setup

---

## 📌 Objective

This project demonstrates how to securely configure and access an AWS EC2 instance using:

- Key Pair Authentication
- Security Groups (Firewall Rules)
- SSH Access Control
- Basic System Hardening

---

## 🛠️ Services Used

- AWS EC2
- Security Groups
- Key Pairs
- Linux (Amazon Linux)
- SSH

---

## 🔑 Step 1: Key Pair Creation

- Created a secure RSA key pair named `devops-key`
- Used `.pem` file for SSH authentication

📸 Screenshot:

![Key Pair](Images/keypair.png)

---

## 🚀 Step 2: EC2 Instance Launch

- Launched EC2 instance (`t2.micro`)
- Selected Amazon Linux AMI
- Attached key pair for secure login

📸 Screenshot:

![EC2 Instance](Images/ec2-instance.png)

---

## 🌐 Step 3: Security Group Configuration

Configured inbound rules:

| Type | Port | Source |
|------|------|--------|
| SSH  | 22   | My IP |
| HTTP | 80   | 0.0.0.0/0 |

🔒 Security Best Practice:
- Restricted SSH access to specific IP
- Avoided open SSH access (0.0.0.0/0)

📸 Screenshot:

![Security Group](Images/security-group.png)

---

## 🔗 Step 4: SSH Access

Connected to EC2 instance using:

```bash
ssh -i devops-key.pem ec2-user@<PUBLIC-IP>
