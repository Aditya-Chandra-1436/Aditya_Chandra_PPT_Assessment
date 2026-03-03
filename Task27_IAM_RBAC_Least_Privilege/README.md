📘 TASK 3 — IAM + RBAC + Least Privilege (AWS + Azure)
🎯 Objective

Implement Role-Based Access Control (RBAC) using the Least Privilege Principle in:

AWS (IAM)

Azure (Microsoft Entra ID)

🟠 PART 1 — AWS IAM Implementation
✅ Step 1: Create IAM User

Service: IAM

User Name: Developer

Access Type: Console Access

✅ Step 2: Attach EC2 Full Access

Attached AWS Managed Policy:

AmazonEC2FullAccess

✔ User can manage EC2 instances.

✅ Step 3: Create Custom S3 Policy

Created a custom policy:

Policy Name:
AllowCreateDenyDeleteS3
Policy JSON:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCreateAndList",
      "Effect": "Allow",
      "Action": [
        "s3:CreateBucket",
        "s3:ListAllMyBuckets",
        "s3:GetBucketLocation"
      ],
      "Resource": "*"
    },
    {
      "Sid": "DenyDeleteBucket",
      "Effect": "Deny",
      "Action": [
        "s3:DeleteBucket",
        "s3:DeleteObject"
      ],
      "Resource": "*"
    }
  ]
}
✅ Step 4: Attach Policy to User

Attached custom policy directly to:

Developer
🧪 AWS Testing Results
Action	Result
Launch EC2	✅ Allowed
Start/Stop EC2	✅ Allowed
Create S3 Bucket	✅ Allowed
List Buckets	✅ Allowed
Delete Bucket	❌ Access Denied
Delete Object	❌ Access Denied

✔ Explicit Deny overrides Allow
✔ Least Privilege enforced

🔵 PART 2 — Azure RBAC Implementation
✅ Step 1: Create Resource Group

Resource Group Name:

RG-TASK3

Region: Selected nearest region

✅ Step 2: Create Virtual Machine

VM Name:

VM-TASK3

Created inside:

RG-TASK3
✅ Step 3: Create Entra ID User

Service: Microsoft Entra ID
User Name:

devuser

Display Name:

Developer User

Mail Nickname:

devuser
✅ Step 4: Assign Reader Role (Resource Group Level)

Scope:

RG-TASK3

Role:

Reader

Assigned To:

devuser

✔ Can view all resources
❌ Cannot modify

✅ Step 5: Assign Contributor Role (VM Level Only)

Scope:

VM-TASK3

Role:

Contributor

Assigned To:

devuser

✔ Can start/stop VM
✔ Can modify VM
❌ Cannot assign roles
❌ Cannot delete Resource Group
❌ Cannot create new VM

🧪 Azure Testing Results
Action	Result
View Resource Group	✅ Allowed
View VM	✅ Allowed
Start/Stop Assigned VM	✅ Allowed
Create New VM	❌ Denied
Delete Resource Group	❌ Denied
Modify Other Resources	❌ Denied

✔ RBAC successfully implemented
✔ Least Privilege principle enforced

🔐 Key Security Concepts Used
1️⃣ Least Privilege Principle

Users are granted only the permissions required to perform their tasks.

2️⃣ Explicit Deny (AWS)

If a permission is explicitly denied, it overrides any Allow.

3️⃣ Scope-Based RBAC (Azure)

Permissions are assigned at different scopes:

Subscription

Resource Group

Resource (VM)

More specific scope = more controlled access.

📊 Final Architecture Overview
AWS
IAM User (Developer)
   ├── AmazonEC2FullAccess
   └── Custom S3 Policy (Create Allowed, Delete Denied)
Azure
Entra ID User (devuser)
   ├── Reader → Resource Group (RG-TASK3)
   └── Contributor → VM-TASK3 only
🏁 Conclusion

This task successfully demonstrates:

Role-Based Access Control (RBAC)

Least Privilege Principle

Explicit Deny in AWS

Scope-based permission control in Azure

Both AWS IAM and Azure RBAC were configured and tested successfully.
