# Task 1 – Static Website Hosting on EC2 (Ubuntu + Nginx)

## Objective
To deploy a static website on an Amazon EC2 Ubuntu instance using the Nginx web server.

## Services Used
- Amazon EC2
- Ubuntu 20.04 LTS
- Nginx Web Server
- SSH

## Steps Performed
1. Logged in to the AWS Management Console.
2. Launched an EC2 instance with Ubuntu 20.04 AMI.
3. Configured the security group to allow SSH (port 22) and HTTP (port 80).
4. Connected to the EC2 instance using SSH.
5. Installed Nginx web server on the instance.
6. Created a static HTML file with in-built CSS.
7. Deployed the website under `/var/www/html`.
8. Accessed the website using the public IPv4 address of the EC2 instance.

## Commands Used
```bash
sudo apt update
sudo apt install nginx -y
cd /var/www/html
sudo nano index.html
