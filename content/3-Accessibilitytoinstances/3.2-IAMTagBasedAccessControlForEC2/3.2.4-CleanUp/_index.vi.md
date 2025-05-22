---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 3.2.4 </b> "
---
{{%notice note%}}
Xin lưu ý rằng những thay đổi bạn thực hiện đối với chính sách và vai trò không liên quan đến bất kỳ khoản phí nào.
{{%/notice%}}

1. Sử dụng người dùng IAM gốc, chọn vai trò ec2-admin-team-alpha trong [bảng điều khiển IAM](https://console.aws.amazon.com/iam/) và chọn **Xóa vai trò** 

2. Đối với mỗi chính sách bạn đã tạo, hãy chọn nút radio rồi chọn menu thả xuống Hành động chính sách rồi chọn Xóa .
Các chính sách được tạo ra là:
- ec2-create-tags
- ec2-create-tags-existing
- ec2-list-read
- ec2-manage-instances
- ec2-run-instances

### Tài liệu tham khảo & tài nguyên hữu ích
[Hướng dẫn sử dụng AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
[Các trường hợp sử dụng và thực hành tốt nhất của IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPracticesAndUseCases.html)
[Trở thành Chuyên gia Chính sách IAM trong vòng 60 phút hoặc ít hơn](https://youtu.be/YQsK4MtsELU)
[Hành động, Tài nguyên và Khóa điều kiện cho Quản lý danh tính và quyền truy cập](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_identityandaccessmanagement.html) 