# Monitoring And Logging

## EventBridge:
### Overview
- Cloudwatch events are renamed to EventBridge with additional functionality 
- __It provides all the functionality like cloudwatch events, and it also supports custom events__
- __Key elements__:
  - Event buses: Event buses receive events from a variety of sources and match them to rules in your account
  - Event
  - EventBridge Rule
  - Target


## CloudWatch Alarms:
### Overview
- __Key elements__:
  - Alarm notification: notifying when an alarm is triggered
  - Alarm action: performing some action when an alarm is triggered 


## CloudWatch Logs and Metrics:
### Overview
- Metrics:
  - Some are provided by aws, and we can create our own custom metrics and namespaces as well
  - __They are regional__
  - __Namespace is a container for metrics__
    - example: AWS/EBS, AWS/ELB, AWS/EC2 etc --> __Remember the format__
  - Can't be deleted but will expire after 15 months
  - __Cloudwatch dimension: K:V pair that uniquely identifies a metric__
  - __Metrics streams__: Stream metrics to s3 or firehose
- Logs:
  - Log groups
  - Log streams
  - Logs
  - Log events
  - Log agent
  - Retention policies
  - Metric filters

## CloudTrail:
### Overview
- Used for auditing on AWS --> CloudTrail records API activity
- __CloudTrail logs are stored in S3__
- __Enable log file validation__: To determine whether a log file was modified, deleted, or unchanged after AWS CloudTrail delivered it
- __CloudTrail can send logs to CloudWatch__

## Kinesis:
### Overview
- 