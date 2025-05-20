---
title : "Operating your workloads securely"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---
### Ensuring Security Throughout the Entire Workload Lifecycle
To operate a workload securely on AWS, you need to consider security throughout its entire lifecycle — from design, build, operation, to continuous improvement.

One of the most effective ways to achieve this is by applying **Organized Governance**. Governance is not just about making the right decisions, but also ensuring those decisions are consistently implemented, rather than relying on individual experience or judgment.

{{%notice note%}}
You need clear governance processes to answer the question: "How do I know that the security control objectives have been properly implemented for this workload?"
{{%/notice%}}

A consistent decision-making process helps you accelerate deployment and raise security standards across the organization.

### Applying Security Practices Across All Domains
To operate securely, you must ensure that all security domains are covered — from access management, data protection, activity monitoring to incident response.

Apply the defined requirements and processes at both the organizational level and for each specific workload.

Additionally, always keep updated with:
- The latest recommendations from AWS and the industry
- Threat intelligence so you can build risk models and define appropriate control objectives

### Automation is the Key to Effective Security
Automation ensures that security processes are performed consistently and free from human error.

Humans tend to make mistakes, especially when performing repetitive tasks or handling many alerts simultaneously.

In contrast, automation helps:
- Processes to be executed the same way every time
- Easier review of deployment code
- Increased reliability and reduced risk of errors during changes
- Enables easy updates and redeployments, especially when new controls are introduced

### Validate Configurations Before Production Deployment
Before applying any configuration or automation in production, you should:
- Test in a staging or testing environment to ensure automation performs as expected
- Gather early feedback to avoid costly and time-consuming fixes later

Always make changes via code (infrastructure as code), avoiding manual configurations. This makes it easier to repeat, track, and recover from issues.

### Leverage Shared Components Instead of “Each for Themselves”
Instead of letting each team or application build their own security systems, you should develop shared security capabilities to save time and standardize the environment.

Examples of shared components:
- AWS account creation processes
- Centralized identity management systems
- Standard logging configurations
- Pre-built AMIs or containers available for the entire organization

This approach helps:
- Development teams save time on deployment
- Accelerate time-to-market for workloads
- Ensure security objectives are consistently met

With consistency across teams, your organization can also more easily report risks and control status to stakeholders such as executives, customers, or auditors.

### Best Practices
[SEC01-BP03 Define and Validate Control Objectives](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_control_objectives.html)  
[SEC01-BP04 Update Security Threats and Recommendations](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_updated_threats.html)  
[SEC01-BP05 Narrow Security Management Scope](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_reduce_management_scope.html)  
[SEC01-BP06 Automate Deployment of Standard Security Controls](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_automate_security_controls.html)  
[SEC01-BP07 Identify Threats and Prioritize Mitigation Using Threat Modeling](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_threat_model.html)  
[SEC01-BP08 Regularly Evaluate and Deploy New Security Services and Features](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_implement_services_features.html)
