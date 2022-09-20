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

### AutoScaling Lifecycle hooks for configuring policies
- 






