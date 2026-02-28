# Task 11 – S3 Event Notification using Lambda and SNS

## Objective
To send an email notification automatically whenever a file is uploaded to an Amazon S3 bucket using AWS Lambda and Amazon SNS.

---

## AWS Services Used
- Amazon S3
- AWS Lambda
- Amazon SNS
- IAM

---

## Steps Performed
1. Created an SNS topic and added an email subscription.
2. Confirmed the email subscription.
3. Created a Lambda function using Python.
4. Attached SNS permissions to the Lambda execution role.
5. Added Lambda code to publish messages to the SNS topic.
6. Created an S3 bucket.
7. Configured the S3 bucket to trigger the Lambda function on object upload.
8. Uploaded a file to the S3 bucket.
9. Verified that an email notification was received.

---

## Outcome
- S3 upload events successfully triggered the Lambda function.
- Lambda published messages to SNS.
- Email notifications were received for each file upload.

---

## Screenshots
- SNS topic with confirmed email subscription  
- Lambda function showing S3 trigger  
- Email notification received
