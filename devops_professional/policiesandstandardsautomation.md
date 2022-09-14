# Policies and Standards Automations

## AWS Organizations for Multi-Account Environment:
### Overview
- Manage multiple AWS accounts under a __single management account__
- __Terminology__:
  - __Organizational units__: Group of single or multiple accounts within an organization
  - __Member accounts__: Any account other than the management account and Organizational units
- No additional billing for Organizations but the owner of the management account pays for the bills on the accounts in it
- __Service control policies (SCPs)__ are a type of organization policy that you can use to manage permissions in your organization.
  __SCPs offer central control over the maximum available permissions for all accounts in your organization__
- __AWS Cloudformation StackSets and AWS Service Catalog helps in automating deployments across accounts in an organization__


## Trusted Advisor for policies and standards:
### Overview
- Provides recommendations on our account on the following topics
  - Cost optimization 
  - Service limits
  - Security
  - Performance
  - Fault tolerance
- Different plans:
  - Basic
  - Developer
  - Business
  - Enterprise


## Service Catalog for organizational control:
### Overview
- Consists of a catalog of products, which are basically cloudformation templates we can upload
- Then we can deploy this products by passing input parameters 
- Key terms:
  - __Portfolios__: collection of products 


## Systems manager Introduction and Setup:
### Overview
- 






