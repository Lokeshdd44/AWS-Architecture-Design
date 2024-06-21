# AWS-Architecture-Design
I came across an interesting scenario about a start-up looking to migrate their existing application onto cloud (AWS in this case). 

# Scenario
I magine you meet a samll startup company planning to launch a new application that allows consumers & service providers to interact in real time. Currently, their architecture uses LAMP stack comprising of opern-source software. Like many small start-ups they are condident that they will be the next big thing and expect significant, rapid, yed un-quantified growth in the next few months. With this in mind, they are concerned about the following:

  1. Scaling to meet the demand, but with uncertainty around when and how much this demand will be – they are very concerned about buying too much infrastructure too soon or not enough too late!
  2. Disaster Recovery planning, since this application is core their business.
  3. Manage user identities & sync user specific data across multiple devices.
  4. Ability for Service Providers to send notifications to consumer.
  5. Ability to run analytics on top of collected data, with analytics they should be able to visualize & understand app data usage.
  6. Ability to configure their database and data access layer for high performance and throughput.
  7. Effective distribution of load.
  8. A self-healing infrastructure that recovers from failed service instances.
  9. Security of data at rest and in transit.
 10. Securing access to the environment as the delivery team expands.
 11. An archival strategy for inactive objects greater than 6 months.
 12. Ability to easily manage and replicate multiple environments based on their blueprint architecture.

# Objective
Recommend a manageable, secure, scalable, high performance, efficient, elastic, highly available, fault tolerant and recoverable architecture that allows the startup to organically grow. The architecture should specifically address the requirements/concerns as described above.

# Assumptions
The application is already built, and no significant changes need to be made to host it in AWS.
The application is considered to be business critical for the start-up.
The application is built using typical three-tier architecture.
The delivery team would be connecting with the AWS environment over the internet. If private connectivity is required then additional services like VPN, AWS DirectConnect would required to be setup.
Access to AWS account(s) will be controlled through AWS Identity and Access management (IAM), integration with external identity provider and SSO is not considered.
There are no specific compliance requirements defined for this workload like HIPAA, PCI-DSS, FedRAMP etc.

# Solution
![image](https://github.com/Lokeshdd44/AWS-Architecture-Design/assets/99136410/af517b9b-fab9-4c4d-b452-ee840d417328)

# Solution Flow
  1. Customer/Service Provider (User) initiates real-time interaction through the client app. User is redirected to Amazon Cognito for sign-in/sign-up.
  2. After successful authentication the client app receives the access token from Amazon Cognito.
  3. Amazon Cognito also enables the sync of user specific data across multiple devices.
  4. The client app communicates with the backend APIs through Amazon Route 53. Route 53 decides which region the request should be forward to based on the routing rules.
  5. The request is forwarded to Application Load Balancer from Route 53 where it is inspected by Web Application Firewall for vulnerabilities.
  6. If no vulnerabilities are detected Application Load Balancer sends the request to Elastic Beanstalk auto-scaling group where the request is processed by one of the application instances.
  7. Application interacts with the Amazon Aurora database through RDS proxy and performs the request CRUD operations on the database and returns the response back to the application.
  8. Amazon Pinpoint continuously collects usage data from application and makes it available for analysis. The data is also continuously exported to Amazon S3 since Amazon Pinpoint can only store data for 90 days. Additionally, Amazon QuickSight is used to perform advanced analytics and create interactive dashboards.
  9. Any data older than 6 months is archived to Glacier by using S3 lifecycle management policy.
 10. Based on the analysis provided by Amazon Pinpoint the application can trigger push notifications to specific (or all) users.
 11. The developer checks-in the code changes to AWS CodeCommit, the code is scanned for credentials leak, code quality, open-source vulnerabilities etc.
 12. AWS CodeBuild then builds the required container image(s) and pushes the image(s) to AWS Elastic Container Registry (ECR).
 13. In ECR the container images are scanned for any vulnerabilities using Amazon Inspector.
 14. AWS CodeDeploy then pushes the new version to Elastic Beanstalk. Elastic Beanstalk pulls the latest image from ECR and initiates the deployment process.
 15. The delivery team accesses the AWS account using IAM credentials to perform their tasks, principle of least privileges is followed when granting access to the delivery team members.
 16. All services are monitored using AWS CloudWatch and AWS CloudTrail.
 17. AWS Cost management tools are used for creating budgets and cost alerts.
 18. AWS Trusted Advisor recommendations are reviewed periodically to ensure that the application remains in a Well-Architected state.
