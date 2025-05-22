---
title : "Kiểm soát truy cập dựa trên thẻ IAM cho EC2"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---
### Giới thiệu
Bài thực hành này sẽ hướng dẫn bạn các bước để cấu hình các chính sách AWS Identity and Access Management (IAM) mẫu và vai trò AWS IAM với các quyền liên quan để sử dụng thẻ tài nguyên EC2 để kiểm soát quyền truy cập. Sử dụng thẻ rất hiệu quả vì nó giúp bạn mở rộng quy mô quản lý quyền của mình, tuy nhiên bạn cần cẩn thận về việc quản lý các thẻ mà bạn sẽ học trong bài thực hành này.

Trong phòng thí nghiệm này, bạn sẽ tạo một loạt các chính sách được gắn vào một vai trò mà một cá nhân như quản trị viên EC2 có thể đảm nhiệm. Điều này cho phép quản trị viên EC2 tạo thẻ khi tạo tài nguyên chỉ khi chúng khớp với các yêu cầu và kiểm soát các tài nguyên và giá trị hiện có mà họ có thể gắn thẻ.

Các kỹ năng bạn học được sẽ giúp bạn bảo vệ khối lượng công việc của mình theo AWS Well-Architected Framework .

### Mục tiêu
- Đạt được đặc quyền tối thiểu của IAM
- Tìm hiểu về các điều kiện chính sách của IAM

### Thực hành tốt nhất
Các biện pháp bảo mật tốt nhất được áp dụng trong phòng thí nghiệm này là:
- Quản lý thông tin đăng nhập và xác thực: Sử dụng MFA để truy cập nhằm cung cấp khả năng kiểm soát truy cập bổ sung.
- Cấp quyền tối thiểu: Các vai trò được giới hạn với các đặc quyền tối thiểu để hoàn thành nhiệm vụ.
- Điều kiện tiên quyết