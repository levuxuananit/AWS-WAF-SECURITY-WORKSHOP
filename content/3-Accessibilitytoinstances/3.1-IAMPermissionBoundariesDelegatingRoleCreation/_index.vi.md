---
title : "Giới hạn quyền IAM ủy quyền tạo vai trò"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---
### Giới thiệu
Trong phần quản lý danh tính và truy cập, chúng ta sẽ thực hiện các bước để cấu hình ranh giới quyền AWS Identity and Access Management (IAM) mẫu. AWS hỗ trợ ranh giới quyền cho các thực thể IAM (người dùng hoặc vai trò). Ranh giới quyền là một tính năng nâng cao trong đó bạn sử dụng chính sách được quản lý để đặt các quyền tối đa mà chính sách dựa trên danh tính có thể cấp cho một thực thể IAM. Khi bạn đặt ranh giới quyền cho một thực thể, thực thể đó chỉ có thể thực hiện các hành động được chính sách cho phép.

Trong phần này, bạn sẽ tạo một loạt các chính sách được đính kèm vào một vai trò mà một cá nhân như nhà phát triển có thể đảm nhiệm, sau đó nhà phát triển có thể sử dụng vai trò này để tạo các vai trò người dùng bổ sung bị giới hạn ở các dịch vụ và vùng cụ thể. Điều này cho phép bạn ủy quyền quyền truy cập để tạo các vai trò và chính sách IAM mà không vượt quá các quyền trong ranh giới quyền. Chúng tôi cũng sẽ sử dụng một tiêu chuẩn đặt tên có tiền tố, giúp kiểm soát và sắp xếp các chính sách và vai trò mà nhà phát triển của bạn tạo ra dễ dàng hơn.

### Mục tiêu
- Ranh giới quyền IAM
- Điều kiện chính sách IAM

### Thực hành tốt nhất
Các biện pháp bảo mật tốt nhất được áp dụng trong phòng phần này là:
- Quản lý thông tin xác thực và xác thực Sử dụng MFA để truy cập nhằm cung cấp khả năng kiểm soát truy cập bổ sung.
- Cấp quyền truy cập thông qua vai trò hoặc liên kết: Các vai trò có chính sách liên quan đã được sử dụng để xác định ranh giới quyền hạn phù hợp.
- Cấp quyền tối thiểu: Các vai trò được giới hạn với các đặc quyền tối thiểu để hoàn thành nhiệm vụ.