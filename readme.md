# AWS EC2 CloudWatch Monitoring Project

## Overview

What this project demonstrates

• Infrastructure as Code for repeatable environments
• secure IAM role usage instead of static credentials
• metric collection and operational visibility
• automated alerting pipelines
• validation through simulated load conditions

More importantly, it reflects an engineering mindset. Systems should communicate their health without requiring manual inspection.

## Why did I do this project? 

Large systems rarely fail all at once. Trouble usually begins with small signals such as a CPU spike, throttling, or a resource bottleneck that goes unnoticed until it compounds into downtime, degraded user experience, and expensive incident response.

At scale, reliability comes from catching those early signals and routing them into automated responses before a human ever has to intervene.

This project reflects that mindset in its simplest form.

It provisions compute infrastructure, applies least privilege access, streams operational metrics, and turns system stress into actionable alerts. The goal is not the alarm itself. The goal is building systems that can explain their own health.

## Architecture Diagram
![terraformdiagram](https://github.com/AtharvaGitProfile/AWS-EC2-CloudWatch-Monitoring/blob/master/Terraform%20Diagram.png)

## Resources Created

1. **IAM Role and Instance Profile**
   - Creates an IAM role with policies allowing EC2 to publish metrics to CloudWatch.
   - Creates an instance profile attached to the EC2 instance.
![alttext](https://github.com/AtharvaGitProfile/aws-ec2-cloudwatch-monitoring/blob/912f5ba30dd5cc2a3fa915611924b8c9ee0037f1/IAM%20Role%20HCL.png)

2. **EC2 Instance**
   - Launches an EC2 instance with specified AMI, instance type, and key pair.
   - Associates the IAM instance profile for CloudWatch access.
![alttext](https://github.com/AtharvaGitProfile/aws-ec2-cloudwatch-monitoring/blob/2a9d9b6f5b7382ab4f079f879ca2e08720f44c47/instance.png)

3. **Variable Setup**
   - Sets up the required variables to be used in the configuration of the resources in the infrastructure.
![alttext](https://github.com/AtharvaGitProfile/aws-ec2-cloudwatch-monitoring/blob/b1a81a68ed1152250149fe55a774af9e1f712f22/Variables.png)

4. **CloudWatch Metric Alarm**
   - Sets a CPU utilization alarm that triggers when CPU usage exceeds 80%.
   - Alarm sends notifications via SNS.
![alttextt](https://github.com/AtharvaGitProfile/aws-ec2-cloudwatch-monitoring/blob/23e0c57941329b07930b41c6cd257c6bdf33bdb5/Alarm.png)


5. **SNS Topic and Subscription**
   - Creates an SNS topic for alarm notifications.
   - Subscribes an email endpoint to the SNS topic for alerts.
![alttext](https://github.com/AtharvaGitProfile/aws-ec2-cloudwatch-monitoring/blob/8d02f2c2a522f4af58b7625cc4b6476389a2bcf6/SNS%20Topic%20Subscription.png)

## Usage

- Clone the repository.
- Configure AWS credentials and region.
- Adjust `variables.tf` as needed (AMI ID, instance type, key pair name, etc.).
- Run `terraform init` to initialize the project.
- Run `terraform apply` and confirm to provision resources.
- Perform a CPU stress test on the EC2 instance to trigger alarms.
- Monitor the configured email subscription for SNS alarm notifications.

![alttext](https://github.com/AtharvaGitProfile/aws-ec2-cloudwatch-monitoring/blob/57e040cf156e48b6d99e16eb65590e1884ee9d0e/Alarm%20Notification.png)

## Notes

- Ensured that the IAM user had permissions to manage IAM roles, EC2, CloudWatch, and SNS.
- The alarm evaluation period and threshold are configured in `main.tf`.
