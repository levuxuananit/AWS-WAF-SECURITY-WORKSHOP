---
title : "Test Role"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3.2.3 </b> "
---
### Assume the ec2-admin-team-alpha role
You will now use your existing MFA-enabled IAM user to assume the new ec2-admin-team-alpha role.

1. Sign in to the AWS Management Console as an MFA-enabled IAM user. https://console.aws.amazon.com .

2. In the console, select your username from the navigation bar in the upper right corner. It usually looks like this: username@account_ID_number_or_alias, then select Switch Roles . Alternatively, you can paste the link you wrote down earlier into your browser.

3. On the Switch Roles page, enter your account ID number in the Account field and the name of the ec2-admin-team-alpha role you created in the previous step in the Role field. (Optional) Enter the text you want to display in the navigation bar instead of your username when this role is active. A name is suggested, based on your account and role information, but you can change it to whatever makes sense to you. You can also choose a color to highlight the display name.

4. Select Switch Roles . If this is the first time you have selected this option, a page will appear with more information. After reading, select Switch Roles . If you clear your browser cookies, this page may appear again.

![switch_role](../../../../static/images/3.connect/3.1/17_switch_role.png)

5. The display name and color will replace your username in the navigation bar, and you can begin using the permissions that role grants you instead of the permissions you have as an IAM user.

{{%notice note%}}
The last few roles you used will appear in the menu. The next time you need to switch to one of those roles, just select the role you want. You will only need to enter the account and role information manually if the role is not shown in the Identity menu.
{{%/notice%}}