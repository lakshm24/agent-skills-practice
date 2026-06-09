--- 
name: aws-ec2-status
description: >
  Check the status of AWS EC2 instances in a given region.
  Use when asked about instance health, running instances, stopped instances or EC2 state checks.
---
# AWS EC2 Status Check

## Overview
Retrieves and summarizes the current state of EC2 instances across a specified AWS region.

## Prerequisites
- AWS CLI installed and configured
- Appropriate IAM permissions (ec2:DescribeInstances) 

## Workflow
1. Identify the target AWS region
2. Run the status check command
3. Filter by state if needed (running/stopped/terminated)
4. Report findings clearly

## Commands
```bash
# list all instances in a region
aws ec2 describe-instances --region us-east-1 \ 
  --query 'Reservations[*].Instances[*].[InstanceId, State.Name, InstanceType]' \
  --output table 

# filter only running instances
aws ec2 describe-instances --region us-east-1 \
  --filters "Name=instance-state-name,Values=running" \
  --query 'Reservations[*].Instances[*].[InstanceId, InstanceType,PublicIpAddress]' \
  --output table
```