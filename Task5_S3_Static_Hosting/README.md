# Task 5 – Static Website Hosting using Amazon S3

## Objective
To host a static website using Amazon S3 by enabling static website hosting and configuring public access permissions.

This task demonstrates serverless website hosting using AWS S3.

---

## AWS Service Used
- Amazon S3

---

## Steps Performed

### Step 1: Create S3 Bucket
1. Logged in to the AWS Management Console.
2. Navigated to the S3 service.
3. Created a new S3 bucket with a globally unique name.
4. Selected the required AWS region.

---

### Step 2: Disable Block Public Access
1. While creating the bucket, disabled **Block all public access**.
2. Acknowledged the public access warning.
3. Created the bucket successfully.

---

### Step 3: Upload Website Files
1. Opened the created S3 bucket.
2. Uploaded the `index.html` file containing the static website content.

---

### Step 4: Enable Static Website Hosting
1. Opened the **Properties** tab of the bucket.
2. Enabled **Static website hosting**.
3. Selected **Static website hosting** option.
4. Set `index.html` as the index document.
5. Saved the configuration.

---

### Step 5: Configure Bucket Policy for Public Access
1. Opened the **Permissions** tab.
2. Added a bucket policy to allow public read access for objects.
3. Saved the bucket policy.

---

### Step 6: Access the Website
1. Copied the **S3 website endpoint** from the bucket properties.
2. Opened the URL in a web browser.
3. Verified that the static website was accessible publicly.

---

## Outcome
- Successfully hosted a static website using Amazon S3.
- Website is accessible using the S3 static website endpoint.
- No EC2 or server management was required.
