# Task 4 – Auto Scaling Group (ASG) with Application Load Balancer (ALB)

## Objective
To create a highly available and scalable web application using an Auto Scaling Group and an Application Load Balancer in AWS.

---

## AWS Services Used
- EC2
- Launch Template
- Auto Scaling Group
- Application Load Balancer
- Target Group
- Security Groups
- Ubuntu 20.04
- Nginx

---

## Step-by-Step Implementation

---

## STEP 1: Create Security Groups

### 1.1 Create Security Group for Load Balancer
1. Go to AWS Console → EC2 → Security Groups
2. Click **Create security group**
3. Name: `Task4-ALB-SG`
4. VPC: Default VPC
5. Add Inbound Rule:
   - Type: HTTP
   - Port: 80
   - Source: 0.0.0.0/0
6. Keep outbound rules as default (Allow all)
7. Click **Create security group**

---

### 1.2 Create Security Group for EC2 (ASG Instances)
1. Click **Create security group**
2. Name: `Task4-EC2-ASG-SG`
3. VPC: Default VPC
4. Add Inbound Rules:
   - HTTP | Port 80 | Source: `Task4-ALB-SG`
   - SSH  | Port 22 | Source: My IP
5. Keep outbound rules as default
6. Click **Create security group**

---

## STEP 2: Create Launch Template

1. Go to EC2 → Launch Templates
2. Click **Create launch template**
3. Launch template name: `Task4-LT`
4. AMI: Ubuntu 20.04 LTS
5. Instance type: t2.micro
6. Key pair: Select existing key pair
7. Network settings:
   - Security group: `Task4-EC2-ASG-SG`

### User Data (IMPORTANT)
Paste the following script in **Advanced details → User data**:

```bash
#!/bin/bash
apt update -y
apt install nginx -y
systemctl start nginx
systemctl enable nginx
echo "<h1>Auto Scaling Instance $(hostname)</h1>" > /var/www/html/index.html

Click Create launch template

STEP 3: Create Target Group

Go to EC2 → Target Groups

Click Create target group

Target type: Instances

Target group name: Task4-TG

Protocol: HTTP

Port: 80

VPC: Default VPC

Health Check Settings:

Protocol: HTTP

Path: /

Click Create target group

STEP 4: Create Application Load Balancer

Go to EC2 → Load Balancers

Click Create load balancer

Select Application Load Balancer

Name: Task4-ALB

Scheme: Internet-facing

IP address type: IPv4

Network mapping:

VPC: Default

Select at least 2 Availability Zones

Security group: Task4-ALB-SG

Listener:

HTTP : 80

Forward to: Task4-TG

Click Create load balancer

STEP 5: Create Auto Scaling Group

Go to EC2 → Auto Scaling Groups

Click Create Auto Scaling group

Name: Task4-ASG

Select launch template: Task4-LT

Click Next

Network:

VPC: Default

Subnets: Select at least 2 subnets

Load balancing:

Attach to an existing load balancer

Select target group: Task4-TG

Group size:

Desired capacity: 2

Minimum capacity: 1

Maximum capacity: 3

Scaling policy:

Target tracking scaling policy

Metric: Average CPU Utilization

Target value: 50%

Click Create Auto Scaling group

STEP 6: Verification
6.1 Verify EC2 Instances

Go to EC2 → Instances

Confirm 2 EC2 instances are running under Auto Scaling Group

6.2 Verify Target Group Health

Go to EC2 → Target Groups → Targets

Status should be Healthy

6.3 Verify Website Access

Go to EC2 → Load Balancers

Copy the ALB DNS name

Web page should load successfully


