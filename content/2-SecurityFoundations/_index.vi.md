---
title : "Nền tảng Bảo mật"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
[Trụ cột bảo mật]() mô tả cách tận dụng các công nghệ đám mây để bảo vệ dữ liệu, hệ thống và tài sản theo cách có thể cải thiện tình hình bảo mật của bạn. Bài báo này cung cấp hướng dẫn chuyên sâu, thực hành tốt nhất để thiết kế khối lượng công việc an toàn trên AWS.

### Nguyên tắc thiết kế
Trên đám mây, để tăng cường bảo mật cho khối lượng công việc, bạn nên tuân thủ các nguyên tắc sau:

- **Xây dựng nền tảng danh tính vững chắc**: Áp dụng nguyên tắc đặc quyền tối thiểu, phân tách nhiệm vụ rõ ràng và quản lý tập trung danh tính. Hạn chế sử dụng thông tin xác thực tĩnh dài hạn.

- **Duy trì khả năng truy xuất nguồn gốc**: Giám sát, cảnh báo và ghi nhật ký mọi hoạt động theo thời gian thực. Kết hợp với hệ thống để tự động điều tra và phản hồi.

- **Áp dụng bảo mật theo từng lớp**: Thực hiện phòng thủ chuyên sâu từ lớp mạng đến ứng dụng và mã nguồn. Mỗi lớp đều cần có cơ chế bảo vệ riêng.

- **Tự động hóa bảo mật**: Dùng các giải pháp bảo mật dưới dạng mã để dễ dàng triển khai, kiểm soát và mở rộng quy mô một cách an toàn và hiệu quả.

- **Bảo vệ dữ liệu ở mọi trạng thái**: Phân loại dữ liệu và sử dụng mã hóa, mã thông báo và kiểm soát truy cập khi truyền và khi lưu trữ.

- **Hạn chế truy cập trực tiếp vào dữ liệu**: Tối ưu hóa bằng cách tự động xử lý và sử dụng công cụ giảm thiểu tương tác thủ công, từ đó giảm rủi ro do con người gây ra.

- **Chuẩn bị cho sự cố bảo mật**: Xây dựng chính sách và quy trình phản hồi phù hợp. Thường xuyên luyện tập và ứng dụng công cụ tự động để tăng tốc phát hiện và phục hồi.

### Sự định nghĩa

Bảo mật trên đám mây bao gồm bảy lĩnh vực:
- [Nền tảng an ninh]()
- [Quản lý danh tính và quyền truy cập]()
- [Phát hiện]()
- [Bảo vệ cơ sở hạ tầng]()
- [Bảo vệ dữ liệu]()
- [Phản ứng sự cố]()
- [Bảo mật ứng dụng]()
