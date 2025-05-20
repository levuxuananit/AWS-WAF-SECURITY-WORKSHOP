---
title : "Vận hành khối lượng công việc của bạn một cách an toàn"
date : "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 2.4 </b> "
---
### Toàn bộ vòng đời khối lượng công việc cần được đảm bảo an toàn
Để vận hành một khối lượng công việc (workload) an toàn trên AWS, bạn cần xem xét bảo mật trong toàn bộ vòng đời của nó, bảo mật từ giai đoạn thiết kế, xây dựng, vận hành, cho đến cải tiến liên tục.

Một trong những cách hiệu quả nhất để đạt được điều này là áp dụng phương pháp **Quản trị có tổ chức**. Quản trị không chỉ là đưa ra quyết định đúng, mà còn là đảm bảo các quyết định được thực hiện một cách nhất quán, thay vì phụ thuộc vào kinh nghiệm hoặc sự phán đoán cá nhân.

{{%notice note%}}
Bạn cần có quy trình quản trị rõ ràng để trả lời câu hỏi: "Làm thế nào tôi biết rằng các mục tiêu kiểm soát bảo mật đã được thực hiện đúng với khối lượng công việc này?"
{{%/notice%}}

Một quy trình ra quyết định nhất quán sẽ giúp bạn đẩy nhanh việc triển khai và nâng cao tiêu chuẩn bảo mật trong toàn tổ chức.

### Áp dụng thực hành bảo mật cho mọi lĩnh vực
Muốn vận hành an toàn, bạn phải đảm bảo rằng tất cả các lĩnh vực bảo mật đều được bao phủ – từ quản lý truy cập, bảo vệ dữ liệu, giám sát hoạt động đến ứng phó sự cố.

Hãy áp dụng những yêu cầu và quy trình đã xác định ở cấp tổ chức và khối lượng công việc cụ thể cho toàn bộ hệ thống.

Ngoài ra, cần luôn cập nhật:
- Các khuyến nghị mới nhất từ AWS và ngành công nghiệp
- Thông tin về mối đe dọa để bạn có thể xây dựng mô hình rủi ro và xác định các mục tiêu kiểm soát phù hợp

### Tự động hóa là chìa khóa cho bảo mật hiệu quả
Tự động hóa giúp đảm bảo rằng các quy trình bảo mật được thực hiện nhất quán và không bị lỗi con người.

Con người dễ mắc lỗi, đặc biệt khi phải thực hiện các tác vụ lặp đi lặp lại, hoặc khi phải xử lý nhiều cảnh báo cùng lúc.

Ngược lại, khi bạn tự động hóa:
- Quy trình sẽ được thực hiện giống nhau mỗi lần
- Dễ dàng kiểm tra mã triển khai
- Tăng độ tin cậy và giảm nguy cơ sai sót khi thay đổi
- Tự động hóa cũng cho phép bạn dễ dàng cập nhật và triển khai lại ứng dụng, đặc biệt khi có thêm yêu cầu kiểm soát mới.

### Kiểm tra cấu hình trước khi đưa vào sản xuất
Trước khi áp dụng bất kỳ cấu hình hay tự động hóa nào vào môi trường sản xuất, bạn nên:
- Kiểm thử trong môi trường thử nghiệm trước để đảm bảo tự động hóa thực hiện đúng các bước
- Nhận phản hồi sớm, giúp tránh việc sửa lỗi muộn gây tốn thời gian và công sức

Hãy thực hiện mọi thay đổi bằng mã (infrastructure as code), tránh cấu hình thủ công. Điều này giúp bạn có thể dễ dàng lặp lại, theo dõi, và phục hồi nếu có sự cố.

### Tận dụng các thành phần dùng chung thay vì "ai lo việc nấy"
Thay vì để từng nhóm hoặc từng ứng dụng tự xây dựng hệ thống bảo mật riêng, bạn nên xây dựng các năng lực bảo mật dùng chung để tiết kiệm thời gian và chuẩn hóa hệ thống.

Ví dụ về các thành phần dùng chung:
- Quy trình tạo tài khoản AWS
- Hệ thống quản lý danh tính tập trung
- Cấu hình ghi nhật ký (logging) chuẩn
- Tạo AMI hoặc container chuẩn sẵn có cho toàn tổ chức

Cách làm này giúp:
- Các nhóm phát triển tiết kiệm thời gian triển khai
- Tăng tốc độ đưa workload vào hoạt động
- Đảm bảo các mục tiêu bảo mật được đáp ứng nhất quán hơn

Với sự nhất quán giữa các nhóm, tổ chức của bạn cũng sẽ dễ dàng báo cáo rủi ro và tình trạng kiểm soát cho các bên liên quan như lãnh đạo, khách hàng hay cơ quan kiểm tra.

### Thực hành tốt nhất
[SEC01-BP03 Xác định và xác nhận mục tiêu kiểm soát](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_control_objectives.html)
[SEC01-BP04 Cập nhật các mối đe dọa bảo mật và khuyến nghị](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_updated_threats.html)
[SEC01-BP05 Thu hẹp phạm vi quản lý bảo mật](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_reduce_management_scope.html)
[SEC01-BP06 Tự động triển khai các biện pháp kiểm soát bảo mật tiêu chuẩn](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_automate_security_controls.html)
[SEC01-BP07 Xác định các mối đe dọa và ưu tiên giảm thiểu bằng cách sử dụng mô hình mối đe dọa](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_threat_model.html)
[SEC01-BP08 Đánh giá và triển khai các dịch vụ và tính năng bảo mật mới thường xuyên](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_implement_services_features.html)