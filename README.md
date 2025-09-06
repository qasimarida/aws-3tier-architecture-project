 AWS 3-Tier Web Architecture (Hands-On Portfolio Project)

This is a **real-world AWS architecture project** I built from scratch to practice designing **secure, scalable, production-grade cloud infrastructure**.

It follows the **3-tier model** with networking, compute, and database layers, using **VPC, subnets, EC2, ALB, Auto Scaling, RDS, S3, IAM, and CloudWatch**.

I built this project as part of my personal **cloud portfolio** to demonstrate skills in AWS core services, automation, and security best practices.

---

## 📌 Goals

* Build a VPC network with **public + private subnets**
* Launch **EC2 instances** in private subnets
* Set up **Application Load Balancer (ALB) + Auto Scaling Group (ASG)**
* Deploy **RDS database** in private subnet
* Provide EC2 read-only access to **S3** bucket
* Apply **IAM roles, least-privilege, and security groups**
* Configure **CloudWatch monitoring + SNS email alerts**

---

## 🧱 Architecture Overview

### **Network**

* Custom **VPC** with 2 public + 2 private subnets (across 2 AZs)
* **Internet Gateway** → public internet access
* **NAT Gateway** → private subnet outbound access
* **Route Tables** configured for IGW + NAT

### **Compute**

* **Bastion Host (EC2)** in public subnet → SSH access (restricted to my IP)
* **App Servers (EC2)** in private subnets → managed by Auto Scaling Group
* **Application Load Balancer (ALB)** in public subnet routes traffic to EC2s
* EC2 **IAM Role** grants access to S3, CloudWatch, SNS

### **Database**

* **Amazon RDS (MySQL)** in private subnet
* No public exposure → only accessible from EC2 App SG

### **Storage & Monitoring**

* **S3 bucket** for static hosting (public read for files)
* **CloudWatch alarms** for EC2 metrics
* **SNS** for email alerts (CPU threshold, failures)

---

## ⚙️ Auto Scaling Setup

* **Launch Template** with AMI, instance type, SG, IAM role, and user-data
* **Auto Scaling Group**:

  * Min: 1, Max: 3 instances
  * Target Group linked to ALB
  * Health checks ensure auto-replacement of failed EC2s

---

## 🔐 Security Best Practices

* App Servers + RDS inside **private subnets**
* SSH only via **Bastion Host** (restricted by IP)
* ALB accepts public HTTP/HTTPS → forwards only to healthy EC2s
* RDS only accessible from **App Server Security Group**
* EC2 IAM roles grant **least-privilege access**:

  * Read-only → S3
  * Write → CloudWatch Logs
  * Publish → SNS

---

## ✅ AWS Services Used

* **Networking:** VPC, Subnets, Route Tables, IGW, NAT
* **Compute:** EC2 (App + Bastion), Launch Templates, ASG, ALB
* **Database:** RDS (MySQL)
* **Storage:** S3 (static hosting + EC2 access)
* **Security:** IAM Roles, Security Groups
* **Monitoring:** CloudWatch + SNS

---

## 🧠 Key Learnings

* Designing a secure **multi-tier VPC** with public/private subnets
* Using **Auto Scaling + ALB** for high availability
* Enforcing **least privilege IAM policies** for EC2
* Securely connecting **EC2 → RDS**
* Setting up **monitoring + alerts** with CloudWatch + SNS

---

## 📸 Screenshots (Examples)

* VPC + Subnets
* ALB + Target Group (healthy instances)
* Auto Scaling Group configuration
* RDS private instance (no public access)
* S3 bucket setup
* CloudWatch alarms + SNS email

---

## 🛠️ Reproduction Steps

1. Create VPC with 2 public + 2 private subnets across AZs
2. Add Internet Gateway + NAT Gateway
3. Launch Bastion Host (EC2) in public subnet
4. Create Launch Template for App EC2
5. Configure Auto Scaling Group + attach ALB Target Group
6. Deploy ALB with HTTP listener
7. Launch RDS (MySQL) in private subnet
8. Create S3 bucket + grant EC2 IAM read-only access
9. Attach IAM roles for EC2 → S3, CloudWatch, SNS
10. Set CloudWatch alarm (CPU) + SNS notification

---

## 🧪 Testing

* Verified SSH only works via Bastion
* ALB forwards HTTP traffic → App Servers in private subnet
* App EC2 can connect to RDS via SG rules
* App EC2 can read from S3 bucket
* CloudWatch alarm triggered → SNS email received


Do you want me to draft that **now**, or do you first want to upload this README to GitHub and then continue?
