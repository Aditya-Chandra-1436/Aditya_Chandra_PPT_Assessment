# Hybrid Architecture Simulation – AWS

## 📌 Objective

To simulate a secure hybrid cloud architecture where:

* A **Bastion Host** (Jump Server) is deployed in a public subnet.
* A **Private EC2 instance** is deployed in a private subnet.
* Direct internet access to the private instance is blocked.
* Access to the private instance is allowed only through the Bastion Host.

---

## 🏗 Architecture Overview

User (On-Prem / Local Machine)
→ SSH to Bastion Host (Public Subnet)
→ SSH to Private VM (Private Subnet)

The private instance has:

* No Public IP
* No Internet Gateway route
* SSH access restricted to Bastion Security Group only

---

## 🛠 Services Used

* Amazon VPC
* Subnets (Public & Private)
* Internet Gateway
* Route Tables
* EC2 Instances
* Security Groups
* SSH

---

## 📂 Network Configuration

### VPC

* Name: hybrid-vpc
* CIDR: 10.0.0.0/16

### Public Subnet

* Name: public-subnet
* CIDR: 10.0.1.0/24
* Auto-assign Public IP: Enabled
* Route: 0.0.0.0/0 → Internet Gateway

### Private Subnet

* Name: private-subnet
* CIDR: 10.0.2.0/24
* Auto-assign Public IP: Disabled
* No internet route

---

## 🔐 Security Configuration

### Bastion Security Group (Bastion-SG)

Inbound:

* SSH (Port 22)
* Source: My IP

Outbound:

* Allow all

### Private Security Group (Private-SG)

Inbound:

* SSH (Port 22)
* Source: Bastion-SG (Security Group reference)

Outbound:

* Allow all

---

## 🚀 Deployment Steps Summary

1. Created VPC with CIDR 10.0.0.0/16.
2. Created public and private subnets.
3. Created and attached Internet Gateway.
4. Configured public route table with 0.0.0.0/0 → IGW.
5. Associated private subnet with isolated route table (no internet route).
6. Launched Bastion Host in public subnet with Public IP.
7. Launched Private VM in private subnet without Public IP.
8. Configured Security Groups to allow SSH only via Bastion.
9. Verified private instance cannot be accessed directly.
10. Successfully accessed Private VM through Bastion.

---

## 🔎 Testing & Validation

### Test 1 – Direct SSH to Private VM

Attempted:
ssh -i key.pem [ec2-user@10.0.2.x](mailto:ec2-user@10.0.2.x)

Result:
Connection failed (Expected behavior)

Reason:
Private instance has no public IP and no internet route.

---

### Test 2 – SSH to Bastion

ssh -i key.pem ec2-user@<Bastion-Public-IP>

Result:
Login successful.

---

### Test 3 – SSH from Bastion to Private VM

ssh -i key.pem [ec2-user@10.0.2.x](mailto:ec2-user@10.0.2.x)

Result:
Login successful.

---

### Test 4 – Internet Access from Private VM

ping google.com

Result:
Request failed (Expected behavior)

Reason:
Private subnet has no route to Internet Gateway.

---

## 🔁 Traffic Flow Explanation

1. User initiates SSH connection to Bastion Public IP.
2. Bastion receives traffic via Internet Gateway.
3. Bastion connects to Private VM using private IP.
4. Private Security Group allows SSH only from Bastion-SG.
5. Private VM remains inaccessible from the public internet.

---

## 🔐 Security Outcome

✔ Private instance has no Public IP
✔ Private subnet has no internet route
✔ SSH restricted to Bastion only
✔ Direct access blocked
✔ Architecture follows least privilege principle

---

## 📊 Real-World Use Case

This architecture is commonly used in:

* Production environments
* Banking infrastructure
* Enterprise networks
* Hybrid on-prem to cloud deployments

Bastion Host acts as a secure entry point to internal resources.

----

## ✅ Conclusion

The hybrid architecture was successfully implemented and validated.

The Private VM is securely isolated and accessible only through the Bastion Host, ensuring controlled and secure remote administration.

