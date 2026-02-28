# Task 3 – Attach EBS Volume from Different Availability Zone using Snapshot

## Objective
To demonstrate how data can be moved across different Availability Zones in AWS by creating an EBS snapshot and restoring it into another Availability Zone.

This task validates understanding of EBS snapshots, cross-AZ volume restoration, and data persistence.

---

## Services Used
- AWS EC2
- Amazon EBS Volume
- Amazon EBS Snapshot
- Ubuntu 20.04

---

## Architecture Overview
EC2 Instance (AZ-1)  
→ EBS Volume  
→ Snapshot  
→ New EBS Volume (AZ-2)  
→ EC2 Instance (AZ-2)

---

## Steps Performed

### Part A: Create EC2 and EBS Volume in AZ-1
1. Launched an Ubuntu EC2 instance in Availability Zone 1.
2. Created a new EBS volume in the same Availability Zone.
3. Attached the EBS volume to the EC2 instance.
4. Connected to the EC2 instance using SSH.
5. Partitioned, formatted, and mounted the EBS volume.
6. Created a test file on the mounted volume to verify data persistence.

---

### Part B: Create Snapshot
7. Created an EBS snapshot of the attached volume using the AWS Management Console.
8. Waited for the snapshot status to change to **Completed**.

---

### Part C: Restore Snapshot in AZ-2
9. Created a new EBS volume from the snapshot in a different Availability Zone.
10. Launched a new Ubuntu EC2 instance in the same Availability Zone as the restored volume.
11. Attached the restored EBS volume to the new EC2 instance.

---

### Part D: Verify Data on New EC2
12. Mounted the restored volume on the second EC2 instance.
13. Verified that the test file created earlier was present and readable.

---

## Commands Used

### On EC2 Instance in AZ-1
```bash
lsblk
sudo fdisk /dev/nvme1n1
sudo mkfs.ext4 /dev/nvme1n1p1
sudo mkdir /mnt/task3
sudo mount /dev/nvme1n1p1 /mnt/task3
echo "Task 3 Snapshot Test Data" | sudo tee /mnt/task3/testfile.txt
cat /mnt/task3/testfile.txt
