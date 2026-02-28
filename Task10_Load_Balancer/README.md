# Task 10 – VPC 3-Tier Architecture

## Objective
To design and implement a 3-tier VPC architecture in AWS with public and private subnets, demonstrating secure network segmentation and controlled internet access.

---

## AWS Services Used
- Amazon VPC
- Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- Amazon EC2

---

## Architecture Overview
Internet  
→ Internet Gateway  
→ Public Subnet (Web/Bastion Tier)  
→ NAT Gateway  
→ Private Subnet (Application Tier)  
→ Private Subnet (Database Tier)

---

## Steps Performed

### Step 1: Create VPC
- Created a VPC named `Task10-VPC`
- CIDR block: `10.0.0.0/16`

---

### Step 2: Create Subnets
- Public Subnet: `10.0.1.0/24`
- Private App Subnet: `10.0.2.0/24`
- Private DB Subnet: `10.0.3.0/24`

---

### Step 3: Create and Attach Internet Gateway
- Created an Internet Gateway
- Attached it to `Task10-VPC`

---

### Step 4: Create NAT Gateway
- Allocated an Elastic IP
- Created NAT Gateway in the Public Subnet

---

### Step 5: Configure Route Tables
- Public Route Table:
  - Route `0.0.0.0/0` → Internet Gateway
  - Associated with Public Subnet
- Private Route Table:
  - Route `0.0.0.0/0` → NAT Gateway
  - Associated with both Private subnets

---

### Step 6: Launch EC2 Instances in Each Tier
- **Public EC2 Instance**
  - Launched in Public Subnet
  - Public IP enabled
  - Used for internet access and as a bastion host
- **Private Application EC2 Instance**
  - Launched in Private App Subnet
  - No public IP
  - Internet access only via NAT Gateway
- **Private Database EC2 Instance**
  - Launched in Private DB Subnet
  - No public IP
  - Accessible only from Application tier

This step validates tier isolation and correct routing.

---

## Outcome
- Successfully created a 3-tier VPC architecture.
- Public tier has direct internet access.
- Private tiers are isolated and use NAT Gateway for outbound access.
- Network design follows AWS best practices.

---

## Screenshots
The following screenshots are included:
- VPC with CIDR configuration
- Public and Private subnets
- Route tables showing IGW and NAT routes
- EC2 instances placed in correct subnets
