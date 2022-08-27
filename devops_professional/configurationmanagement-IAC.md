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
- 
