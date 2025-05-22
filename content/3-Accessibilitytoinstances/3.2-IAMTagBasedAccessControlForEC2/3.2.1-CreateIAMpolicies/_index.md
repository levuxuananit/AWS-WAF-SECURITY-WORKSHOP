---
title : "Create IAM policies"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.2.1 </b> "
---
### Create a policy called ec2-list-read
This policy allows read-only with a region condition. The only service actions we will allow are EC2, note that you will typically require additional supporting actions such as Elastic Load Balancing if you want to reuse this policy after this exercise, depending on your requirements.

1. Sign in to the AWS Management Console as an MFA-enabled IAM user so you can assume roles in your AWS account and open the [IAM console](https://console.aws.amazon.com/iam/). If you need to enable MFA, follow the IAM User Guide. You will need to sign out and sign back in with MFA for your session to have MFA enabled.

2. In the navigation pane, select **Policies** and then select **Create Policy**.
![create_policy](/images/3.connect/3.1/11_create_policy.png)

3. On the Create Policy page, select the JSON tab.

![json](/images/3.connect/3.1/12_json.png)

4. Replace the beginning of the policy already in the editor with the policy below.

5. Select Next.

6. Enter a Policy name of ```ec2-list-read``` and any description to help you identify the policy, verify the summary, and select **Create Policy**.

![ec2-list-read](/images/3.connect/3.1/13_ec2-list-read.png)

### Create a policy named ec2-create-tags
This policy allows tags to be created for EC2, provided the action is [RunInstances](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RunInstances.html), which is launching an instance.

1. Create a managed policy using the JSON policy below and the name ```ec2-create-tags```.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ec2createtags",
            "Effect": "Allow",
            "Action": "ec2:CreateTags",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "ec2:CreateAction": "RunInstances"
                }
            }
        }
    ]
}
```

### Create a policy named ec2-create-tags-existing
This policy only allows EC2 tags to be created (and overwritten) if the resource is already tagged with **Team / Alpha**.

1. Create a policy managed using the JSON policy below and named ```ec2-create-tags-existing```.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ec2createtagsexisting",
            "Effect": "Allow",
            "Action": "ec2:CreateTags",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "ec2:ResourceTag/Team": "Alpha"
                },
                "ForAllValues:StringEquals": {
                    "aws:TagKeys": [
                        "Team",
                        "Name"
                    ]
                },
                "StringEqualsIfExists": {
                    "aws:RequestTag/Team": "Alpha"
                }
            }
        }
    ]
}
```
### Create a policy named ec2-run-instances
The first part of this policy allows instances to be launched, only if the conditions of the specific region and tag key are matched. The second part allows other resources to be created at the time of instance launch with the conditions of the region.

1. Create a managed policy using the JSON policy below and the name ```ec2-run-instances```.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ec2runinstances",
            "Effect": "Allow",
            "Action": "ec2:RunInstances",
            "Resource": "arn:aws:ec2:*:*:instance/*",
            "Condition": {
                "StringEquals": {
                    "aws:RequestedRegion": [
                        "us-east-1",
                        "us-west-1"
                    ],
                    "aws:RequestTag/Team": "Alpha"
                },
                "ForAllValues:StringEquals": {
                    "aws:TagKeys": [
                        "Name",
                        "Team"
                    ]
                }
            }
        },
        {
            "Sid": "ec2runinstancesother",
            "Effect": "Allow",
            "Action": "ec2:RunInstances",
            "Resource": [
                "arn:aws:ec2:*:*:subnet/*",
                "arn:aws:ec2:*:*:key-pair/*",
                "arn:aws:ec2:*::snapshot/*",
                "arn:aws:ec2:*:*:launch-template/*",
                "arn:aws:ec2:*:*:volume/*",
                "arn:aws:ec2:*:*:security-group/*",
                "arn:aws:ec2:*:*:placement-group/*",
                "arn:aws:ec2:*:*:network-interface/*",
                "arn:aws:ec2:*::image/*"
            ],
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

### Create a policy named ec2-manage-instances
This policy allows instances to be restarted, terminated, started, and stopped, provided that the **Group** is **Alpha** and the region.

1. Create a managed policy using the JSON policy below and the name ```ec2-manage-instances```.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ec2manageinstances",
            "Effect": "Allow",
            "Action": [
                "ec2:RebootInstances",
                "ec2:TerminateInstances",
                "ec2:StartInstances",
                "ec2:StopInstances"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "ec2:ResourceTag/Team": "Alpha",
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