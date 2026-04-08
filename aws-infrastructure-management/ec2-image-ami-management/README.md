# 📦 EC2 Image (AMI) Management

---

## 📌 Objective

This project demonstrates how to:

* Create an AMI (Amazon Machine Image) from an EC2 instance
* Launch a new EC2 instance using the AMI
* Verify data and configuration cloning

This represents **real-world use cases** like backup, scaling, and environment replication.

---

## 🛠️ Services Used

* AWS EC2
* AMI (Amazon Machine Image)
* Security Groups
* SSH

---

## 🔹 STEP 1 — Prepare EC2 Instance

Use an existing EC2 instance (Amazon Linux recommended).

Create a test file to verify cloning:

```bash
echo "AMI Test Successful" > /home/ec2-user/test.txt
```

EC2 instance running + Public IP
![EC2 Instance](Images/ec2-instance.png)

able to ssh and creating file
![running-ec2](Images/running-ec2.png)

---

## 🔹 STEP 2 — Create AMI

1. Go to **EC2 → Instances**
2. Select your instance
3. Click **Actions → Image and templates → Create Image**
4. Provide details:

   * Name: `devops-ami`
   * Description: Test AMI
5. Click **Create Image**

📸 Screenshot: AMI creation
![Create AMI](Images/create-ami.png)

---

## 🔹 STEP 3 — Verify AMI

1. Go to **EC2 → AMIs**
2. Check status → **Available**

📸 Screenshot: AMI available
![AMI Available](Images/ami-available.png)

---

## 🔹 STEP 4 — Launch EC2 from AMI

1. Select AMI
2. Click **Launch Instance**
3. Configure:

   * Instance type: `t2.micro`
   * Key pair: existing key
   * Security Group: SSH (My IP)
4. Launch instance

📸 Screenshot: New EC2 instance from AMI
![New EC2](Images/new-ec2-from-ami.png)

---

## 🔹 STEP 5 — Verify Cloned Data

Connect to the new instance:

```bash
ssh -i devops-key.pem ec2-user@<NEW-PUBLIC-IP>
```

Verify the test file:

```bash
cat /home/ec2-user/test.txt
```

Expected output:

```bash
AMI Test Successful
```

📸 Screenshot: Data verification
![Data Verified](Images/ami-data-verified.png)

---

## 📁 Project Structure

```
ec2-image-ami-management/
│
├── Images/
│   ├── ec2-instance.png
│   ├── create-ami.png
│   ├── ami-available.png
│   ├── new-ec2-from-ami.png
│   └── ami-data-verified.png
│
└── README.md
```

---

## 🎯 Outcome

* Created reusable machine image (AMI)
* Launched new EC2 instance from AMI
* Verified that data and configuration are cloned

---

## 💡 Key Concepts

* AMI acts as a **template** for launching EC2 instances
* Used for **backup, scaling, and disaster recovery**
* Ensures **consistent environments across deployments**
