# Task 2 – Disk Partitioning (MBR & GPT)

## Objective
To understand and perform disk partitioning using:
- **MBR (Master Boot Record)** on Linux (Ubuntu)
- **GPT (GUID Partition Table)** on Windows

This task demonstrates practical disk management skills across different operating systems.

---

## Tools & Services Used
- AWS EC2 (Ubuntu 20.04)
- Amazon EBS Volume
- Linux utilities: `lsblk`, `fdisk`, `mkfs`, `mount`
- AWS EC2 (Windows Server)
- Windows Disk Management (GUI)
- Microsoft Remote Desktop (from macOS)

---

## Part A: Disk Partitioning in Ubuntu (MBR)

### Description
In this part, a new EBS volume was attached to an Ubuntu EC2 instance and partitioned using the **MBR** partitioning scheme.

### Steps Performed
1. Launched an Ubuntu EC2 instance from the AWS Management Console.
2. Created a new EBS volume and attached it to the EC2 instance.
3. Connected to the EC2 instance using SSH.
4. Verified the attached disk using `lsblk`.

   > The attached EBS volume was exposed as an NVMe device (`/dev/nvme1n1`), which is standard behavior for modern EC2 instance types.

5. Created a primary partition using `fdisk` (MBR).
6. Formatted the partition with the `ext4` file system.
7. Mounted the partition to a directory and verified successful mounting.

### Commands Used
```bash
lsblk
sudo fdisk /dev/nvme1n1
sudo mkfs.ext4 /dev/nvme1n1p1
sudo mkdir /mnt/mbr_disk
sudo mount /dev/nvme1n1p1 /mnt/mbr_disk
df -h

Part B: Disk Partitioning in Windows (GPT)
Description

In this part, disk partitioning was performed in Windows using the GPT (GUID Partition Table) scheme through the graphical user interface.

Steps Performed
1. Launched a Windows Server EC2 instance from the AWS Management Console.

2. Connected to the Windows instance using Microsoft Remote Desktop (RDP).

3.Opened Disk Management.

4.Initialized the new disk using GPT (GUID Partition Table).

5.Created a new simple volume.

6.Assigned a drive letter and formatted the volume using NTFS.
