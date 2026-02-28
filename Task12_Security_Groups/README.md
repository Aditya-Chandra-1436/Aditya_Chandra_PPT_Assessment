# Task 12 – Website Down Alert using Canary (Lambda) + SNS

## Objective
To monitor website availability and send an email alert automatically when the website goes down using AWS managed monitoring services.

---

## AWS Services Used
- Amazon CloudWatch Synthetics (Canary)
- AWS Lambda (managed by Canary)
- Amazon SNS
- Amazon CloudWatch Alarms
- IAM

---

## Steps Performed
1. Created an SNS topic for alert notifications.
2. Added and confirmed an email subscription to the SNS topic.
3. Created a CloudWatch Synthetics Canary to monitor website uptime.
4. Configured the Canary to run periodically and check the website URL.
5. Created a CloudWatch alarm based on Canary failure metrics.
6. Attached the SNS topic to the alarm for notifications.
7. Verified alert by simulating website failure.

---

## Outcome
- Website uptime is continuously monitored using a Canary.
- CloudWatch alarm triggers automatically on website failure.
- Email alert is sent using SNS when the website is down.

