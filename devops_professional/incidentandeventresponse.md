# Incident And Event Response

## Incident And Event Response:
### Overview:
- Relate concepts of Autoscaling, CloudWatch alarms, CloudWatch events, Ops work and Cloudformation


## CloudFormation Rollback:
### Overview
- Go over CloudFormation troubleshooting

## CodeDeploy Rollback:
### Overview
- cli for CodeDeploy is not `aws codedeploy` it is `aws deploy`
- Configure SNS 'pre-deployment'
- Deployment statuses:
  - Created
  - Queued 
  - In progress
  - Baking
  - Ready
  - Failed
  - Succeeded
  - Stopped


## Guard Duty:
### Overview
- Intelligent threat protection for accounts and workloads using ML
- Amazon GuardDuty is a continuous security monitoring service that analyzes and 
  processes data sources, such as AWS CloudTrail data events for Amazon S3 logs, 
  CloudTrail management event logs, DNS logs, Amazon EBS volume data, Amazon EKS audit logs, and Amazon VPC flow logs
- Findings can be delivered to S3 or/and EventBridge or Lambda
- Inspector analyses our applications whereas Guard Duty does an account level analysis
- Macie, analyzes data and data security on AWS S3


## AWS Inspector:
### Overview
- Amazon Inspector is a vulnerability management service that continuously scans your AWS workloads for vulnerabilities
- Amazon Inspector automatically discovers and scans Amazon EC2 instances and container images residing 
  in Amazon Elastic Container Registry (Amazon ECR) for software vulnerabilities and unintended network exposure
- Can interact with Lambda and SNS for automation 

## Security Hub:
- Cloud security poster management

## Trusted Advisor:
- Provides recommendations on best practices

## AWS Config:
- Compliance and auditing 
