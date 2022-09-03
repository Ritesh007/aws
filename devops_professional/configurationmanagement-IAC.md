# Configuration Management and IAC 


## Elastic BeanStalk:
### Overview
- Steps:
  - Create application by providing the platform and source code
  - Advanced option: Load Balancer, EC2's, deployment config etc
- __EBS is used towards developers, simple to use, all "under the hood concept", quick deploy__
- __If you want complete control 'EBS' is not a good option__
- Key Terms:
  - Application: Consists of multiple env in it
  - Environment: Falls under application
    - Webserver: Run a website, web application, or web API that serves HTTP requests
    - Worker: Run a worker application that processes long-running workloads on demand or performs tasks on a schedule
- When we create EBS application, we are creating a Cloudformation underneath it 

### EBS Deployment Strategies
- All at once
- Rolling deployment 
- Rolling deployment with Additional batches
  - adds additional instances with new code deployed, registers under load balancer and deleted old instances
- Immutable
  - New version instances will de deployed and once they are up, they will replace old version instances
- BlueGreen

### EBS Environment Configuration 
- __Different ways to set Environment configurations in EBS__:
  1. Configuration files are YAML- or JSON-formatted documents with a .config file extension 
    that you place in a folder named .ebextensions and deploy in your application source bundle.
  2. saved configurations in ebs
  3. Direct changes to ebs
- Priority order
  - Highest priority is 3, then 2 and then 1

### EBS Docker Deployments
- EBS supports:
  - Single container 
  - Multi container (ECS)

### EBS with RDS
- We can create an RDS within our EBS environment using advanced configurations.
  - But it's never a good idea for RDS to be part of EBS, because if we delete EBS environment the rds is also deleted - it's good for test not prod
  - It should always be outside EBS 


## Lambda:
### Overview
- It's serverless
- Charged only when it runs
- It's stateless
- It's event driven
- Lambda can be in a vpc or outside a vpc
- __Max timeout for lambda function is 15 minutes__
  - If it takes longer then use step functions 

### Lambda Functions vs. Lambda Applications
- A Lambda function is a piece of code (managed by AWS) that is executed whenever it is triggered 
  by an event from an event source. A Lambda application is a cloud application that includes one or more Lambda functions, 
  as well as potentially other types of services.

### Lambda layers
- Lambda layers provide a convenient way to package libraries and other dependencies that you can use with your Lambda functions

### Lambda Versions and Aliases
- We can publish one or more versions of a lambda function
  - __default version - $Latest__
- Alias can point to 1 or 2 versions 
- Using Alias we can change the version pointer quickly with no or minimal downtime

### Lambda SAM(Serverless Application Model) framework
- AWS Serverless Application Model (AWS SAM) is an open-source framework that you can use to build serverless applications on AWS
- It is a cloudformation extension optimized for serverless applications
- When we run sam code it transforms to cloudformation internally and deploys to aws
- SAM has its own CLI
- AWS SAM templates are an extension of AWS CloudFormation templates
- __The AWS::Serverless transform, which is a macro hosted by CloudFormation, takes an entire template written in 
    the AWS Serverless Application Model (AWS SAM) syntax and transforms and expands it into a compliant CloudFormation template__
  - Transform: AWS::Serverless-2016-10-31
#### Exam Tips
- SAM syntax is Cloudformation - only yaml not json


## Step Functions:
### Overview
- AWS Step Functions help us implement State Machines
- AWS Step Functions is a serverless orchestration service
  - Using AWS Step Functions Service Integrations, you can configure your Step Functions workflow to call over 200 AWS services. 
    This includes compute services (AWS Lambda, Amazon ECS, Amazon EKS, and AWS Fargate), database services (Amazon DynamoDB), 
    messaging services (Amazon SNS and Amazon SQS), data processing and analytics services (Amazon Athena, AWS Batch, AWS Glue, 
    Amazon EMR, and AWS Glue DataBrew), machine learning services (Amazon SageMaker), and APIs created by Amazon API Gateway
- Step Functions is based on state machines and tasks.
- __State machines__:
  - Is a collection of tasks
  - Each state will take input from a previous state
  - Standard vs Express Workflows
    - Standard Workflows are ideal for long-running, durable, and auditable workflows. They can run for up to a year.
    - Express Workflows are ideal for high-volume, event-processing workloads such as IoT data ingestion, streaming data processing and transformation, and mobile application backends. 
      They can run for up to five minutes
- __Step functions allow human approval__


## API Gateway:
### Overview
- HTTP:
  - __Cheaper and faster than REST__
  - Supports lambda and HTTP
  - __Doesn't have all features as REST__
- Rest APIs: 
  - __Think of this as one-way communication (request and response model)__
  - A response can't happen without a request
  -  Supports lambda, HTTP and AWS Services
- WebSocket:
  - __A 2 way channel__
  - A response can be sent without a request
- __API gateway can be integrated with lambda irrespective of lambda is in a VPC or not__
- __To connect to other private resources in a VPC, we need to create VPC links in API Gateway__

### API Gateway with Lambda Proxy integration
- Enabling this while setting up API Gateway and lambda integration:
  - requests will be proxied to Lambda with request details available in the events of the lambda handler
- __For API gateway to access lambda - a lambda resource based policy should be added__


## Cloudformation:
### Overview
- It's IAC
- First line in CloudFormation - AWSTemplateFormatVersion
- Resources is the only mandatory section 
- Template:
  - AWSTemplateFormatVersion (optional)
  - Description (optional)
  - [MetaData](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/metadata-section-structure.html): (optional)template implementation details about specific resources
  - Mapping(optional)
  - Parameters(optional)
  - Resources -> Only required section in cloudformation 
  - Outputs(optional)
  - Conditions (optional)
  - Rules(optional): validates a parameter or a combination of parameters passed to a template during a stack creation or stack update
  - Transform(optional):
    - For SAM
    - and other purpose is to include extra code into our template

### Cloudformation intrinsic functions
- Key intrinsic functions 
  - Ref
  - Fn::GetAtt
  - Fn::FindInMap
  - Fn::ImportValue
  - Fn::Join
  - Fn::Sub
  - Conditional Functions 

### Cloudformation wait conditions and creation policies
- __Wait conditions__:
  - Pause the execution of the stack creation till success signal is received 
  - Syntax:
    - WaitHandle:
        Type: AWS::CloudFormation::WaitConditionHandle
      WaitCondition:
        Type: AWS::CloudFormation::WaitCondition
      Properties:
        Count: Integer
        Handle: !Ref 'WaitHandle'
        Timeout: String
  - __Creation policies__: 
    - Similar to wait condition, but instead of being a separate resource like wait condition, these are attributes in a resource
  - Syntax:
    - CreationPolicy:
        ResourceSignal:
          Count: '3'
          Timeout: PT15M
  - Creation policies are preferred for ec2's and auto-scaling groups

### [CloudFormation Helper Scripts](https://catalog.workshops.aws/cfn101/en-US/basics/operations/helper-scripts)
- AWS CloudFormation provides the following Python helper scripts that you can use to install software 
  and start services on an Amazon EC2 instance that you create as part of your stack:
  - cfn-init: Use to retrieve and interpret resource metadata, install packages, create files, and start services.
  - cfn-signal: Use to signal with a CreationPolicy or WaitCondition, so you can synchronize other resources in the stack when the prerequisite resource or application is ready.
  - cfn-get-metadata: Use to retrieve metadata for a resource or path to a specific key.
  - cfn-hup: Use to check for updates to metadata and execute custom hooks when changes are detected.
- __Used in ec2 user data__
- __Works with metadata section in the template__

### CloudFormation Stack Protection 
- There are 4 ways to do it
  - Enable Termination protection on the Stack
  - Stack level policies 
  - Resource level policies 
  - IAM policies 

### Updating CloudFormation Stacks 
- Direct updates 
- Change sets

### CloudFormation nested stacks and cross stack references 

### CloudFormation Drift detection and remediation 
- If there are changes to the infrastructure from outside the stack that is called Drift
- Detect Drift 
  - From AWS Console drift detection in the cloudformation service
  - Using AWS Config

### [CloudFormation custom resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cfn-customresource.html#cfn-customresource-servicetoken) 
- In a CloudFormation template, you use the AWS::CloudFormation::CustomResource or Custom::String resource type to specify custom resources.
- Custom resources provide a way for you to write custom provisioning logic in CloudFormation template and have 
  CloudFormation run it during a stack operation, such as when you create, update or delete a stack.


## OpsWorks Essentials
### Overview
- Provide managed instances for Chef and Puppet
- OpsWork Stack:
  - A stack is a set of layers, instances and related AWS resources whose configuration you want to manage together.
  - Every stack contains at least one layer
  - example - layer1 has a load balancer, layer2 has ec2 instances, layer3 is RDS
- Stacks: A set of resources we want to manage as a group . Use case : can build a stack for dev , staging , production
- Layers: Used to represent and configure components of a stack . Example : a layer for load balancer , a layer for web app , and a
  layer for database
- Instances: Relates to at least one layer
- Apps: deploy applications on the instances, chef/puppet help in preparing the instances to run the application

### Creation steps
- Create Stack
- Add layer
- Create instance 
- ADD apps
- deploy apps using chef/puppet recipes/cookbooks

### OpsWorks Flavors
- OpsWorks Stack: Define, group, provision, deploy, and operate your applications in AWS by using Chef in local mode.
- OpsWorks for chef automate: Create Chef servers that include Chef Automate premium features, and use the Chef DK or any Chef tooling to manage them.
- OpsWorks for Puppet Enterprise: Create Puppet servers that include Puppet Enterprise features. Inspect, deliver, update, monitor, and secure your infrastructure.

### Deployment Strategies with OpsWorks
- Each Layer in ops works have 5 life cycle events
  - Setup
  - Configure
  - Deploy
  - undeploy
  - Shutdown
- based on the lifecycle events ops work runs recipes 
- Deployment strategies for Ops works
  - Manual
  - Rolling
  - BlueGreen

### Exam Tips
- Ops integrates with Core aws services not all like cloudformation


## ECS
### Overview
- 


