---
title : "Shared Responsibility"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---
### What is the Shared Responsibility Model?
The **Shared Responsibility Model** is a core concept in AWS cloud computing, which clearly defines the boundaries between AWS’s responsibilities and the customer’s responsibilities for ensuring security and compliance. In this model, AWS is responsible for securing the **"cloud infrastructure"**, which includes hardware, software, networking, and physical facilities that run AWS services. On the other hand, customers are responsible for **"security in the cloud"**, meaning all configurations, data, and applications they deploy and use within the AWS environment.

![Shared-Responsibility](/images/2.prerequisite/aws-shared-responsibility.png)

### AWS Responsibilities
AWS is responsible for protecting the infrastructure that runs all of the services offered in the AWS Cloud. This infrastructure includes hardware, software, networking, and facilities that run AWS Cloud services.

### Customer Responsibilities
Customer responsibility is determined by the AWS Cloud services that a customer selects. This defines the amount of configuration work the customer must perform as part of their security responsibilities.

For example: A service like Amazon Elastic Compute Cloud (Amazon EC2) is classified as Infrastructure as a Service (IaaS), and therefore requires customers to perform all necessary security management and configuration tasks. Customers deploying EC2 instances are responsible for managing the guest operating system (including updates and security patches), any application software or utilities installed by the customer on the instances, and the configuration of the firewall provided by AWS (called Security Groups) on each instance. For abstracted services such as Amazon S3 and Amazon DynamoDB, AWS operates the infrastructure layer, operating system, and platform, while customers access endpoints to store and retrieve data. Customers are responsible for managing their data (including encryption options), classifying their assets, and using IAM tools to apply appropriate permissions.

### The Shared Responsibility Model Extends to IT Controls
Responsibility for IT controls is shared between AWS and customers, similar to the way on-premises IT infrastructure operates. AWS relieves customers of some operational burdens by managing physical infrastructure controls. Each customer’s implementation model is different, resulting in a distributed control environment. Customers can use AWS compliance documentation to assist in control evaluations and validation.

Control responsibilities may fall to AWS, the AWS customer, or be shared:
- **Inherited controls**: Controls that the customer fully inherits from AWS.
- **Shared controls**: Controls that apply to both the infrastructure layer and the customer layer but in different contexts or perspectives. In shared controls, AWS provides the requirements for the infrastructure, and customers must implement their own control measures in their use of AWS services.
- **Customer-specific controls**: Controls that are entirely the responsibility of the customer, based on the applications they deploy within AWS services.
