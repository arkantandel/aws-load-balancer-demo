# Load Balancer Setup Guide

This README explains how to create and configure a Load Balancer in AWS step-by-step. It is written for beginners and intermediate users.

---

## 🚀 Overview

A **Load Balancer** distributes incoming traffic across multiple EC2 instances to improve:

* Availability ✔️
* Fault Tolerance ✔️
* Performance ✔️

AWS provides several types, but we’ll create the **Application Load Balancer (ALB)**.

---

## 📌 Prerequisites

Before you begin, make sure you have:

* An AWS account
* At least **2 running EC2 instances** (same VPC)
* Proper **Security Groups** allowing:

  * HTTP (80)
  * Or HTTPS (443) if using SSL

---

## 🛠 Step 1: Create Target Group

Target Group is where load balancer sends traffic.

1. Open **EC2 Console** → *Load Balancing* → **Target Groups**
2. Click **Create Target Group**
3. Choose:

   * **Target type:** Instances
   * **Protocol:** HTTP
   * **Port:** 80
4. Select your **VPC**
5. Register your EC2 instances
6. Click **Create**

---

🛠 Step 2: Create Load Balancer (Application Load Balancer)

1. Go to **EC2 Console** → *Load Balancers* → **Create Load Balancer**
2. Select **Application Load Balancer**
3. Configure:

   * **Name:** my-load-balancer
   * **Scheme:** Internet-facing
   * **IP type:** IPv4
4. Network Mapping:**

   * Select at least 2 public subnets
5. Security Group:**

   * Allow HTTP (80)
6. Listeners:

   * Listener: HTTP 80 → Forward to Target Group
7. Click Create Load Balancer

---

## 🧪 Step 3: Test Load Balancer

Copy the **DNS name** of your load balancer.

Paste it in your browser:

```
http://<your-alb-dns-name>
```

You should see your EC2 instance page.

Refresh multiple times to verify traffic distribution.

---

## 📈 Optional: Health Checks

Go to Target Group → **Health Checks**.

* Protocol: HTTP
* Path: `/`

Healthy = instance is serving traffic.

---

## 🔐 Optional: HTTPS/SSL Setup

To enable HTTPS:

1. Request certificate in **AWS Certificate Manager (ACM)**
2. Add HTTPS Listener (443)
3. Attach ACM certificate

---

## 🧾 Useful CLI Commands

### Create Load Balancer:

```bash
aws elbv2 create-load-balancer \
  --name my-alb \
  --subnets subnet-123 subnet-456 \
  --security-groups sg-1234
```

### Create Target Group:

```bash
aws elbv2 create-target-group \
  --name my-targets \
  --protocol HTTP \
  --port 80 \
  --vpc-id vpc-123456
```

### Register Instances:

```bash
aws elbv2 register-targets \
  --target-group-arn <arn> \
  --targets Id=i-001 Id=i-002
```

---

## 🔗 Add Your Links

### 👤 LinkedIn

[linkedin.com/in/arkan-tandel-81709b360](https://linkedin.com/in/arkan-tandel-81709b360)

### 💻 GitHub

[github.com/arkantandel](https://github.com/arkantandel)

---

## 🎯 Final Notes

* ALB supports **Path-based** & **Host-based** routing
* Use Autoscaling for automatic scaling
* Always use Health Checks to maintain availability

