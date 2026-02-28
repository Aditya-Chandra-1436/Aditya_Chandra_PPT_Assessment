# Task 13 – Start/Stop EC2 using Lambda and API Gateway

## Objective
To automate starting and stopping an EC2 instance using an HTTP API by integrating AWS Lambda with API Gateway.

---

## AWS Services Used
- Amazon EC2
- AWS Lambda
- Amazon API Gateway (HTTP API)
- IAM

---

## Steps Performed
1. Created an EC2 instance to be controlled.
2. Created a Lambda function to start and stop the EC2 instance using AWS SDK.
3. Attached `AmazonEC2FullAccess` policy to the Lambda execution role.
4. Created an HTTP API in API Gateway.
5. Created a route `/ec2` and integrated it with the Lambda function.
6. Enabled default stage with auto-deploy.
7. Triggered the API using query parameters to start and stop EC2.

---

## API Endpoints Used
- **Stop EC2**
https://<api-id>.execute-api.<region>.amazonaws.com/ec2?action=stop

- **Start EC2**
https://<api-id>.execute-api.<region>.amazonaws.com/ec2?action=start

---

## Outcome
- API Gateway successfully triggered Lambda.
- Lambda started and stopped the EC2 instance based on API input.
- EC2 state changes were verified from the EC2 console.

---
