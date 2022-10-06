# Practice exam 1 

- aws:PrincipalTag is a tag that exists on the user
- ec2:ResourceTag is a tag that exists on the instance
- CodeCommit does not provide a generate release notes feature
- some servers, a MySQL database, and a load balancer - the easiest way tp set this up is OpsWork
- AWS Server Migration Service: migrate servers from on-premise to AWS
- EC2 servers in a cluster placement group: 
  - A cluster placement group is a logical grouping of instances within a single Availability Zone. 
    A cluster placement group can span peered VPCs in the same Region. Instances in the same cluster 
    placement group enjoy a higher per-flow throughput limit for TCP/IP traffic and are placed in the 
    same high-bisection bandwidth segment of the network
- Native encryption supported: EFS, EBS, S3 and ElasticCache for Redis but not for ElastiCache for Memcached
- The AWS Management Console sign-in is a valid event source in CloudWatch Events and EventBridge
- Memory utilization is not a default CloudWatch metric, so you will have to publish a custom metric first
- While you can import certificates to AWS Certificate Manager, the auto-renewal won't work instead generate new ones with ACM
- CloudFront supports wildcard certificates

# Practice exam 2
- CLI order:
  - Command line options -> Environment variables -> CLI credentials -> CLI Configuration File -> Container credentials -> Instance credentials
- Which of the following files must be included with multi-container Docker environments on Elastic Beanstalk?
  - Dockerrun.aws.json
- In EBS: The .config file is valid in JSON or YAML
- Use SQL with Kinesis Data Analytics
- Code Deploy supports canary only for ecs and lambda 