---
title : "Mô hình chia sẻ trách nhiệm"
date : "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---
### Mô hình chia sẻ trách nhiệm là gì?
Mô hình chia sẻ trách nhiệm (Shared Responsibility Model) là một khái niệm cốt lõi trong điện toán đám mây của AWS, xác định rõ ràng ranh giới giữa trách nhiệm của AWS và trách nhiệm của khách hàng trong việc đảm bảo bảo mật và tuân thủ. Trong mô hình này, AWS chịu trách nhiệm bảo vệ “cơ sở hạ tầng của đám mây”, bao gồm phần cứng, phần mềm, mạng lưới và các cơ sở vật lý hỗ trợ hoạt động của dịch vụ. Ngược lại, khách hàng chịu trách nhiệm về “bảo mật trong đám mây”, tức là mọi cấu hình, dữ liệu, và ứng dụng mà họ triển khai và sử dụng trong môi trường AWS.
![Shared-Responsibility](/images/2.prerequisite/aws-shared-responsibility.png)

### Trách nhiệm của AWS
AWS chịu trách nhiệm bảo vệ cơ sở hạ tầng chạy tất cả các dịch vụ được cung cấp trong Đám mây AWS. Cơ sở hạ tầng này bao gồm phần cứng, phần mềm, mạng và các tiện ích chạy dịch vụ Đám mây AWS.

### Trách nhiệm của khách hàng
Trách nhiệm của khách hàng sẽ được xác định bởi các dịch vụ Đám mây AWS mà khách hàng lựa chọn. Điều này xác định lượng công việc cấu hình mà khách hàng phải thực hiện như một phần trách nhiệm bảo mật của họ.

Ví dụ: một dịch vụ như Amazon Elastic Compute Cloud (Amazon EC2) được phân loại là Cơ sở hạ tầng dưới dạng Dịch vụ (IaaS) và do đó, yêu cầu khách hàng phải thực hiện tất cả các tác vụ quản lý và cấu hình bảo mật cần thiết. Khách hàng triển khai phiên bản Amazon EC2 chịu trách nhiệm quản lý hệ điều hành khách (bao gồm các bản cập nhật và bản vá bảo mật), bất kỳ phần mềm ứng dụng hoặc tiện ích nào do khách hàng cài đặt trên các phiên bản và cấu hình tường lửa do AWS cung cấp (gọi là nhóm bảo mật) trên mỗi phiên bản. Đối với các dịch vụ trừu tượng, chẳng hạn như Amazon S3 và Amazon DynamoDB, AWS vận hành lớp cơ sở hạ tầng, hệ điều hành và nền tảng, và khách hàng truy cập các điểm cuối để lưu trữ và truy xuất dữ liệu. Khách hàng chịu trách nhiệm quản lý dữ liệu của họ (bao gồm các tùy chọn mã hóa), phân loại tài sản của họ và sử dụng các công cụ IAM để áp dụng các quyền thích hợp.

### Mô hình trách nhiệm chia sẻ mở rộng sang kiểm soát công nghệ thông tin
Trách nhiệm kiểm soát công nghệ thông tin được chia sẻ giữa AWS và khách hàng, tương tự như vận hành hạ tầng công nghệ thông tin. AWS giúp giảm tải công việc cho khách hàng bằng cách quản lý các kiểm soát liên quan đến cơ sở hạ tầng vật lý. Mỗi khách hàng có mô hình triển khai khác nhau, dẫn đến môi trường kiểm soát phân tán. Khách hàng có thể sử dụng tài liệu tuân thủ của AWS để phục vụ việc đánh giá và xác minh kiểm soát.

Biện pháp kiểm soát do AWS, khách hàng AWS hoặc cả hai cùng quản lý:
- **Kiểm soát được kế thừa**: Quyền kiểm soát mà khách hàng được kế thừa hoàn toàn từ AWS.
- **Kiểm soát chung**: Kiểm soát áp dụng cho cả lớp cơ sở hạ tầng và lớp khách hàng, nhưng trong các bối cảnh hoặc góc nhìn riêng biệt. Trong kiểm soát chung, AWS cung cấp các yêu cầu cho cơ sở hạ tầng và khách hàng phải cung cấp triển khai kiểm soát của riêng họ trong quá trình sử dụng dịch vụ AWS. 
- **Kiểm soát cụ thể cho khách hàng**:  Các biện pháp kiểm soát hoàn toàn do khách hàng chịu trách nhiệm dựa trên ứng dụng họ đang triển khai trong các dịch vụ AWS.