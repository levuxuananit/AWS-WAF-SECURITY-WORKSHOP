---
title : "Create IAM Policy"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1.1 </b> "
---
### Create a Permissions Boundary Policy
This policy will act as a permissions boundary when developers create their own IAM roles, using the previously granted permissions. In this lab, you will configure the policy to only allow access to the EC2 and Lambda services in two specific regions:
- us-east-1 (North Virginia)
- us-west-1 (North California)
- You are free to change these regions to your preferred regions or add/remove others as needed.

{{%notice note%}}
**EC2** and **Lambda** are services that may require additional supporting permissions to fully function. So if you plan to reuse this policy after completing the lab, make sure to add the necessary permissions based on your actual use case.
{{%/notice%}}

1. Sign in to the AWS Management Console as an IAM user with MFA enabled to assume roles in your AWS account and open the [IAM console](https://console.aws.amazon.com/iam/).

2. In the navigation pane, select **Policies** and then select **Create policy**.
![create_policy](/images/3.connect/3.1/1_create_policy.png)

3. On the Create Policy page, select the **JSON tab**.
![json](/images/3.connect/3.1/2_json.png)

4. Replace the beginning of the policy already in the editor with the policy below.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "EC2RestrictRegion",
            "Effect": "Allow",
            "Action": "ec2:*",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:RequestedRegion": [
                        "us-east-1",
                        "us-west-1"
                    ]
                }
            }
        },
        {
            "Sid": "LambdaRestrictRegion",
            "Effect": "Allow",
            "Action": "lambda:*",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:RequestedRegion": [
                        "us-east-1",
                        "us-west-1"
                    ]
                }
            }
        }
    ]
}
```
5. Select Next.

6. Enter the name of the ```restricted-region-boundary``` and any description to help you identify the policy, verify the summary, and then select **Create policy**.
![create_policy_restricted_region_boundary](/images/3.connect/3.1/3_create_policy_restricted_region_boundary.png)

### Create IAM Policy with name prefix and permission boundary for developer role
The following policy will be attached to the developer role and will allow the developer to create policies and roles with the name prefix **app1** and only if the permission boundary is restricted.
You will need to change this account id ``8**********7`` to your account number. You can find your account id by navigating to [accout settings](https://console.aws.amazon.com/billing/home?#/account) in the console. Prefixing a policy name helps you differentiate different groups or different applications running in the same AWS account. It keeps your resources neat, IAM policies are also considered resources. Follow these steps to create this cool policy:

1. Create a policy and name it ```creatorole-restrict-region-boundary```.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "CreatePolicy",
            "Effect": "Allow",
            "Action": [
                "iam:CreatePolicy",
                "iam:CreatePolicyVersion",
                "iam:DeletePolicyVersion"
            ],
            "Resource": "arn:aws:iam::8**********7:policy/app1*"
        },
        {
            "Sid": "CreateRole",
            "Effect": "Allow",
            "Action": [
                "iam:CreateRole"
            ],
            "Resource": "arn:aws:iam::8**********7:role/app1*",
            "Condition": {
                "StringEquals": {
                    "iam:PermissionsBoundary": "arn:aws:iam::8**********7:policy/restrict-region-boundary"
                }
            }
        },
        {
            "Sid": "AttachDetachRolePolicy",
            "Effect": "Allow",
            "Action": [
                "iam:DetachRolePolicy",
                "iam:AttachRolePolicy"
            ],
            "Resource": "arn:aws:iam::8**********7:role/app1*",
            "Condition": {
                "ArnEquals": {
                    "iam:PolicyARN": [
                        "arn:aws:iam::8**********7:policy/*",
                        "arn:aws:iam::aws:policy/*"
                    ]
                }
            }
        }      
    ]
}
```
### Create a Developer IAM Console Access Policy
The policy below enables IAM service actions to be listed and read so you can see what you have created using the console. Note that this is not required if you are just creating roles and policies, or if you are using the Command Line Interface (CLI) or CloudFormation.

1. Create a policy and name it ```iam-restricted-list-read```.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Get",
            "Effect": "Allow",
            "Action": [
                "iam:ListPolicies",
                "iam:GetRole",
                "iam:GetPolicyVersion",
                "iam:ListRoleTags",
                "iam:GetPolicy",
                "iam:ListPolicyVersions",
                "iam:ListAttachedRolePolicies",
                "iam:ListRoles",
                "iam:ListRolePolicies",
                "iam:GetRolePolicy"
            ],
            "Resource": "*"
        }
    ]
}
```