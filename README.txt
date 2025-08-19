# AWS 3-Tier Web Architecture (Hands-On Portfolio Project)

This is a real-world AWS architecture project I built from scratch to practice designing secure, production-grade cloud infrastructure.

It follows the standard 3-tier model using public/private subnets, ALB, EC2 instances with auto scaling, RDS, S3, IAM roles, and monitoring tools.

I built this project as part of my personal cloud portfolio to show I can work with core AWS services, automate deployments, and apply security best practices.

---

## 📌 Project Goals

- Build a real VPC network with public/private subnets
- Launch EC2 instances inside private subnets
- Set up Application Load Balancer + Auto Scaling Group
- Connect EC2 to RDS database (in private subnet)
- Use S3 for static content + read-only access from EC2
- Apply IAM roles, least-privilege access, and security groups
- Monitor using CloudWatch + email alerts with SNS

---

## 🧱 Architecture Overview

**Network Structure:**
- VPC with 2 public subnets + 2 private subnets
- Internet Gateway for public subnets
- NAT Gateway for private subnet outbound access
- Route Tables configured properly (IGW + NAT)

**Compute Layer:**
- Bastion EC2 in public subnet for SSH (locked to my IP)
- App Server EC2 in private subnet (auto-scaled)
- ALB in public subnet routes traffic to private EC2s
- EC2 has IAM Role to access S3 + CloudWatch + SNS

**Database Layer:**
- RDS (MySQL) in private subnet
- No public access, only reachable from EC2 app

**Storage & Monitoring:**
- S3 bucket for static file hosting (public read)
- CloudWatch alarms for EC2 + SNS email notifications

---

## ⚙️ Auto Scaling + Launch Template

To automate instance creation, I used a **Launch Template** with:
- AMI + instance type
- Security group + IAM role
- User data script for startup

Then I created an **Auto Scaling Group** with:
- Min capacity: 1
- Max capacity: 3
- Target Group connected to ALB
- ALB handles health checks and routing

This setup allows EC2s to scale automatically and replace unhealthy instances.

---

## 🔐 Security Best Practices

- EC2 App Server and RDS in private subnets (not exposed to internet)
- SSH access only through Bastion Host (locked to my IP)
- ALB allows HTTP/HTTPS from anywhere, but only forwards to healthy EC2s
- RDS only accessible from App Server SG
- IAM roles for EC2 to access:
  - S3 (read-only)
  - CloudWatch Logs
  - SNS (for email alerts)

---

## ✅ AWS Services Used

- VPC, Subnets, Route Tables, IGW, NAT Gateway
- EC2 (App, Bastion, DB Client)
- Launch Templates + Auto Scaling Groups
- Application Load Balancer + Target Groups
- RDS (MySQL)
- S3 (static hosting + EC2 read-only)
- IAM Roles and Security Groups
- CloudWatch + SNS

---

## 🧠 What I Learned

- How to design a full VPC layout with real security in mind
- The difference between public/private subnets in practice
- Using launch templates and auto scaling to make infrastructure dynamic
- Connecting EC2 → RDS with proper SGs
- Granting EC2 limited access to S3, CloudWatch, and SNS using IAM
- How to test high-availability setup using health checks and ALB

---

## 📸 Screenshots


- VPC/Subnet layout
- EC2 instances
- ALB with healthy targets
- Auto Scaling Group setup
- Launch Template config
- RDS in private subnet (no public access)
- S3 bucket config
- CloudWatch alarm + SNS email
- IAM role policies

---

## 🛠️ How to Reproduce (Manual Steps)

1. Create VPC with 4 subnets (2 public, 2 private) across 2 AZs
2. Set up IGW for public, NAT Gateway for private
3. Launch EC2 Bastion in public subnet
4. Create Launch Template for EC2 App
5. Set up Auto Scaling Group connected to ALB target group
6. Deploy ALB with HTTP listener
7. Launch RDS (MySQL) in private subnet
8. Create S3 bucket with public read + EC2 IAM access
9. Attach IAM roles for EC2 → S3, CloudWatch, SNS
10. Set CloudWatch alarm for CPU + SNS email alerts

---

## 🧪 Testing

- Verified SSH only works through Bastion
- App Server receives HTTP traffic via ALB
- EC2 instance can connect to RDS (tested with internal EC2 DB client)
- EC2 can read files from S3 bucket
- CloudWatch triggers email on CPU threshold

---

## 📬 Contact

If you’d like to chat about cloud, collaborate, or have feedback on this project, feel free to reach out.

---

