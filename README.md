# 🖥️ AWS Serverless EC2 Scheduler

This project automatically **starts and stops an EC2 instance during working hours** using two AWS Lambda functions, triggered by **EventBridge (CloudWatch Events)** rules. Ideal for cost-saving in environments that don't require 24/7 compute.

---

## ✅ Use Case

Many companies run EC2 instances only during business hours (e.g., 8 AM to 5 PM). This project creates a serverless solution using:

- AWS Lambda
- CloudWatch (EventBridge)
- IAM
- EC2

---

## 🔧 Components

- 2 Lambda functions:
  - `start-ec2.py` — Starts the EC2 instance
  - `stop-ec2.py` — Stops the EC2 instance
- 2 IAM Policies:
  - `StartEC2Policy`: StartInstances, DescribeInstances
  - `StopEC2Policy`: StopInstances, DescribeInstances
- 2 IAM Roles with those policies attached (one per Lambda)
- 2 EventBridge schedules:
  - `start-ec2-rule`: 8:00 AM IST (2:30 AM UTC)
  - `stop-ec2-rule`: 5:00 PM IST (11:30 AM UTC)

---

## 📁 File Descriptions

- `start-ec2.py`: Python script to start an EC2 instance using boto3
- `stop-ec2.py`: Python script to stop an EC2 instance using boto3

---

## 📦 Deployment Steps

1. **Create EC2 Instance** (optional, if not already created)
2. **Create IAM Policies**:
   - Start: `StartInstances`, `DescribeInstances`
   - Stop: `StopInstances`, `DescribeInstances`
3. **Create Lambda Functions**:
   - Python 3.9 or 3.10 runtime
   - Attach the correct IAM role
4. **Create CloudWatch EventBridge Rules**:
   - Use cron expression to trigger at specific times
5. **Test and Monitor**:
   - Use CloudTrail to confirm EC2 start/stop events

---

## 📝 Notes

- Make sure the Lambda execution role has EC2 permissions and CloudWatch logs access
- AWS region should match your EC2 instance (e.g., `ap-south-1`)
- Logs are available in CloudWatch Logs

