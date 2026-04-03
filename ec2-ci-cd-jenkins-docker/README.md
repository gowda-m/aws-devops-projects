# 🚀 AWS Jenkins Docker Container Auto Deployment Pipeline

---

## 📌 Overview

This project demonstrates a complete CI/CD pipeline using AWS, Jenkins, and Docker to automatically deploy a static website inside a Docker container on a separate EC2 instance.

---

## 🛠️ Technologies Used

* AWS (IAM, EC2, Security Groups)
* Jenkins
* Docker
* GitHub

---

# 🔹 STEP 1: Create IAM User

* IAM → Users → Create User
* Name: `jenkins-user`
* Attach policy: `AdministratorAccess`

---
![IAM_user](Images/IAM_user.png.png)

---

# 🔹 STEP 2: Create Key Pair

* EC2 → Key Pairs → Create
* Name: `jenkins-key`

📸 Screenshot
![Key](screenshots/02_keypair.png)

---

# 🔹 STEP 3: Create Security Group

| Type       | Port |
| ---------- | ---- |
| SSH        | 22   |
| HTTP       | 80   |
| Custom TCP | 8080 |

📸 Screenshot
![SG](screenshots/03_sg.png)

---

# 🔹 STEP 4: Launch EC2 Instances

Created **2 EC2 instances**:

1️⃣ Jenkins Server
2️⃣ Docker Server

* AMI: Amazon Linux
* Instance type: t2.micro
* Same key pair and security group

📸 Screenshot
![EC2](screenshots/04_ec2.png)

---

# 🔹 STEP 5: Connect to Servers

```bash
ssh -i jenkins-key.pem ec2-user@<jenkins-public-ip>
ssh -i jenkins-key.pem ec2-user@<docker-public-ip>
```

📸 Screenshot
![SSH](screenshots/05_ssh.png)

---

# 🔹 STEP 6: Install Jenkins (Jenkins Server)

```bash
sudo yum install java-11-openjdk -y

sudo wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

sudo yum install jenkins -y

sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Access Jenkins:

```
http://<jenkins-public-ip>:8080
```

📸 Screenshot
![Jenkins](screenshots/06_jenkins.png)

---

# 🔹 STEP 7: Unlock Jenkins

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

* Enter password in browser
* Install suggested plugins

📸 Screenshot
![Dashboard](screenshots/07_dashboard.png)

---

# 🔹 STEP 8: Setup SSH (Jenkins → Docker Server)

Generate SSH key on Jenkins server:

```bash
ssh-keygen
```

Copy key to Docker server:

```bash
ssh-copy-id ec2-user@<docker-public-ip>
```

Test connection:

```bash
ssh ec2-user@<docker-public-ip>
```

📸 Screenshot
![SSH Setup](screenshots/08_ssh_setup.png)

---

# 🔹 STEP 9: Install Docker (Docker Server)

```bash
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker
```

Verify:

```bash
docker --version
```

📸 Screenshot
![Docker Install](screenshots/09_docker_install.png)

---

# 🔹 STEP 10: Create GitHub Repository

Files:

* `index.html`
* `Dockerfile`
* `Jenkinsfile`

📸 Screenshot
![GitHub](screenshots/10_github.png)

---

# 🔹 STEP 11: Create Jenkins Pipeline

* Jenkins → New Item → Pipeline
* Add GitHub repository URL
* Configure to use Jenkinsfile

📸 Screenshot
![Pipeline](screenshots/11_pipeline.png)

---

# 🔹 STEP 12: Trigger Build

* Click **Build Now**

📸 Screenshot
![Build](screenshots/12_build.png)

---

# 🔹 STEP 13: Docker Build & Run (via Jenkins)

* Jenkins builds Docker image
* Runs container on Docker server

Verify:

```bash
docker ps
```

📸 Screenshot
![Docker PS](screenshots/13_docker_ps.png)

---

# 🔹 STEP 14: Verify Website

Open in browser:

```
http://<docker-public-ip>
```

📸 Screenshot
![Website](screenshots/14_website.png)

---

# 🔹 STEP 15: Auto Build Trigger (GitHub Webhook)

Configure webhook in GitHub:

```
http://<jenkins-public-ip>:8080/github-webhook/
```

📸 Screenshot
![Webhook](screenshots/15_webhook.png)

---

# 🔹 STEP 16: Auto Deployment Test

* Modify `index.html`
* Push changes to GitHub
* Jenkins automatically triggers build
* Docker container gets updated

📸 Screenshot
![Auto Build](screenshots/16_auto_build.png)

---

## 🔁 CI/CD Workflow

```text
GitHub → Jenkins Server → Docker Server → Container → Browser
```

---

## 🚀 Final Result

* Jenkins runs on separate EC2 instance
* Docker runs on separate EC2 instance
* Fully automated CI/CD pipeline
* Auto deployment on code changes
* Website served via Docker container

---

## ⚠️ Notes

* Setup is for learning and testing purposes
* Security group allows required ports (22, 80, 8080)
* Can be extended with load balancer, domain, and SSL

---
