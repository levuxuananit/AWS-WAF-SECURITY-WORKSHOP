---
title : "Mô hình chia sẻ trách nhiệm"
date : "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---
### Mô hình chia sẻ trách nhiệm là gì?
Mô hình chia sẻ trách nhiệm (Shared Responsibility Model) là một khái niệm cốt lõi trong điện toán đám mây của AWS, xác định rõ ràng ranh giới giữa trách nhiệm của AWS và trách nhiệm của khách hàng trong việc đảm bảo bảo mật và tuân thủ. Trong mô hình này, AWS chịu trách nhiệm bảo vệ “cơ sở hạ tầng của đám mây”, bao gồm phần cứng, phần mềm, mạng lưới và các cơ sở vật lý hỗ trợ hoạt động của dịch vụ. Ngược lại, khách hàng chịu trách nhiệm về “bảo mật trong đám mây”, tức là mọi cấu hình, dữ liệu, và ứng dụng mà họ triển khai và sử dụng trong môi trường AWS.
![Shared-Responsibility](../../../static/images/2.prerequisite/aws-shared-responsibility.png)

### Ý nghĩa của mô hình chia sẻ trách nhiệm
Mô hình này mang lại nhiều giá trị thiết thực cho khách hàng. Trước hết, nó giúp giảm bớt gánh nặng quản lý hạ tầng vật lý và nền tảng – vốn đòi hỏi chi phí đầu tư và nhân lực lớn – khi AWS đảm nhiệm hoàn toàn các phần này. Thứ hai, mô hình cho phép khách hàng tập trung vào việc xây dựng, triển khai và vận hành ứng dụng, thay vì lo lắng về cơ sở hạ tầng bên dưới. Đồng thời, nó cung cấp cho khách hàng sự linh hoạt và khả năng kiểm soát cao, giúp họ dễ dàng tích hợp các dịch vụ vào môi trường CNTT hiện có, đáp ứng các yêu cầu pháp lý, quy định nội bộ, và tiêu chuẩn ngành. Mô hình này cũng góp phần nâng cao tính minh bạch và hiểu biết trong quản trị rủi ro, giúp các tổ chức phân định rõ trách nhiệm và có chiến lược bảo mật phù hợp với từng loại dịch vụ AWS mà họ sử dụng.

### Trách nhiệm của khách hàng
Trách nhiệm của khách hàng trong mô hình chia sẻ phụ thuộc vào mức độ dịch vụ mà họ lựa chọn, đặc biệt là khi sử dụng các dịch vụ cơ sở hạ tầng như Amazon EC2 (IaaS). Khách hàng cần:
- Quản lý hệ điều hành khách, bao gồm việc cập nhật, vá lỗi và duy trì bảo mật.
- Cài đặt và vận hành các ứng dụng, dịch vụ, cơ sở dữ liệu hay phần mềm bên thứ ba trên các máy ảo hoặc nền tảng được cung cấp
- Cấu hình tường lửa và nhóm bảo mật (Security Groups) để kiểm soát lưu lượng truy cập vào hệ thống.
- Bảo vệ và quản lý dữ liệu, bao gồm việc phân loại thông tin, thiết lập các cơ chế mã hóa và đảm bảo tính riêng tư của dữ liệu
- Thiết lập quyền truy cập thông qua IAM (Identity and Access Management) để đảm bảo chỉ người có thẩm quyền mới được thực hiện các tác vụ cụ thể.
- Đào tạo và nâng cao nhận thức an ninh cho nhân viên, nhằm giảm thiểu rủi ro từ yếu tố con người trong việc sử dụng các dịch vụ đám mây.

### Trách nhiệm của AWS
AWS chịu trách nhiệm về bảo mật “của” đám mây, bao gồm:
- Bảo vệ cơ sở hạ tầng toàn cầu, gồm các trung tâm dữ liệu, hệ thống mạng, máy chủ vật lý và các lớp ảo hóa chạy các dịch vụ AWS.
- Quản lý, giám sát và duy trì an toàn vật lý, bao gồm kiểm soát truy cập vào trung tâm dữ liệu, giám sát 24/7 và các biện pháp phòng chống thảm họa.
- Duy trì tính sẵn sàng và bảo mật cho các nền tảng trừu tượng, chẳng hạn như Amazon S3, DynamoDB – nơi khách hàng chỉ tương tác ở cấp độ logic, còn mọi tác vụ về bảo mật hệ thống và nền tảng đều do AWS chịu trách nhiệm.
- Đảm bảo tuân thủ các tiêu chuẩn và chứng nhận quốc tế như ISO 27001, SOC 1/2/3, PCI DSS,... và cung cấp tài liệu minh bạch để khách hàng có thể sử dụng trong các hoạt động kiểm toán và đánh giá nội bộ.
- Hỗ trợ triển khai các biện pháp kiểm soát IT, bao gồm các quyền kiểm soát kế thừa, kiểm soát vật lý, kiểm soát chung và cung cấp công cụ hỗ trợ khách hàng triển khai biện pháp kiểm soát riêng theo nhu cầu.