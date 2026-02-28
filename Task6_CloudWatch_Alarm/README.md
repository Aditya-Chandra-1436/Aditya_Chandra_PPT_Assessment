# Task 6 – S3 Replication and Lifecycle Policy

## Objective
To configure **Amazon S3 Replication** for automatic backup of objects and apply a **Lifecycle Policy** for cost optimization by transitioning data to cheaper storage classes.

This task demonstrates understanding of data protection and cost management in Amazon S3.

---

## AWS Services Used
- Amazon S3
- IAM (Auto-created replication role)

---

## Part A: S3 Replication Configuration

### Description
In this part, objects uploaded to a source S3 bucket are automatically replicated to a destination S3 bucket using S3 replication rules.

---

### Steps Performed

1. Created a **source S3 bucket**.
2. Created a **destination S3 bucket**.
3. Enabled **Versioning** on both source and destination buckets (mandatory for replication).
4. Configured an **S3 Replication Rule** on the source bucket:
   - Applied to all objects
   - Destination bucket selected
   - IAM replication role auto-created by AWS
5. Uploaded new objects to the source bucket **after** enabling the replication rule.
6. Verified that objects were automatically replicated to the destination bucket.

---

### Important Replication Note
> Amazon S3 replication only applies to objects uploaded **after** the replication rule is created. Objects uploaded before enabling replication are not replicated automatically.

---

## Part B: S3 Lifecycle Policy Configuration

### Description
A lifecycle rule was created to automatically move objects to a lower-cost storage class after a specified time period.

---

### Steps Performed

1. Opened the **source S3 bucket**.
2. Navigated to the **Management** tab.
3. Created a **Lifecycle Rule** with the following configuration:
   - Applied to all objects
   - Transition current versions of objects
   - Move objects to **Glacier** storage class after 30 days
4. Enabled and saved the lifecycle rule.

---

## Outcome
- Successfully configured S3 replication between two buckets.
- Verified automatic replication of newly uploaded objects.
- Implemented a lifecycle policy to reduce storage costs by transitioning data to Glacier.
- Demonstrated backup strategy and cost optimization using Amazon S3.

---

