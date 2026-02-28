# Task 7 – Create Amazon EFS and Connect to Multiple Ubuntu EC2 Instances

## Objective
To create an Amazon Elastic File System (EFS) and mount it on multiple Ubuntu EC2 instances to demonstrate shared storage functionality in AWS.

This task validates understanding of scalable file systems and shared access across EC2 instances.

---

## AWS Services Used
- Amazon EC2
- Amazon EFS
- Security Groups
- Ubuntu 20.04
- NFS (Network File System)

---

## Architecture Overview
EC2 Instance 1  
↔ Amazon EFS (Shared File System)  
↔ EC2 Instance 2  

Both EC2 instances access the same file system simultaneously.

---

## Step-by-Step Implementation

---

## Step 1: Launch Two Ubuntu EC2 Instances
1. Logged in to the AWS Management Console.
2. Launched two Ubuntu EC2 instances:
   - Instance 1: `Task7-EC2-1`
   - Instance 2: `Task7-EC2-2`
3. Used instance type `t2.micro`.
4. Attached a security group allowing:
   - SSH (Port 22) from My IP.
5. Ensured both instances were launched in the same VPC.

---

## Step 2: Create Security Group for EFS
1. Opened EC2 → Security Groups.
2. Created a new security group named `Task7-EFS-SG`.
3. Added inbound rule:
   - Type: NFS
   - Port: 2049
   - Source: EC2 Security Group (used by both instances).
4. Kept outbound rules as default (Allow all).

---

## Step 3: Create Amazon EFS File System
1. Opened Amazon EFS service.
2. Clicked **Create file system**.
3. Provided name: `Task7-EFS`.
4. Selected the default VPC.
5. Created mount targets in all Availability Zones.
6. Attached the security group `Task7-EFS-SG`.
7. Created the file system successfully.

---

## Step 4: Verify Mount Targets
1. Opened the created EFS file system.
2. Checked the **Network** tab.
3. Verified that mount targets were in **Available** state.

---

## Step 5: Mount EFS on EC2 Instance 1
1. Connected to `Task7-EC2-1` using SSH.
2. Installed NFS utilities:
   ```bash
   sudo apt update
   sudo apt install nfs-common -y

Created mount directory:

sudo mkdir /mnt/efs

Mounted the EFS file system:

sudo mount -t nfs4 <EFS-DNS-NAME>:/ /mnt/efs

Created a test file:

echo "Hello from EC2-1" | sudo tee /mnt/efs/shared.txt
Step 6: Mount EFS on EC2 Instance 2
Connected to Task7-EC2-2 using SSH.

Installed NFS utilities:

sudo apt update
sudo apt install nfs-common -y

Created mount directory:

sudo mkdir /mnt/efs

Mounted the same EFS file system:

sudo mount -t nfs4 <EFS-DNS-NAME>:/ /mnt/efs
Step 7: Verify Shared Access

On EC2 Instance 2, read the file created by EC2 Instance 1:
cat /mnt/efs/shared.txt

Verified that the content was accessible, confirming shared storage.

Outcome

Successfully created an Amazon EFS file system.

Mounted the same EFS on multiple EC2 instances.

Verified shared file access across instances.

Demonstrated scalable and shared storage using Amazon EFS.
