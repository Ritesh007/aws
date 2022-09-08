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
- Used for auditing on AWS --> __CloudTrail records API activity__
- __CloudTrail logs are stored in S3__
- __Enable log file validation__: To determine whether a log file was modified, deleted, or unchanged after AWS CloudTrail delivered it
- __CloudTrail can send logs to CloudWatch__

## Kinesis:
### Overview
- When you see real time data flow think of Kinesis
- Collect, process, analyze, stream data real time
- __Types of Kinesis__ 
  - Kinesis Video stream: 
    - stream videos real time
  - Kinesis Data streams:
    - Collect gigabytes of data per second and make it available for processing and analyzing in real time
  - Kinesis Data Firehose:
    - Process and deliver data streams
    - Amazon Kinesis Data Firehose is the easiest way to capture, transform, and load data streams into 
      AWS data stores for near real-time analytics with existing business intelligence tools
    - Does ETL for the data
  - Kinesis Data Analytics :
    - Analyze streaming data and gain actionable insights in real time


### XRay:
### Overview
- 