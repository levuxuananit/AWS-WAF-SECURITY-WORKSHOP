---
title : "Tạo Role"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2.2 </b> "
---
### Tạo vai trò cho quản trị viên EC2 và đính kèm các chính sách được quản lý đã tạo trước đó.

1. Đăng nhập vào AWS Management Console với tư cách là người dùng IAM đã bật MFA để có thể đảm nhận vai trò trong tài khoản AWS của bạn và mở bảng [điều khiển IAM](https://console.aws.amazon.com/iam/).

2. Trong ngăn điều hướng, chọn Vai trò rồi chọn Tạo vai trò.
![create_role](/images/3.connect/3.1/14_create_role.png)

3. Chọn tài khoản AWS , sau đó chọn Tài khoản AWS khác và nhập ID tài khoản bạn đang sử dụng và tích vào Yêu cầu MFA , sau đó chọn Tiếp theo . Thực thi MFA tại đây vì đây là phương pháp hay nhất.
![select_trusted_entity](/images/3.connect/3.1/15_select_trusted_entity.png)

4. Trong trường tìm kiếm, hãy bắt đầu nhập ec2- sau đó đánh dấu vào ô bên cạnh các chính sách bạn vừa tạo:
- ec2-create-tags
- ec2-create-tags-existing
- ec2-list-read
- ec2-manage-instances
- ec2-run-instances
![add_permission](/images/3.connect/3.1/16_add_permission.png)

5. Sao đó, nhập tên ```ec2-admin-team-alpha``` cho **Tên vai trò**.
   
6. Kiểm tra vai trò bạn đã tạo bằng cách chọn **ec2-admin-team-alpha** từ danh sách. Ghi lại cả ARN vai trò và liên kết đến bảng điều khiển.
   
7. Vai trò hiện đã được tạo và sẵn sàng để thử nghiệm!