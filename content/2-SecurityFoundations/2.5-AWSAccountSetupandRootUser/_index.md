---
title : "AWS Account Setup and Root User"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.5 </b> "
---
### Check AWS Account Authentication Reports
You should check your security configuration in the following situations:
- You should check periodically or in the following cases:
- Periodically as a good security practice.
- There is a change in personnel (e.g. someone leaves).
- Stop using certain AWS services → remove permissions that are no longer needed.
- Add/remove software such as EC2, OpsWorks, CloudFormation, etc.
- Suspect unauthorized access to the account.

When reviewing your account security configuration, remember to:
- Double-check: Don't skip any section, no matter how little you use it.
- Don't guess: If you're not sure about a policy or role, research it thoroughly
- Keep it simple: Use IAM groups, consistent names, and clear policies for easy management.
You can download the credential information report from the AWS Management Console as a CSV file. Note: It may take up to 4 hours for changes to be reflected.
- More information can be found at https://docs.aws.amazon.com/general/latest/gr/aws-security-audit-guide.html

You can use the **AWS Management Console** to download the credential report as a comma-separated values ​​(CSV) file. Please note that it may take up to 4 hours for the credential report to reflect changes. To download the credential report using the AWS Management Console:
1. Sign in to the **AWS Management Console** and open the [IAM console](https://console.aws.amazon.com/iam/).
In the navigation pane, select Credential Report.
2. Select Download Report .
![download-credentials-report](/images/2.SecurityFoundations/download-credentials-report.png)

{{%notice note%}}
You can find more information about the report at https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html
{{%/notice%}}

### MFA Virtual Device
You can use the IAM service in the **AWS Management Console** to configure and enable a virtual MFA device for the root user. MFA is an intermediary application, usually a personal phone, that authenticates whether the person logging in is the root user. Only the root user can manage the MFA device for themselves. You need to log in with the root user's credentials, you cannot use another IAM account to change this setting.

If you lose or cannot use the MFA device, you can still log in by verifying your identity via:
- The email registered with your AWS account.
- The phone number registered.

{{%notice note%}}
So, before enabling MFA, make sure that: The email and phone number in your AWS account are correct and that you have access.
{{%/notice%}}

To learn about signing in with alternative authentication factors, see [What happens if your MFA device is lost or broken?](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_lost-or-broken.html). To disable this feature, contact [AWS Support](https://console.aws.amazon.com/support/home#/).

### Enable a Virtual MFA Device for a Root User Account in AWS
1. Use your AWS account email address and password to sign in as the root user of your AWS account to the [IAM console](https://console.aws.amazon.com/iam/).

2. Do one of the following:
- Option 1: Select Console, and in the Quick Links pane, select **My Security Credentials**.
- Option 2: On the right side of the navigation bar, select your account name and select **Security Credentials**. If necessary, select **Continue to Security Credentials**. Then, expand the **Multi-Factor Authentication (MFA**) section on the page.

![security_credentials](/images/2.SecurityFoundations/2_SC.png)

3. Next, select "Assign MFA device" to connect your MFA device

[assign_MFA](/images/2.SecurityFoundations/3_assign_MFA.png)

4. Next, select the MFA device type:
- Name the device: ```MyMFADevice```
- Select: **Authenticator app**
![select_device](/images/2.SecurityFoundations/4_select_device.png)
The options include:
- **Virtual MFA device**: Use an authenticator app like Google Authenticator
- **Hardware TOTP token**: Use a dedicated hardware device
- **Security key**: Use a FIDO security key

1. Finally, install the device MFA:
- Select **Show QR code**
- Enter 2 consecutive MFA codes below:
  - Enter the code from your virtual app.
  - Wait 30 seconds and enter the second code.
![setup_device](/images/2.SecurityFoundations/5_setup_device.png)

### Configure Alternate Contact Accounts
Alternate contacts allow AWS to contact someone else about account-related issues, even when you are not available.

1. First, sign in to AWS as the root user and open the AWS account settings page

![setup_account](/images/2.SecurityFoundations/6_setup_account.png)

2. Next, navigate to the alternate contacts configuration section.

![setup_account](/images/2.SecurityFoundations/7_alternate_contacts.png.png)

3. Next, enter contact information for billing, operations, and security.

4. Finally, select **Update**.

### Delete your AWS account's root user access key
The access key (including the Access Key ID and Secret Access Key) is used to make requests to AWS programmatically (e.g., using the AWS CLI or SDK). However, never use the root user's access key, as it has full access rights to all services and resources, including billing information. You cannot limit permissions when using the root user's access key, so it is very risky in terms of security.

**Safe access method**:
- Do not create access keys for the root user unless absolutely necessary.

- Sign in to the AWS Management Console with the root user's email and password.

- Create an IAM user with administrative privileges.

- Use that IAM user to create access keys if needed.

- Delete the root user's access key as soon as possible to protect the account.
- Rotate (replace) or delete the key in the Security Credentials section of the AWS Management Console.

- **Note**: You need to sign in with your root user credentials (email and password) to do this.

1. On the right side of the navigation bar, select your account name and select **Security Credentials**
![security_credentials](/images/2.SecurityFoundations/2_SC.png)

2. Delete the root user access key.
![delete_accesske](/images/2.SecurityFoundations/8_delete_accesskey.png)

{{%notice note%}}
Never share your AWS account password or access key with anyone.
{{%/notice%}}

### Periodically change your AWS account root user password
1. Use your AWS account email address and password to sign in to the AWS Management Console as the root user.
{{%notice note%}}
If you previously signed in to the console using IAM user credentials, your browser may remember this preference and open a sign-in page specific to your account. You cannot use the IAM user sign-in page to sign in with your AWS account root user credentials. If you see the IAM user sign-in page, click Sign in with root account credentials near the bottom of the page to return to the main sign-in page. From there, you can enter your AWS account email address and password.
{{%/notice%}}

2. In the upper-right corner of the console, select your account name or number, and then select **Account**.

![security_credentials](/images/2.SecurityFoundations/2_SC.png)

3. In the Account Settings pane, select **Actions**, select **Edit Email Address and Password**.

![update_email_password](/images/2.SecurityFoundations/9_update_email_password.png)

4. Prompt for MFA code to navigate to the email address and password settings page, select **Edit**, then enter current password, new password, and confirm new password (same as email address)

[account_detai](/images/2.SecurityFoundations/10_account_detail.png)

5. Select **Save Changes** to save your new password.

{{%notice note%}}
Choose a strong password. Although you can set an account password policy for IAM users, it does not apply to your AWS account root user. AWS requires that your password meet the following conditions: - Be at least 8 characters and at most 128 characters long. - Include at least three of the following character types: uppercase, lowercase, numbers, and ! @ # $ % ^ & * () <> [] {} | _ + - = symbols. - Not the same as your AWS account name or email address.

{{%/notice%}}

**To protect your password, it is important to follow these best practices**:
- Change your password periodically and keep it secret, because anyone who knows your password can access your account.

- Use a different password on AWS than you use on other sites.
- Avoid using easy-to-guess passwords, like secret, password, amazon or 123456, things like dictionary words, your name, email address or other personal information that can be easily obtained.

### Configure Strong Password Policies for Your Users
1. Sign in to the AWS Management Console and [IAM console](https://console.aws.amazon.com/iam/).
2. In the navigation pane, select Account Settings.
3. In the Password Policies pane, select Edit in the upper-right corner.
![password_policy](/images/2.SecurityFoundations/11_password_policy.png)
4. In the Edit password policy pane, you can select the default IAM or create your own Custom password policy.
![password_policy](/images/2.SecurityFoundations/12_edit_pasword_policy.png)
5. Select **Save Changes** to save the password policy.

