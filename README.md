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

# ObjectivePermalink
Recommend a manageable, secure, scalable, high performance, efficient, elastic, highly available, fault tolerant and recoverable architecture that allows the startup to organically grow. The architecture should specifically address the requirements/concerns as described above.

# AssumptionsPermalink
The application is already built, and no significant changes need to be made to host it in AWS.
The application is considered to be business critical for the start-up.
The application is built using typical three-tier architecture.
The delivery team would be connecting with the AWS environment over the internet. If private connectivity is required then additional services like VPN, AWS DirectConnect would required to be setup.
Access to AWS account(s) will be controlled through AWS Identity and Access management (IAM), integration with external identity provider and SSO is not considered.
There are no specific compliance requirements defined for this workload like HIPAA, PCI-DSS, FedRAMP etc.

# Solution
