---
title : "Tạo chính sách IAM"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.2.1 </b> "
---
### Tạo chính sách có tên ec2-list-read
Chính sách này cho phép quyền chỉ đọc với điều kiện vùng. Các hành động dịch vụ duy nhất mà chúng tôi sẽ cho phép là EC2, lưu ý rằng bạn thường yêu cầu các hành động hỗ trợ bổ sung như Elastic Load Balancing nếu bạn muốn sử dụng lại chính sách này sau bài thực hành này, tùy thuộc vào yêu cầu của bạn.

1. Đăng nhập vào AWS Management Console với tư cách là người dùng IAM đã bật MFA để có thể đảm nhận vai trò trong tài khoản AWS của bạn và mở [bảng điều khiển IAM](https://console.aws.amazon.com/iam/). Nếu bạn cần bật MFA, hãy làm theo Hướng dẫn sử dụng IAM. Bạn sẽ cần phải đăng xuất và đăng nhập lại bằng MFA để phiên của bạn có MFA được kích hoạt.

2. Trong ngăn điều hướng, chọn **Policies** rồi chọn **Create Policy**.
![create_policy](/images/3.connect/3.1/11_create_policy.png)

3. Trên trang Tạo chính sách, chọn tab JSON.
![json](/images/3.connect/3.1/12_json.png)

4. Thay thế phần bắt đầu của chính sách đã có trong trình soạn thảo bằng chính sách bên dưới.

5. Chọn Tiếp theo.

6. Nhập tên Chính sách của ```ec2-list-read``` và bất kỳ mô tả nào để giúp bạn xác định chính sách, xác minh tóm tắt rồi chọn **Tạo chính sách**.
![ec2-list-read](/images/3.connect/3.1/13_ec2-list-read.png)

### Tạo chính sách có tên ec2-create-tags
Chính sách này cho phép tạo thẻ cho EC2, với điều kiện của hành động là [RunInstances](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RunInstances.html), đang khởi chạy một phiên bản.

1. Tạo chính sách được quản lý bằng chính sách JSON bên dưới và tên ```ec2-create-tags```.
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

### Tạo chính sách có tên ec2-create-tags-existing
Chính sách này chỉ cho phép tạo (và ghi đè) thẻ EC2 nếu tài nguyên đã được gắn thẻ **Team / Alpha**.

1. Tạo chính sách được quản lý bằng chính sách JSON bên dưới và tên là ```ec2-create-tags-existing```.
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

### Tạo chính sách có tên ec2-run-instances
Phần đầu tiên của chính sách này cho phép khởi chạy các phiên bản, chỉ khi các điều kiện của vùng và khóa thẻ cụ thể được khớp. Phần thứ hai cho phép tạo các tài nguyên khác tại thời điểm khởi chạy phiên bản với điều kiện vùng.

1. Tạo chính sách được quản lý bằng cách sử dụng chính sách JSON bên dưới và tên ```ec2-run-instances```.
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
### Tạo chính sách có tên ec2-manage-instances
Chính sách này cho phép khởi động lại, chấm dứt, bắt đầu và dừng các phiên bản, với điều kiện là **Nhóm** chính là **Alpha** và khu vực.

1. Tạo chính sách được quản lý bằng chính sách JSON bên dưới và tên ```ec2-manage-instances```.
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
