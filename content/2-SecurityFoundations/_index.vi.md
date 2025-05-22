---
title : "Nền tảng Bảo mật"
date : "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
### Trụ cột bảo mật
**Trụ cột bảo mật** bao gồm khả năng bảo vệ dữ liệu, hệ thống và tài sản nhằm tận dụng công nghệ đám mây để nâng cao mức độ bảo mật.

### Nguyên tắc thiết kế
Trên đám mây, để tăng cường bảo mật cho khối lượng công việc, bạn nên tuân thủ các nguyên tắc sau:
- **Xây dựng nền tảng danh tính vững chắc**: Áp dụng nguyên tắc đặc quyền tối thiểu, phân tách nhiệm vụ rõ ràng và quản lý tập trung danh tính. Hạn chế sử dụng thông tin xác thực tĩnh dài hạn.
- **Duy trì khả năng truy xuất nguồn gốc**: Giám sát, cảnh báo và ghi nhật ký mọi hoạt động theo thời gian thực. Kết hợp với hệ thống để tự động điều tra và phản hồi.
- **Áp dụng bảo mật theo từng lớp**: Thực hiện phòng thủ chuyên sâu từ lớp mạng đến ứng dụng và mã nguồn. Mỗi lớp đều cần có cơ chế bảo vệ riêng.
- **Tự động hóa bảo mật**: Dùng các giải pháp bảo mật dưới dạng mã để dễ dàng triển khai, kiểm soát và mở rộng quy mô một cách an toàn và hiệu quả.
- **Bảo vệ dữ liệu ở mọi trạng thái**: Phân loại dữ liệu và sử dụng mã hóa, mã thông báo và kiểm soát truy cập khi truyền và khi lưu trữ.
- **Hạn chế truy cập trực tiếp vào dữ liệu**: Tối ưu hóa bằng cách tự động xử lý và sử dụng công cụ giảm thiểu tương tác thủ công, từ đó giảm rủi ro do con người gây ra.
- **Chuẩn bị cho sự cố bảo mật**: Xây dựng chính sách và quy trình phản hồi phù hợp. Thường xuyên luyện tập và ứng dụng công cụ tự động để tăng tốc phát hiện và phục hồi.

### Lĩnh vực thực hành tốt nhất
Bảo mật trong đám mây bao gồm bảy lĩnh vực:
- **Nền tảng bảo mật (Security Foundations)**: Đặt ra các nguyên tắc cơ bản và thiết lập môi trường bảo mật vững chắc từ đầu, bao gồm việc cấu hình đúng tài khoản, khuôn mẫu tổ chức, kiểm soát bảo mật cơ bản và chính sách quản trị.
- **Quản lý danh tính và quyền truy cập (Identity and Access Management - IAM)**: Đảm bảo chỉ những người, dịch vụ và hệ thống được ủy quyền mới có thể truy cập tài nguyên. Áp dụng nguyên tắc đặc quyền tối thiểu, xác thực đa yếu tố (MFA) và quản lý tập trung quyền truy cập.
- **Phát hiện (Detection)**: Giám sát và ghi nhận các hành động trong môi trường AWS. Sử dụng dịch vụ như AWS CloudTrail, Amazon GuardDuty để phát hiện các hành vi bất thường hoặc có nguy cơ.
- **Bảo vệ hạ tầng (Infrastructure Protection)**: Triển khai các lớp bảo mật để bảo vệ mạng, máy chủ và dịch vụ khỏi truy cập trái phép. Bao gồm cấu hình VPC, nhóm bảo mật (Security Groups), tường lửa và kiểm soát lưu lượng.
- **Bảo vệ dữ liệu (Data Protection)**: Bảo vệ dữ liệu khi truyền và khi lưu trữ bằng các cơ chế như mã hóa, kiểm soát truy cập và phân loại dữ liệu theo mức độ nhạy cảm.
- **Ứng phó sự cố (Incident Response)**: Chuẩn bị các quy trình và công cụ để phản ứng kịp thời với các sự cố bảo mật. Bao gồm mô phỏng, ghi lại sự kiện và tự động hóa quá trình phát hiện, phân tích và khôi phục.
- **Bảo mật ứng dụng (Application Security)**: Tích hợp bảo mật vào vòng đời phát triển phần mềm (DevSecOps). Kiểm tra lỗ hổng, quản lý bản vá và mã hóa thông tin trong ứng dụng để đảm bảo an toàn từ cấp độ mã nguồn.

### Nội dung
Worklog này giới thiệu một số kiến nền tảng bảo mật:
- [Trụ cột bảo mật](./2-SecurityFoundations/)
- [Mô hình chia sẻ trách nhiệm](./2.1-SharedResponsibility/)
- [Quản trị](./2.1-SharedResponsibility/)
- [Quản lý và phân tách tài khoản](./2.3-AWSAccountManagementAndSeparation/)
- [Vận hành khối lượng công việc một cách an toàn](./2.4-OperatingYourWorkloadsSecurely/)
- [Thiết lập tài khoản AWS và người dùng gốc](./2.5-AWSAccountSetupandRootUser/)
- [Tạo tài khoản Data Bunker](./2.6-CreateADataBunkerAccount/)