# SDLC Automation

## CI/CD Concepts:
### Problem statement 
- Rapid Releases with Stable systems

### Solution
- Devops - an intersection of Dev, Ops and QA, which enables shorter release cycles and stable systems
- Key part of this is Automation 
- Devops Infinite cycle - Plan, Code, Build, Test, Release, Deploy, Operate, Monitor (To remember - PCB-TR-DOM)

### What is CI/CD
- CI - Continuous Integration 
- CD - Continuous Delivery or Continuous Deployment 
  - Continuous Delivery - Getting everything ready for deployment but not deploying
  - Continuous Deployment - Deploying continuously till prod

### Tools provided by AWS for CI/CD 
- __Code Commit__: Used to store code (source code repository)
- __Code Build__: For CI (building the code)
- __Code Deploy__: For CD (deploying the code)
- __Code Pipeline__: Managing the whole CI/CD pipelines


## CodeCommit:
### Overview
- AWS Managed Service that host Git Repositories
- Highly Available, Scalable, Fault Tolerant 
- Integrates with key AWS services 
- Works with existing git based tools
#### Exam Tips 
- CodeCommit has many benefits but it is not the only repository we can use for AWS CI/CD pipelines
- When setting up the AWS CI/CD pipelines, dropdowns are of great help
- Other repos we can use in AWS CI/CD - S3, GitHub, BitBucket and GitHub enterprise
  - __For S3 to act like a source code repository - turn on versioning__

### CodeCommit Repository Actions:
- __CLI Actions__: 
  - Create: `aws codecommit create-repository --repository-name <name-of-repository>`
  - View: `aws codecommit get-repository --repository-name <name-of-repository>`
  - List: `aws codecommit list-repositories`
  - Delete: `aws codecommit delete-repository --repository-name <name-of-repository>`
#### Exam Tips 
- Using this CLI operations we can script it - which leads with automation
- Most of the commands are very literal 

### CodeCommit Cloning, Commit, Pushes and Pulls
- These are regular git commands
- To use the git commands against the AWS CodeCommit users must have git credentials generated from their IAM security credentials

### CodeCommit Merging and Branching
- Similar to regular git

### CodeCommit Data Security
- Encryption: 
  - Data is encrypted in transit and at rest by AWS KMS. When we create the repository in CodeCommit 
    AWS creates a KMS key in the background and uses that to encrypt.
  - Repositories are automatically encrypted at rest using KMS
  - Repositories are encrypted at transit based on our choice of setup - SSH or HTTPS
#### Exam Tips
- AWSCodeCommitPowerUser policy: This policy allows users access to all the functionality of CodeCommit and repository-related resources, 
  except it does not allow them to delete CodeCommit repositories or create or delete repository-related resources in other AWS services, such as Amazon CloudWatch Events. We recommend that you apply this policy to most users.


## CodeBuild:
### Overview
- __What is CodeBuild__
  - AWS Managed CI service which runs tests, builds packages/artifacts that are ready to deploy
- __Access to CodeBuild__
  - Console, CLI, SDK, using Code pipeline
- __Output Artifacts__
  - Stored in S3 - The S3 bucket is encrypted and versioned 
- __Build Project__
  - Tells CodeBuild where the source code is, which build env to use, what commands to run and where to store the artifacts
- __Build Spec__
- Set of build commands
#### Exam Tips
- Remember the term Build Project & Build spec and why we need it in CodeBuild

### CodeBuild Walk through
- __CodeBuild Input__
  - Build project
- __CodeBuild Outputs__
  - S3 bucket

### Working with Build Projects and the Build Spec file
- __Steps in a Build Project__
  1. Submitted
  2. Provisioning 
  3. Download Source
  4. Install
  5. Pre Build
  6. Build
  7. Post Build
  8. Upload Artifacts
  9. Finalizing
  10. Completing
- __Build Spec__
  - Set of build commands in yaml format
  - Can be part of the source code or the build project
  - By default - If we want the buildspec in the source code - it should be in the project root folder named `buildspec.yml`
  - If we want a different name and placement for the buildspec file then mention the location in the build project
  - Only 1 buildspec per build project
  - phases and version are mandatory in buildspec file, rest all are optional

### CodeBuild VPC
- Typically, AWS CodeBuild cannot access resources in a VPC
- In the Build project - To access resources in a VPC from code build we need to setup VPCID, Security group id and subnet id that your AWS CodeBuild project will access


## CodeDeploy:
### Overview
- AWS Managed Deployment service - supports on-premise, ec2, lambda and ecs
- __Can deploy cross region__
- Terminology:
  - __Application__: tells on which one of these we want the deployment to be - on-premise, ec2, lambda and ecs
  - __Deployment Group__: Is where we mention on where to deploy and service roles
    - You can associate more than one deployment group with an application in CodeDeploy
  - __Deployment configuration__: Tells how to deploy 
- __To use ec2 or on-premise we need to install CodeDeploy agents on the instances__

### appsec.yml
- This is a yaml or json formatted file
- Defines the specifications for the deployment
- appspec.yml or appspec.yaml should be in the root directory of the source code
- Helps in running lifecycle events during deployment - using 'hooks'
  - __Hooks__:
  - BeforeInstall: "BeforeInstallHookFunctionName"
  - AfterInstall: "AfterInstallHookFunctionName"
  - AfterAllowTestTraffic: "AfterAllowTestTrafficHookFunctionName"
  - BeforeAllowTraffic: "BeforeAllowTrafficHookFunctionName"
  - AfterAllowTraffic: "AfterAllowTrafficHookFunctionName"
- __Think about appspec file and hooks in appspec file to run custom actions during deployment__


## CodePipeline:
### Overview:
- AWS managed CD service
- Automated the deployment pipelines
- __Source stage__:
  - Mandatory 
  - Supported sources: ECR, CodeCommit, Bitbucket, GitHub, GitHub Enterprise, S3
- __Build stage__:
  - Build or Deploy stage, anyone is mandatory
  - Supported: Jenkins, CodeBuild
  - __Jenkins needs an AWS plugin__
- __Deploy Stage__:
  - Build or Deploy stage, anyone is mandatory
  - Supported: CodeDeploy, ECS, Cloudformation, Service Catalog, Cloudformation StackSet, AppConfig, S3, EBS, OpsWork stack, Alexa Skill Set

### CodePipeline Continuous Delivery and Approval Actions
- __We can add approval actions in our pipeline__
- __Approvals can be added within a stage or between stages__

### CodePipeline with EventBridge
- __EventBridge can work in any stage in the pipeline__

### Jenkins with AWS Developer Tools
- Jenkins is an open source CI/CD tool
- Jenkins can replace CodeBuild or CodePipeline or CodeDeploy
- Jenkins interacts with AWS using AWS plugins
- Jenkins working model - master slave model
- __Jenkins plugin for CodeBuild can be used to trigger codebuild from jenkins jobs__


## SDLC Automation Scenarios:
- __For any question in the exam try to visualize the flow in you mind, some questions may need notepad for visualization__