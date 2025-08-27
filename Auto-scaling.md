# AWS Auto Scaling with Application Load Balancer Using a Launch Template

## Overview

This documentation covers the steps I followed to configure AWS Auto Scaling with an Application Load Balancer (ALB) using a Launch Template. The goal was to gain hands-on experience with scalable and resilient architectures in AWS, focusing on resource optimization and performance under varying workloads.

---

## 1. **Launch Template Creation**

### a. **Purpose**
A Launch Template defines the configuration (AMI, instance type, security groups, etc.) for EC2 instances that the Auto Scaling group will launch.

### b. **Steps**
1. **Navigate to EC2 Console:**  
   AWS Console → EC2 → "Launch Templates" → "Create launch template"
2. **Details Provided:**
   - **Name:** `web-app-launch-template`
   - **AMI ID:** Amazon Linux 2 (latest)
   - **Instance Type:** `t3.micro` (for testing; adjust as needed)
   - **Key Pair:** My SSH key (for admin access)
   - **Security Group:** Allows HTTP (80), HTTPS (443), and SSH (22) from my IP
   - **User Data:** Installed a simple web server:
     ```bash
     #!/bin/bash
     yum update -y
     yum install -y httpd
     systemctl start httpd
     systemctl enable httpd
     echo "Hello from $(hostname)" > /var/www/html/index.html
     ```
   - **IAM Role:** `AmazonEC2RoleforSSM` attached (for management)
   - **Storage:** 8 GB gp2 (default)

---

## 2. **Application Load Balancer (ALB) Setup**

### a. **Steps**
1. **Navigate to EC2 Console → Load Balancers → Create Load Balancer → Application Load Balancer**
2. **Details Provided:**
   - **Name:** `web-app-alb`
   - **Scheme:** Internet-facing
   - **Listeners:** HTTP (port 80)
   - **Availability Zones:** At least two selected
   - **Target Group:** Created new target group (`web-app-tg`) of type "instance", protocol HTTP, port 80
   - **Health Check:** Path
