---
title : "Tạo chính sách IAM"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1.1 </b> "
---
### Tạo chính sách cho ranh giới quyền
Chính sách này sẽ đóng vai trò làm ranh giới quyền hạn (permissions boundary) khi nhà phát triển tạo các vai trò IAM riêng của họ, sử dụng các quyền được cấp trước đó. Trong phòng thí nghiệm này, bạn sẽ cấu hình chính sách để chỉ cho phép truy cập dịch vụ EC2 và Lambda trong hai vùng cụ thể là:
- us-east-1 (North Virginia)
- us-west-1 (North California)
- Bạn hoàn toàn có thể thay đổi các vùng này thành những vùng yêu thích của mình hoặc thêm / xóa vùng khác tùy theo nhu cầu.

{{%notice note%}}
**EC2** và **Lambda** là những dịch vụ có thể cần thêm các quyền hỗ trợ để hoạt động đầy đủ. Vì vậy, nếu bạn định sử dụng lại chính sách này sau khi hoàn thành lab, hãy đảm bảo bổ sung các quyền cần thiết tùy theo mục đích sử dụng thực tế.
{{%/notice%}}

1. Đăng nhập vào AWS Management Console với tư cách là người dùng IAM đã bật MFA để có thể đảm nhận vai trò trong tài khoản AWS của bạn và mở [bảng điều khiển IAM](https://console.aws.amazon.com/iam/).

2. Trong ngăn điều hướng, chọn **Policies** rồi chọn **Create policy**.
![create_policy](/images/3.connect/3.1/1_create_policy.png)

3. Trên trang Tạo chính sách, chọn **tab JSON**.
![json](/images/3.connect/3.1/2_json.png)

4. Thay thế phần bắt đầu của chính sách đã có trong trình soạn thảo bằng chính sách bên dưới.
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

5. Chọn Tiếp theo.

6. Nhập tên của ```restricted-region-boundary``` và bất kỳ mô tả nào để giúp bạn xác định chính sách, xác minh tóm tắt rồi chọn **Create policy**.
![create_policy_restricted_region_boundary](/images/3.connect/3.1/3_create_policy_restricted_region_boundary.png)

### Tạo Chính sách IAM với tiền tố tên và ranh giới quyền hạn cho vai trò nhà phát triển
Chính sách dưới đây sẽ được đính kèm vào vai trò nhà phát triển và sẽ cho phép nhà phát triển tạo chính sách và vai trò với tiền tố tên là **app1** và chỉ khi ranh giới quyền hạn bị hạn chế.
Bạn sẽ cần thay đổi id tài khoản này ``8**********7`` thành số tài khoản của bạn. Bạn có thể tìm id tài khoản của mình bằng cách điều hướng đến [cài đặt accout](https://console.aws.amazon.com/billing/home?#/account) trong bảng điều khiển. Việc đặt tên tiền tố cho chính sách giúp bạn phân biệt các nhóm khác nhau hoặc các ứng dụng khác nhau chạy trong cùng một tài khoản AWS. Điều đó giúp cho tài nguyên của bạn trông gọn gàng, chính sách IAM cũng được coi là tài nguyên. Hãy thực hiện các bước sau để tạo chính sách thú vị này:

1. Tạo chính sách và tên đặt tên là ```createrole-restrict-region-boundary```.
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

### Tạo chính sách truy cập bảng điều khiển IAM của nhà phát triển
Chính sách dưới đây cho phép liệt kê và đọc các hành động dịch vụ IAM để bạn có thể xem những gì bạn đã tạo bằng bảng điều khiển. Lưu ý rằng đây không phải là yêu cầu nếu bạn chỉ muốn tạo vai trò và chính sách hoặc nếu bạn đang sử dụng Giao diện dòng lệnh (CLI) hoặc CloudFormation.

1. Tạo chính sách và tên ```iam-restricted-list-read```.
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