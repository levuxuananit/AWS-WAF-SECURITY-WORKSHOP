---
title : "Quản lý và phân tách tài khoản AWS"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---
### Tách biệt khối lượng công việc bằng tài khoản riêng biệt
Khuyến nghị nên tổ chức khối lượng công việc (workloads) vào các tài khoản AWS riêng biệt, thay vì chia theo cấu trúc tổ chức hoặc phòng ban. Cách phân tách hiệu quả nhất là dựa vào:
- Chức năng (ví dụ: sản xuất, phát triển, kiểm thử)
- Yêu cầu tuân thủ pháp lý
- Các chính sách kiểm soát bảo mật chung
- 
Lý do: Trong AWS, tài khoản là ranh giới cách ly cứng, giúp hạn chế rủi ro lan rộng. Ví dụ, bạn nên sử dụng tài khoản riêng để cách ly môi trường sản xuất (production) khỏi môi trường phát triển (development) và kiểm thử (test) nhằm đảm bảo an toàn và ổn định.

### Quản lý tập trung với AWS Organizations
**AWS Organizations** là công cụ giúp bạn tự động hóa việc tạo, quản lý và điều phối tài khoản AWS trong một tổ chức lớn.

Khi tạo tài khoản mới qua Organizations, hãy cẩn trọng với địa chỉ email sử dụng, vì đó là tài khoản root và sẽ được dùng để khôi phục mật khẩu nếu cần.

Organizations cũng cho phép bạn nhóm các tài khoản lại với nhau theo mục đích sử dụng thông qua Organizational Units (OU).

Ví dụ: bạn có thể nhóm các tài khoản thuộc môi trường sản xuất vào một OU, và các tài khoản phát triển vào OU khác để áp dụng chính sách phù hợp.

### Thiết lập kiểm soát tập trung bằng SCP
Bạn có thể giới hạn hành vi của tài khoản AWS bằng cách sử dụng Service Control Policies (SCP) – chính sách được áp dụng ở cấp tổ chức, OU hoặc tài khoản cụ thể.

SCP cho phép bạn:
- Chỉ định các dịch vụ AWS, vùng (region) và hành động API nào được phép sử dụng.
- Hạn chế tài khoản khởi tạo tài nguyên tại những vùng chưa được cho phép rõ ràng.

Ví dụ, bạn có thể tạo một SCP ngăn người dùng tạo tài nguyên ở ngoài khu vực Vùng châu Á Thái Bình Dương nếu tổ chức chỉ muốn sử dụng dịch vụ tại khu vực đó.

**AWS Control Tower** là công cụ hỗ trợ đơn giản hóa toàn bộ quá trình thiết lập này. Nó giúp bạn:
- Tự động tạo và cấu hình tài khoản mới.
- Áp dụng các biện pháp bảo vệ (cả phòng ngừa lẫn phát hiện).
- Cung cấp bảng điều khiển để giám sát toàn bộ tổ chức.

## Cấu hình dịch vụ và tài nguyên một cách tập trung
Với AWS Organizations, bạn có thể áp dụng cấu hình dịch vụ AWS cho toàn bộ hệ thống tài khoản trong tổ chức.

Một số ví dụ thực tế:
- AWS CloudTrail: Ghi lại toàn bộ hoạt động API trong tổ chức một cách tập trung, giúp theo dõi và kiểm tra bảo mật.
- AWS Config: Thu thập và đánh giá cấu hình tài nguyên để đảm bảo tuân thủ chính sách. Bạn có thể tổng hợp dữ liệu từ nhiều tài khoản để theo dõi và phản ứng nhanh với các thay đổi.
- AWS CloudFormation StackSets: Cho phép triển khai đồng thời các cấu hình hạ tầng (stack) tới nhiều tài khoản và OU một cách tự động, giúp bảo đảm ính nhất quán và tuân thủ yêu cầu bảo mật.

### Phân quyền quản trị bảo mật rõ ràng
Bạn nên tách các tài khoản quản trị bảo mật ra khỏi tài khoản thanh toán hoặc tài khoản điều hành chung.

Một số dịch vụ như:
- Amazon GuardDuty
- AWS Security Hub
- AWS Config
- ...
Tích hợp với AWS Organizations và cho phép bạn chỉ định một tài khoản cụ thể làm tài khoản quản trị (admin). Từ đó, bạn có thể kiểm soát và giám sát các dịch vụ bảo mật trong toàn bộ hệ thống tài khoản một cách tập trung và rõ ràng hơn.

### Thực hành tốt nhất
[SEC01-BP01 Phân chia khối lượng công việc bằng tài khoản](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_multi_accounts.html)
[SEC01-BP02 Tài khoản người dùng gốc an toàn và các thuộc tính][(](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_aws_account.html))