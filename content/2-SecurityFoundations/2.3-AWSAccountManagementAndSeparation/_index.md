---
title : "AWS account management and separation"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---
### Isolating Workloads with Separate Accounts
It is recommended to organize workloads into separate AWS accounts rather than by organizational structure or departments. The most effective separation is based on:
- Function (e.g., production, development, testing)
- Legal compliance requirements
- Common security control policies

Reason: In AWS, accounts act as a strong isolation boundary to limit risk spread. For example, you should use separate accounts to isolate production environments from development and testing environments to ensure safety and stability.

### Centralized Management with AWS Organizations
**AWS Organizations** is a tool that helps you automate the creation, management, and coordination of AWS accounts within a large organization.

When creating new accounts through Organizations, be careful with the email address used, as this is the root account and will be used to recover the password if needed.

Organizations also allow you to group accounts by usage purpose through Organizational Units (OU).

For example, you can group accounts belonging to production environments into one OU, and development accounts into another OU to apply appropriate policies.

### Centralized Control Setup with SCP
You can restrict AWS account behaviors by using **Service Control Policies (SCPs)** — policies applied at the organization, OU, or specific account level.

SCPs allow you to:
- Specify which AWS services, regions, and API actions are permitted.
- Restrict accounts from creating resources in regions that are not explicitly allowed.

For example, you can create an SCP that prevents users from creating resources outside the Asia Pacific region if your organization only wants to operate services in that region.

**AWS Control Tower** is a tool that simplifies this entire setup process. It helps you:
- Automatically create and configure new accounts.
- Apply protective measures (both preventive and detective).
- Provide dashboards to monitor the entire organization.

## Centralized Service and Resource Configuration
With AWS Organizations, you can apply AWS service configurations across all accounts in your organization.

Some practical examples:
- **AWS CloudTrail**: Centrally logs all API activity across the organization to help with monitoring and security audits.
- **AWS Config**: Collects and evaluates resource configurations to ensure policy compliance. You can aggregate data from multiple accounts for rapid monitoring and response to changes.
- **AWS CloudFormation StackSets**: Allows you to deploy infrastructure configurations (stacks) simultaneously to multiple accounts and OUs automatically, ensuring consistency and compliance with security requirements.

### Clear Security Administration Delegation
You should separate security administration accounts from billing or general operational accounts.

Some services like:
- Amazon GuardDuty
- AWS Security Hub
- AWS Config
- ...
Integrate with AWS Organizations and allow you to designate a specific account as the administration account. From there, you can centrally control and monitor security services across all accounts more clearly.

### Best Practices
[SEC01-BP01 Isolate workloads by account](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_multi_accounts.html)  
[SEC01-BP02 Secure root user account and its attributes](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_aws_account.html)
