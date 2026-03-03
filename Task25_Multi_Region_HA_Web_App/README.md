Fault-Tolerant Web Application on AWS
 Project Objective

Deploy a highly available and fault-tolerant web application across multiple Availability Zones using:

Amazon VPC

EC2 (Private Instances)

Application Load Balancer (ALB)

Auto Scaling Group (ASG)

NAT Gateway

S3

CloudWatch

This architecture ensures high availability, scalability, and security.

 Architecture Overview

The application is deployed inside a custom VPC (10.0.0.0/16) with:

2 Public Subnets

Application Load Balancer

NAT Gateway

2 Private Subnets

EC2 instances

Auto Scaling Group

Traffic Flow:

Internet → ALB → Target Group → EC2 (Private) → NAT (for outbound)

Monitoring:

CloudWatch → CPU Alarm → Auto Scaling

Static assets:

S3 Bucket → Stores CSS / Images
🛠️ Services Used
Service	Purpose
VPC	Isolated network environment
Subnets	Multi-AZ deployment
Internet Gateway	Public internet access
NAT Gateway	Private subnet internet access
EC2	Web servers
Security Groups	Controlled traffic flow
ALB	Load balancing
Target Group	Health checks & routing
Auto Scaling	Automatic scaling
S3	Static file storage
CloudWatch	Monitoring & scaling trigger
⚙️ Deployment Steps (High-Level)

Created Custom VPC (10.0.0.0/16)

Created 2 Public & 2 Private Subnets (Multi-AZ)

Attached Internet Gateway

Created NAT Gateway

Configured Route Tables

Launched EC2 in Private Subnets

Configured Security Groups

Created Application Load Balancer

Created Target Group & Registered Instances

Configured Auto Scaling Group (Min=2, Desired=2)

Created S3 Bucket

Configured CloudWatch Alarm (CPU > 70%)

Tested via ALB Public DNS

 Application Testing

Accessed via:

http://<ALB-DNS-NAME>

Expected Output:

Hello from ip-10-0-x-x.ec2.internal

Refreshing the page shows different hostnames, proving:

 Load balancing
 High availability
 Multi-AZ deployment

 Cost Estimation (Basic Approximation)
Service	Approx Monthly Cost
EC2 (2 × t2.micro)	~$16
ALB	~$18
NAT Gateway	~$32
S3	~$1
CloudWatch	~$1
Estimated Total	~$68/month

Costs may vary based on region and usage.

 Security Design

ALB Security Group:

HTTP 80 → 0.0.0.0/0

Web Security Group:

HTTP 80 → ALB-SG

SSH 22 → VPC CIDR

EC2 Instances:

No Public IP

Private Subnet only
