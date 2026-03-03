TASK 2 — Azure Global Infrastructure + High Availability
📌 Objective

Deploy a highly available VM infrastructure in Azure using:

Availability Sets

Availability Zones

Azure Load Balancer

Azure Monitor

Diagnostic Logs

Validate high availability by simulating VM failure.

🏗️ Architecture Overview
                Internet
                   │
            Public Load Balancer
                   │
      ┌────────────┼────────────┐
      │                             │
Availability Set VMs       Availability Zone VMs
 (VM1, VM2)                (VM3 - Zone1, VM4 - Zone2)
                   │
             Virtual Network
☁️ Implementation Steps
1️⃣ Create Resource Group

Name: rg-ha-task2

Region: Supported region (e.g., Central India)

2️⃣ Create Virtual Network

Name: vnet-ha

Address space: 10.0.0.0/16

Subnet: 10.0.1.0/24

3️⃣ Deploy 2 VMs in Availability Set

Create Availability Set: availset-ha

Deploy VM1 and VM2 inside it

Same VNet and Subnet

✔ Protects against hardware failure.

4️⃣ Deploy 2 VMs in Availability Zones

VM3 → Zone 1

VM4 → Zone 2

✔ Protects against datacenter failure.

5️⃣ Create Public Load Balancer

SKU: Standard

Create new Public IP

Add all 4 VMs to Backend Pool

6️⃣ Configure Health Probe & Rule

Protocol: TCP

Port: 80

Create Load Balancing Rule (Port 80)

✔ Automatically routes traffic to healthy VMs.

7️⃣ Enable Azure Monitor

Create Alert Rule

Condition: CPU > 70%

Add email notification

8️⃣ Enable Diagnostics

Create Storage Account

Enable Boot diagnostics for VMs

Send logs to Storage Account

9️⃣ Test High Availability
Install Web Server (on all VMs)
sudo apt update
sudo apt install apache2 -y
echo "Hello from $(hostname)" | sudo tee /var/www/html/index.html

Open:

http://<LoadBalancer-Public-IP>

Refresh page — different VM names should appear.

Simulate Failure

Stop one VM

Refresh browser

✔ Website continues working
✔ Load Balancer routes to healthy VMs

✅ Features Implemented

Multi-VM Deployment

Availability Set

Multi-Zone Deployment

Load Balancing

Health Probes

Monitoring & Alerts

Diagnostic Logging

Failure Simulation

🧹 Cleanup

Delete Resource Group:

rg-ha-task2

This removes all resources.

🎯 Outcome

Successfully deployed a highly available Azure infrastructure with:

✔ Redundancy
✔ Fault tolerance
✔ Monitoring
✔ Load balancing
✔ Zero single point of failure
