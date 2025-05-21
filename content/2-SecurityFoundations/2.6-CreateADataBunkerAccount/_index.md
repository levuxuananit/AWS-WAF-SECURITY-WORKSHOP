---
title : "Create a Data Bunker Account"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 2.6 </b> "
---
### Introduction
In this workshop, you will create a secure **data bunker**. A **data bunker** is a secure account that stores important security data in a secure location. Make sure that only members of your security team have access to this account. In this lab, you will create a new security account, create a secure S3 bucket in that account, and then enable CloudTrail so that our organization sends these logs to the bucket in the secure data account. You may also want to consider what other data you need in there, such as secure backups.
![schema_data_bunker_account](/images/2.SecurityFoundations/13_schema_data_bunker_account.png)
{{%notice note%}}
A best practice is to use AWS Control Tower to set up your Well-Architected landing zone. The steps in this lab cover what was configured for the [Control Tower Log Storage Account](https://docs.aws.amazon.com/controltower/latest/userguide/how-control-tower-works.html#what-shared).
{{%/notice%}}

### Create a Logging Account from an Organization Management Account
1. Sign in to your AWS Organizations management account.
![aws_organizations](/images/2.SecurityFoundations/14_aws_organizations.png)

2. On the **AWS Organizations** home page, select **Add An AWS Account**.
![alt text](/images/2.SecurityFoundations/16_aws_account.png)

3. Fill in the new account information
- AWS account name: ```AccountSecurityLogs```
- Account owner email address: ```example@gmail.com```
- IAM role name (default): ```OrganizationAccountAccessRole```
![add_aws_oraganizations](/images/2.SecurityFoundations/17_add_aws_oraganizations.png)

{{%notice note%}}
(Optional) If your role does not have permissions to assume any roles, you will also need to add an IAM policy. AWS Administrator policies have this policy by default, otherwise follow the steps in the AWS Organizations documentation to grant access to the role.
Consider implementing best practices as a baseline, such as locking down your AWS account's root user access key and using multi-factor authentication
{{%/notice%}}

4. Complete adding an account and wait for the request to be processed.
![request_to_create_accountt](/images/2.SecurityFoundations/18_request_to_create_account.png)

5. Navigate to Settings and note your Organization ID.
![setting_aws_organization](/images/2.SecurityFoundations/15_setting_aws_organizations.png)

### Create a key to encrypt CloudTrail logs

1. Log in to your organization's logging account (AccountSecurityLogs).

2. Navigate to **AWS Key Management Service (KMS)**, select **Create a key**.

![create_key](/images/2.SecurityFoundations/19_create_key.png)

3. In the key configuration section, select **Symmetric** and select **Next**.

![config_key](/images/2.SecurityFoundations/20_config_key.png)

4. Enter an Alias ​​for your key, for example:

- Alias: ```CloudTrailKey```
- Description: ```Key to encrypt CloudTrail logs```
![add_labels](/images/2.SecurityFoundations/21_add_labels.png)

5. Complete creating **a key to encrypt CloudTrail logs**
![complete_to_create_a_key](/images/2.SecurityFoundations/22_complete_to_create_a_key.png)

### Create a bucket for CloudTrail logs

1. In the logging account (AccountSecurityLogs) that is still in your organization's logging account.

2. Navigate to Amazon S3, select **Create bucket**

![amazon_s3](/images/2.SecurityFoundations/23_amazon_s3.png)

3. Create a bucket as follows:

- Enter a Bucket name, for example: ```securelogbucket2025```
- Select **ACLs disabled**
- Select, allow **Block all public access**
- Keep the default configuration
- Finally, select **Create bucket**
![setup_bucket_name](/images/2.SecurityFoundations/24_setup_bucket_name.png)

4. Select the bucket you just created.
![choose_bucket](/images/2.SecurityFoundations/25_choose_bucket.png)

5. Then select the **Permissions** tab.
![edit_bucket_policy](/images/2.SecurityFoundations/26_edit_bucket_policy.png)

6. Replace Bucket Policy with the following content:
- [bucket] = your bucket name (e.g. **securelogbucket2025**)
- [organization id] = the organization id identified in step 1.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AWSCloudTrailAclCheck20150319",
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudtrail.amazonaws.com"
            },
            "Action": "s3:GetBucketAcl",
            "Resource": "arn:aws:s3:::[bucket]"
        },
        {
            "Sid": "AWSCloudTrailWrite20150319",
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudtrail.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::[bucket]/AWSLogs/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        },
        {
            "Sid": "AWSCloudTrailWrite201503109",
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudtrail.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::[bucket]/AWSLogs/[organization id]/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        }
    ]
}
```
- After changing, press **Save changes**

![paste_policy](/images/2.SecurityFoundations/27_paste_policy.png)

7. Bucket created successfully.
![alt text](/images/2.SecurityFoundations/28_successfully_edited_bucket_policy.png)

### Ensure Read-Only Access for the Logging Account
Follow these steps to prevent **OrganizationAccountAccessRole** from making further changes to this account.

1. Navigate to IAM and select **Role**. Select the organization account access role for your organization. The default is ```OrganizationAccountAccessRole```
![choose_role](/images/2.SecurityFoundations/29_choose_role.png)

2. Select **Add Polices**
![attach_policy](/images/2.SecurityFoundations/30_attach_policy.png)

3. Attach the AWS-managed **ReadOnlyAccess** Policy.

![add_permission](/images/2.SecurityFoundations/31_add_permission.png)

4. Go back to **OrganizationAccountAccessRole** and press X to delete the **AdministratorAccess** policy
![delete_police](/images/2.SecurityFoundations/32_delete_police.png)

### Enable CloudTrail from the management account

1. Switch back to the management account.

2. Navigate to CloudTrail. In the left menu bar, select **Trail**. Then, select the **Create trail** button
![create_trail](/images/2.SecurityFoundations/33_create_trail.png)

3. Enter the information according to the following instructions:
- The trial name is ```OrganizationTrail```
- Select **Use existing S3 bucket** and enter the bucket name of the bucket created in step 3
- In AWS KMS alias, add the name of the KMS alias created in step 2.
![trail_detail](/images/2.SecurityFoundations/34_trail_detail.png)

4. Trail creation successful
![compelete_create_trail](/images/2.SecurityFoundations/35_compelete_create_trail.png)
