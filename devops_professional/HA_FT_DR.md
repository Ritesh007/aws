# High Availability, Fault Tolerance, and Disaster Recovery

## AutoScaling:
### Auto Scaling Launch Templates
- Launch templates (LTs) are newer than launch configurations (LCs) and 
  provide more options to work with. Thus, the AWS documentation recommends 
  use of launch templates (LTs) over launch configuration (LCs)
- Launch Configuration will face out at the end of 2022
- We can reuse and extend launch templates
- You can create a launch template from a launch configuration
- Supports multiple instance type - spot, on-demand and ec2 dedicated hosts
- Can have multiple versions

### ASG Scaling Policies and Scheduled Actions
- __Auto Scaling groups__:
  - are collections of Amazon EC2 instances that enable automatic scaling and fleet management features.
    These features help you maintain the health and availability of your applications.
- Cloudwatch alarm when met with a certain threshold triggers a scaling event
      - __Scaling options__:
        - __Autoscaling policy__: scale based on metrics (like cpu's etc)
        - __Scheduled action__: scale based on time
        - __Manual Scaling__
        - __Predictive scaling__
        - __Maintain current instance levels__
- ASG checks ec2 status checks, and can also use elb health check
- __Lifecycle Hooks__:
  - when in ASG if there is a scale out or scale in activity we can trigger an action using Lifecycle hooks
  - During scale out:
    - in 'pending:wait' state the lifecycle hooks pauses the instance creation to perform an action and after the action is completed
      the state changes to 'pending:proceed'
  - During scale in:
    - in 'terminating:wait' state the lifecycle hooks pauses the instance deletion to perform an action and after the action is completed
      the state changes to 'terminating:proceed'
- __Termination policies__:
  - Decides which instance to terminate
  - If we don't set a termination policy then the default policy is applied
  - We can create custom termination policies select a predefined one
- __Suspend__: we can suspend creation, termination, health check etc. in ASG

### Auto Scaling to support SQS
- We can scale ASG based on the SQS queue using Cloudwatch custom metrics

### Load Balancers Fronting and ASG
- __Load balancer uses its own health check, but it can be configured to use ec2 status checks as well__
- Load balancer routes traffic to only healthy instances in the ASG
- __Load balancer protocols__
  - ALB
    - HTTP
    - HTTPS
  - NLB
    - TLS
    - UDP
    - TCP


### DynamoDB Overview
- fully managed NoSQL database service
- Core concepts:
  - Tables: DynamoDB stores data in tables
  - Items: Each table contains zero or more items
  - Attributes: Each item is composed of one or more attributes
  - Primary Key: The primary key uniquely identifies each item in the table
    - Partition Key: Can be used as a primary key
    - Partition key and sort key : Combination of these two can be used as a primary key
  - Secondary indexes: A secondary index lets you query the data in the table using an alternate key, in addition to queries against the primary key
                       A table can have multiple Secondary indexes
    - Local Secondary indexes: Same partition key with different Sort Key
    - Global Secondary indexes: Different partition and sort keys

### Global tables, DynamoDB Streams, DAX and TTL
- __Global Table__:
  - When you create a DynamoDB global table, it consists of multiple replica tables (one per AWS Region) that DynamoDB 
    treats as a single unit. Every replica has the same table name and the same primary key schema. 
    When an application writes data to a replica table in one Region, DynamoDB propagates the write to 
    the other replica tables in the other AWS Regions automatically.
- __DynamoDB Streams__:
  - DynamoDB Streams is an optional feature that captures data modification events in DynamoDB tables. 
    The data about these events appear in the stream in near-real time, and in the order that the events occurred
  - __DynamoDB Accelerator (DAX)__: In memory cache on the disk with encryption, to accelerate data
    - DAX is a DynamoDB-compatible caching service that enables you to benefit from fast in-memory performance for demanding applications
    - DAX supports server-side encryption. With encryption at rest, the data persisted by DAX on disk will be encrypted
- __TTL__:
  - Amazon DynamoDB Time to Live (TTL) allows you to define a per-item timestamp to determine when an item is no longer needed. 
    Shortly after the date and time of the specified timestamp, DynamoDB deletes the item from your table without consuming any write throughput.

### Highly available RDS
- RDS supports event notifications 
- Multi AZ is synchronous replication, doesn't support read, used for HA, a standby instance in a different AZ
- Read replicas are asyn, supports read

### Content Delivery with CloudFront
- If we don't want to wait for the data on CloudFront to expire, we can invalidate the data on CloudFront to expire using lambda

### Disaster Recovery
- RPO: Recovery point objective 
  - maximum amount of data – as measured by time – that can be lost after a recovery from a disaster
- RTO: Recovery Time objective
  - How long does it take to operate normally back










