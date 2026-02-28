# Task 14 – CloudWatch Alarm (CPU ≥ 70%)

## Objective
To monitor EC2 CPU utilization and automatically stop the instance and send an email alert when CPU usage reaches 70%.

## Services Used
- Amazon EC2
- Amazon CloudWatch
- Amazon SNS

## Steps Performed
1. Created SNS topic and confirmed email subscription
2. Created CloudWatch alarm on EC2 CPUUtilization
3. Set threshold to 70%
4. Configured alarm action to stop EC2
5. Configured SNS email notification

## Result
When CPU usage reaches or exceeds 70%, the EC2 instance is automatically stopped and an email alert is sent.


