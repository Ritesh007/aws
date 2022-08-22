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
#### Exam Tips
- Remember the term Build Project and why we need it in CodeBuild

### CodeBuild Walk through
- 