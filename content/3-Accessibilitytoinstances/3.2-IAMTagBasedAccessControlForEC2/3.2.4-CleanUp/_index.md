---
title : "Clean Up" 
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 3.2.4 </b> "
---
{{%notice note%}}
Please note that changes you make to policies and roles do not involve any charges.

{{%/notice%}}

1. Using the root IAM user, select the ec2-admin-team-alpha role in the [IAM console](https://console.aws.amazon.com/iam/) and select **Delete role**

2. For each policy you created, select the radio button, then select the Policy Action drop-down menu and select Delete .
The policies created are:
- ec2-create-tags
- ec2-create-tags-existing
- ec2-list-read
- ec2-manage-instances
- ec2-run-instances

### References & Useful Resources
-[AWS Identity and Access Management User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
- [IAM Use Cases and Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPracticesAndUseCases.html)
- [Become an IAM Policy Expert in 60 Minutes or Less](https://youtu.be/YQsK4MtsELU)
- [Actions, Resources, and Condition Keys for Identity and Access Management access](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_identityandaccessmanagement.html)