# Task 9 – Access S3 from EC2 using IAM Role

## Objective
To allow an EC2 instance to access Amazon S3 securely using an IAM Role, without using access keys.

---

## Services Used
- Amazon EC2
- AWS IAM (Role & Policy)
- Amazon S3
- AWS CLI v2

---

## Steps Performed
1. Created an S3 bucket for testing access.
2. Created an IAM role for EC2 and attached the `AmazonS3FullAccess` policy.
3. Attached the IAM role to an EC2 instance.
4. Connected to the EC2 instance.
5. Installed **AWS CLI v2 manually** on the EC2 instance.
6. Verified that the EC2 instance assumed the IAM role.
7. Verified access to Amazon S3 from the EC2 instance using AWS CLI commands.
8. Confirmed that no access keys were configured.

---

## Commands Used
```bash
# Install AWS CLI v2
sudo apt update
sudo apt install unzip curl -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

# Verify IAM role and S3 access
aws --version
aws sts get-caller-identity
aws s3 ls
