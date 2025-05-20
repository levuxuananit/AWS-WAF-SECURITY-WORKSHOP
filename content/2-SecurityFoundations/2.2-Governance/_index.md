---
title : "Governance"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---
### Security Governance
**Security governance** is a crucial part of the overall strategy to protect systems and support business objectives. It goes beyond just technical solutions, involving the definition of security policies and control objectives to help the organization manage risks effectively.

AWS recommends a **layered approach** to security governance. In this model, each security layer complements and builds upon the previous one, forming a strong and flexible defense system.

### Foundational Layer
The first and most important layer is understanding the AWS **Shared Responsibility Model**. According to this model:
- AWS is responsible for the security **of** the cloud infrastructure, including hardware, software, networking, and physical facilities where services are operated.
- Customers are responsible for the security **in** the cloud, including service configuration, data management, user identities, and access rights.
- Understanding this boundary helps organizations clearly identify what they need to control and what they can rely on AWS for.

Additionally, AWS provides [Artifact](https://aws.amazon.com/artifact/), a service that offers security and compliance documentation such as audit reports, certifications, and legal agreements.

### Security Foundation Layer
The second layer is where most of the security control objectives are implemented using AWS tools and services. At this layer, you can:
- Manage AWS accounts using a multi-account model to isolate risks.
- Integrate user identities with systems such as AWS IAM Identity Center.
- Set up detection controls like monitoring, logging, and alerting on unusual events.
- When your organization begins using a new AWS service, you can update **Service Control Policies (SCPs)** in AWS Organizations to ensure the service is only used within approved boundaries.

You can also implement **immutable security guardrails** – policies that apply across multiple accounts or the entire organization and cannot be altered by lower-level users.
Examples:
- Restrict usage of services to specific Regions only.
- Prevent users from disabling detection tools or logging.
- This layer also includes encryption policies, such as using AWS Config rules to track service configurations, or integrating security checks in the CI/CD pipeline to detect misconfigurations early.

### Application Layer
The top layer is where product development teams are directly responsible for implementing security controls within the applications they manage.
Examples:
- Implementing input validation in web applications to prevent SQL Injection attacks.
- Ensuring identities and access rights are correctly passed between microservices.
- Securing APIs and encrypting data in transit.

Although product teams have the primary responsibility at this layer, they can still inherit security policies and tools from the middle layer to ensure consistency and reduce operational burden.

### Shared Objective
Regardless of the layer where controls are applied, the ultimate goal is to manage **risk effectively**. The risk management process includes:
- **Identifying inherent risk**: The initial level of risk before any controls are applied. Assessed based on:
  - **Likelihood**: Based on the frequency or history of incidents.
  - **Impact**: Measured in terms of financial loss, downtime, or damage to reputation.
- **Applying controls**: Defining policies, tools, and configurations to reduce the likelihood, impact, or both.
- **Assessing residual risk**: The level of risk remaining after controls are in place. The organization must decide whether this level of risk is acceptable.

Control objectives may apply to a specific **workload**, or scale across **multiple systems** within the organization.
