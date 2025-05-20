---
title : "Security Foundations"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---
### Security Pillar
**The Security Pillar** includes the ability to protect data, systems, and assets to leverage cloud technologies to enhance the level of security.

### Design Principles
In the cloud, to enhance the security of your workloads, you should follow these principles:
- **Establish a strong identity foundation**: Apply the principle of least privilege, clearly separate duties, and centrally manage identities. Avoid using long-term static credentials.
- **Enable traceability**: Monitor, alert, and log all activities in real time. Integrate with systems to automate investigation and response.
- **Apply security at all layers**: Implement defense in depth from the network layer to applications and source code. Each layer should have its own protective mechanisms.
- **Automate security**: Use security as code solutions to simplify deployment, control, and scale securely and efficiently.
- **Protect data in all states**: Classify data and use encryption, tokenization, and access control during transmission and storage.
- **Minimize direct access to data**: Optimize by automating processes and using tools to reduce manual interaction, thus lowering human-related risks.
- **Prepare for security incidents**: Establish appropriate response policies and procedures. Regularly practice and use automation tools to accelerate detection and recovery.

### Best Practice Areas
Security in the cloud covers seven areas:
- **Security Foundations**: Establish fundamental principles and a strong secure environment from the start, including proper account setup, organizational templates, basic security controls, and governance policies.
- **Identity and Access Management (IAM)**: Ensure only authorized people, services, and systems can access resources. Apply the principle of least privilege, multi-factor authentication (MFA), and centralized access management.
- **Detection**: Monitor and log activities in the AWS environment. Use services like AWS CloudTrail and Amazon GuardDuty to detect abnormal or risky behavior.
- **Infrastructure Protection**: Implement layered security to protect networks, servers, and services from unauthorized access. Includes VPC configuration, security groups, firewalls, and traffic control.
- **Data Protection**: Protect data in transit and at rest through mechanisms like encryption, access control, and data classification by sensitivity level.
- I**ncident Response**: Prepare processes and tools to respond promptly to security incidents. Includes simulations, event logging, and automating detection, analysis, and recovery processes.
- **Application Security**: Integrate security into the software development lifecycle (DevSecOps). Perform vulnerability scanning, patch management, and encrypt information within the application to ensure safety from the source code level.

### Security Foundations Table of Contents
- [Security Pillar](./2-SecurityFoundations/)
- [Shared Responsibility Model](./2.1-SharedResponsibility/)
- [Governance](./2-SecurityFoundations/2.2-Governance/)
- [Account Management and Separation](./2.3-AWSAccountManagementAndSeparation/)
- [Operating Your Workloads Securely](./2.4-OperatingYourWorkloadsSecurely/)

