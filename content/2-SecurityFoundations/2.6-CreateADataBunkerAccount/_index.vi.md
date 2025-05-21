---
title : "Tạo tài khoản Data Bunker"
date : "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 2.6 </b> "
---
### Giới thiệu
Trong phòng workshop này, bạn sẽ tạo một **bunker dữ liệu** an toàn. **Bunker dữ liệu** là một tài khoản an toàn sẽ lưu trữ dữ liệu bảo mật quan trọng ở một vị trí an toàn. Đảm bảo rằng chỉ những thành viên trong nhóm bảo mật của bạn mới có quyền truy cập vào tài khoản này. Trong phòng thí nghiệm này, bạn sẽ tạo một tài khoản bảo mật mới, tạo một thùng S3 an toàn trong tài khoản đó rồi bật CloudTrail để tổ chức của chúng tôi gửi các nhật ký này đến thùng trong tài khoản dữ liệu an toàn. Bạn cũng có thể muốn cân nhắc đến những dữ liệu khác mà bạn cần trong đó như các bản sao lưu an toàn.
![schema_data_bunker_account](/images/2.SecurityFoundations/13_schema_data_bunker_account.png)
{{%notice note%}}
Thực hành tốt nhất là sử dụng AWS Control Tower để thiết lập vùng hạ cánh Well-Architected của bạn. Các bước trong phòng thí nghiệm này bao gồm những gì đã được cấu hình cho [Tài khoản lưu trữ nhật ký Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/how-control-tower-works.html#what-shared).
{{%/notice%}}

### Tạo tài khoản ghi nhật ký từ tài khoản quản lý tổ chức
1. Đăng nhập vào tài khoản quản lý của Tổ chức AWS (AWS oganizations) của bạn.
![aws_organizations](/images/2.SecurityFoundations/14_aws_organizations.png)

2. Tại trang chủ của **AWS Organizations**, chọn **Add An AWS Account**.
![alt text](/images/2.SecurityFoundations/16_aws_account.png)

3. Điền thông tin tài khoản mới
- Tên tài khoản AWS: ```AccountSecurityLogs```
- Địa chỉ email của chủ sở hữu tài khoản: ```example@gmail.com```
- Tên IAM role(mặc định): ```OrganizationAccountAccessRole```
![add_aws_oraganizations](/images/2.SecurityFoundations/17_add_aws_oraganizations.png)

{{%notice note%}}
(Tùy chọn) Nếu vai trò của bạn không có quyền đảm nhận bất kỳ vai trò nào, bạn cũng sẽ phải thêm chính sách IAM. Chính sách quản trị viên AWS có chính sách này theo mặc định, nếu không, hãy làm theo các bước trong Tài liệu về Tổ chức AWS để cấp quyền truy cập vào vai trò.
Hãy cân nhắc áp dụng các biện pháp thực hành tốt nhất làm cơ sở như khóa khóa truy cập người dùng gốc của tài khoản AWS của bạn và sử dụng xác thực đa yếu tố 
{{%/notice%}}

4. Hoàn thành thêm tài khoản và chờ yêu cầu được xử lý.
![request_to_create_accountt](/images/2.SecurityFoundations/18_request_to_create_account.png)

5. Điều hướng đến Cài đặt và ghi lại ID tổ chức của bạn.
![setting_aws_organization](/images/2.SecurityFoundations/15_setting_aws_organizations.png)

 ### Tạo khóa để mã hóa nhật ký CloudTrail
1. Đăng nhập vào tài khoản ghi nhật ký (AccountSecurityLogs) của tổ chức của bạn.
   
2. Điều hướng đến **AWS Key Management Service (KMS)**, chọn **Create a key**.
![create_key](/images/2.SecurityFoundations/19_create_key.png)
   
3. Tại phần cấu hình khóa, chọn **Symmetric** và chọn **Next**.
![config_key](/images/2.SecurityFoundations/20_config_key.png)

4. Nhập Biệt danh cho khóa của bạn, ví dụ:
- Alias: ```CloudTrailKey```
- Description: ```Key to encrypt CloudTrail logs```
![add_labels](/images/2.SecurityFoundations/21_add_labels.png)

5. Hoàn thành tạo **khóa để mã hóa nhật ký CloudTrail**
![complete_to_create_a_key](/images/2.SecurityFoundations/22_complete_to_create_a_key.png)

### Tạo thùng cho nhật ký CloudTrail
1. Trong tài khoản ghi nhật ký (AccountSecurityLogs) còn trong tài khoản ghi nhật ký của tổ chức bạn.

2. Điều hướng đến Amazon S3, chọn **Create bucket**
![amazon_s3](/images/2.SecurityFoundations/23_amazon_s3.png)

3. Thực hiện tạo bucket theo hướng dẫn sau:
- Nhập tên Bucket, ví dụ: ```securelogbucket2025```
- Chọn **ACLs disabled**
- Chọn, cho phép **Chặn mọi quyền truy cập công khai**
- Giữ các cấu hình mặc định
- Cuối cùng, chọn **Tạo thùng**
![setup_bucket_name](/images/2.SecurityFoundations/24_setup_bucket_name.png)

4. Chọn bucket mà vừa tạo.
![choose_bucket](/images/2.SecurityFoundations/25_choose_bucket.png)

5. Sau đó chọn tab **Permissions**. 
![edit_bucket_policy](/images/2.SecurityFoundations/26_edit_bucket_policy.png)

6. thay thế Bucket Policy bằng nội dung sau:
- [bucket] = tên bucket của bạn (ví dụ: **securelogbucket2025**)
- [organization id] = id tổ chức được nhận dạng ở bước 1.
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
- Sau khi thay đổi, ấn **Lưu thay đổi**
![paste_policy](/images/2.SecurityFoundations/27_paste_policy.png)

7. Tạo bucket thành công.
![alt text](/images/2.SecurityFoundations/28_successfully_edited_bucket_policy.png)

### Đảm bảo quyền truy cập chỉ đọc của tài khoản ghi nhật ký
Thực hiện theo các bước sau để sẽ ngăn **OrganizationAccountAccessRole** thực hiện thêm các thay đổi cho tài khoản này. 

1. Điều hướng đến IAM và chọn **Role**. Chọn vai trò truy cập tài khoản tổ chức cho tổ chức của bạn. Mặc định là ```OrganizationAccountAccessRole```
![choose_role](/images/2.SecurityFoundations/29_choose_role.png)

2. Chọn **Add Polices**
![attach_policy](/images/2.SecurityFoundations/30_attach_policy.png)

3. Đính kèm Chính sách **ReadOnlyAccess** do AWS quản lý.
![add_permission](/images/2.SecurityFoundations/31_add_permission.png)

4. Quay lại **OrganizationAccountAccessRole** và nhấn X để xóa chính sách **AdministratorAccess**
![delete_police](/images/2.SecurityFoundations/32_delete_police.png)

### Bật CloudTrail từ tài khoản quản lý
1. Chuyển lại tài khoản quản lý.

2. Điều hướng đến CloudTrail. Tại thanh menu bên trái, chọn **Trail**. Sau đó, chọn nút **Create trail**
![create_trail](/images/2.SecurityFoundations/33_create_trail.png)

3. Nhập thông tin theo hướng dẫn sau:
- Tên trial là ```OrganizationTrail```
- Chọn **Sử dụng S3 bucket có sẵn** nhập tên thùng của thùng đã tạo ở bước 3
- Trong AWS KMS alias , thêm tên của KMS alias đã tạo ở bước 2.
![trail_detail](/images/2.SecurityFoundations/34_trail_detail.png)

4. Tạo trail thành công
![compelete_create_trail](/images/2.SecurityFoundations/35_compelete_create_trail.png) 
