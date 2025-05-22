---
title : "Create Role"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2.2 </b> "
---
### Create an EC2 administrator role and attach the previously created managed policies.

1. Sign in to the AWS Management Console as an MFA-enabled IAM user to be able to assume roles in your AWS account and open the [IAM console](https://console.aws.amazon.com/iam/).

2. In the navigation pane, select Roles and then select Create Role.
![create_role](/images/3.connect/3.1/14_create_role.png)

3. Select the AWS account, then select Other AWS Account and enter the account ID you are using and check Require MFA, then select Next. Enforce MFA here as this is a best practice.
![select_trusted_entity](/images/3.connect/3.1/15_select_trusted_entity.png)

4. In the search field, start typing ec2- then check the box next to the policies you just created:
- ec2-create-tags
- ec2-create-tags-existing
- ec2-list-read
- ec2-manage-instances
- ec2-run-instances
![add_permission](/images/3.connect/3.1/16_add_permission.png)

5. Then, enter the name ```ec2-admin-team-alpha``` for **Role Name**.

6. Test the role you created by selecting **ec2-admin-team-alpha** from the list. Make a note of both the role ARN and the link to the dashboard.

7. The role is now created and ready for testing!