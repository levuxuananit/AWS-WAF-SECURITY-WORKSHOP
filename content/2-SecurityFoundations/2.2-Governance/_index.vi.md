---
title : "Quản trị"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---
### Quản trị bảo mật
**Quản trị bảo mật** là một phần quan trọng trong chiến lược tổng thể nhằm bảo vệ hệ thống và hỗ trợ các mục tiêu kinh doanh. Việc này không chỉ dừng lại ở các giải pháp kỹ thuật, mà còn bao gồm việc xác định các chính sách và mục tiêu kiểm soát bảo mật để giúp tổ chức quản lý rủi ro một cách hiệu quả.

AWS đề xuất cách tiếp cận quản trị bảo mật theo mô hình nhiều lớp (layered approach). Trong mô hình này, mỗi lớp bảo mật đều bổ sung và xây dựng dựa trên lớp trước, tạo thành một hệ thống phòng thủ vững chắc và linh hoạt. 

### Lớp nền tảng 
Lớp đầu tiên và quan trọng nhất là hiểu rõ Mô hình Trách nhiệm Chung (Shared Responsibility Model) của AWS. Theo mô hình này:
- AWS chịu trách nhiệm bảo mật "trong" phần hạ tầng đám mây, bao gồm phần cứng, phần mềm, mạng và cơ sở vật lý nơi dịch vụ được vận hành.
- Khách hàng chịu trách nhiệm bảo mật "trên" đám mây, bao gồm cấu hình dịch vụ, quản lý dữ liệu, danh tính người dùng và quyền truy cập.
- Hiểu được ranh giới này giúp tổ chức xác định rõ phần nào mình cần kiểm soát và phần nào có thể tin cậy vào AWS.

Ngoài ra, AWS cung cấp [Artifact](https://aws.amazon.com/artifact/), cung cấp các tài liệu bảo mật và tuân thủ như báo cáo kiểm toán, chứng nhận và các thỏa thuận pháp lý.

### Lớp nền tảng bảo mật
Lớp thứ hai là nơi bạn triển khai phần lớn các mục tiêu kiểm soát bảo mật thông qua công cụ và dịch vụ có sẵn của AWS. Tại lớp này, bạn có thể:
- Quản lý tài khoản AWS theo mô hình nhiều tài khoản để cách ly rủi ro.
- Tích hợp danh tính người dùng với hệ thống như AWS IAM Identity Center.
- Thiết lập các biện pháp kiểm soát phát hiện như giám sát, ghi log, cảnh báo sự kiện bất thường.
- Khi tổ chức bắt đầu sử dụng dịch vụ AWS mới, bạn có thể cập nhật chính sách kiểm soát dịch vụ (SCP) trong AWS Organizations để đảm bảo dịch vụ mới chỉ được sử dụng trong giới hạn cho phép.

Ngoài ra, bạn có thể triển khai các chính sách bảo mật bất biến (immutable security guardrails) – tức là các chính sách áp dụng cho nhiều tài khoản hoặc toàn bộ tổ chức, không thể bị thay đổi bởi người dùng cấp dưới.
Ví dụ:
- Hạn chế chỉ cho phép sử dụng dịch vụ ở một số vùng cụ thể (Regions).
- Ngăn người dùng tắt các công cụ phát hiện hoặc ghi log.
- Lớp này cũng bao gồm các chính sách mã hóa, chẳng hạn như sử dụng AWS Config rules để theo dõi cấu hình dịch vụ, hoặc tích hợp kiểm tra bảo mật trong quy trình CI/CD để phát hiện sớm lỗi cấu hình.

### Lớp ứng dụng
Lớp trên cùng là nơi các nhóm phát triển sản phẩm chịu trách nhiệm trực tiếp cho việc thực hiện các kiểm soát bảo mật trong ứng dụng mà họ quản lý.
Ví dụ:
- Thực hiện kiểm tra đầu vào trong ứng dụng web để ngăn chặn tấn công SQL Injection.
- Đảm bảo danh tính và quyền truy cập được truyền đúng cách giữa các dịch vụ vi mô (microservices).
- Bảo vệ API, mã hóa dữ liệu khi truyền tải.

Dù các nhóm sản phẩm chịu trách nhiệm chính ở lớp này, họ vẫn có thể kế thừa các chính sách và công cụ bảo mật từ lớp giữa, giúp đảm bảo tính nhất quán và giảm gánh nặng vận hành.

### Mục tiêu chung
Dù kiểm soát được triển khai ở lớp nào, thì mục tiêu cuối cùng vẫn là quản lý rủi ro một cách hiệu quả. Quá trình quản lý rủi ro bao gồm:
- Xác định rủi ro cố hữu (Inherent Risk): Là mức rủi ro ban đầu, chưa có biện pháp kiểm soát. Được đánh giá dựa trên:
- Khả năng xảy ra (Likelihood): Dựa trên tần suất hoặc lịch sử xảy ra sự cố.
- Hậu quả (Impact): Đánh giá theo tổn thất tài chính, thời gian gián đoạn hoặc ảnh hưởng đến danh tiếng.
- Áp dụng biện pháp kiểm soát (Controls): Xây dựng các chính sách, công cụ, cấu hình nhằm giảm khả năng xảy ra, mức độ ảnh hưởng, hoặc cả hai.
- Đánh giá rủi ro còn lại (Residual Risk): Là mức rủi ro sau khi đã triển khai các biện pháp kiểm soát. Tổ chức cần quyết định mức độ rủi ro này có thể chấp nhận được hay không.

Mục tiêu kiểm soát có thể áp dụng cho một workload cụ thể, hoặc mở rộng ra nhiều hệ thống trong tổ chức.



