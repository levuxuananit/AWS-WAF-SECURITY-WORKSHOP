---
title : "Thiết lập tài khoản AWS và người dùng gốc"
date : "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 2.5 </b> "
---
### Kiểm tra báo cáo xác thực tài khoản AWS
Bạn nên kiểm tra cấu hình bảo mật của mình trong các tình huống sau:
- Bạn nên kiểm tra định kỳ hoặc trong các trường hợp sau:
- Định kỳ như một thói quen bảo mật tốt.
- Có thay đổi nhân sự (ví dụ: ai đó nghỉ việc).
- Ngừng sử dụng một số dịch vụ AWS → nên xóa quyền không còn cần thiết.
- Thêm/xóa phần mềm như EC2, OpsWorks, CloudFormation, v.v.
- Nghi ngờ tài khoản bị truy cập trái phép.

Khi bạn xem lại cấu hình bảo mật của tài khoản, hãy nhớ:
- Kiểm tra kỹ: Đừng bỏ qua bất kỳ phần nào, dù ít dùng.
- Không phỏng đoán: Nếu không rõ về chính sách hay vai trò nào, hãy tìm hiểu kỹ
- Giữ đơn giản: Dùng nhóm IAM, đặt tên nhất quán, chính sách rõ ràng để dễ quản lý.
Bạn có thể tải báo cáo thông tin xác thực từ AWS Management Console dưới dạng tệp CSV. Lưu ý: có thể mất đến 4 giờ để cập nhật thay đổi.
- Bạn có thể tìm thêm thông tin tại https://docs.aws.amazon.com/general/latest/gr/aws-security-audit-guide.html

Bạn có thể sử dụng **AWS Management Console** để tải xuống báo cáo thông tin xác thực dưới dạng tệp giá trị phân tách bằng dấu phẩy (CSV). Xin lưu ý rằng báo cáo thông tin xác thực có thể mất 4 giờ để phản ánh các thay đổi. Để tải xuống báo cáo thông tin xác thực bằng AWS Management Console:
1. Đăng nhập vào **AWS Management Console** và mở [bảng điều khiển IAM](https://console.aws.amazon.com/iam/).
Trong ngăn điều hướng, chọn Báo cáo thông tin xác thực.
2. Chọn Tải xuống báo cáo .
![download-credentials-report](/images/2.SecurityFoundations/download-credentials-report.png)

{{%notice note%}}
Bạn có thể tìm thêm thông tin về báo cáo tại https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html
{{%/notice%}}

### Thiết bị ảo MFA
Bạn có thể dùng dịch vụ IAM trong **AWS Management Console** để cấu hình và bật thiết bị MFA ảo cho người dùng gốc. MFA là một ứng dụng trung gian, thường là diện thoại cá nhân giúp xác thực người đang đăng nhập có phải người dùng gốc không? Chỉ người dùng gốc mới có thể quản lý thiết bị MFA cho chính mình. Bạn cần đăng nhập bằng thông tin đăng nhập của người dùng gốc, không thể dùng tài khoản IAM khác để thay đổi cài đặt này.

Nếu bạn làm mất hoặc không thể dùng thiết bị MFA, bbạn vẫn có thể đăng nhập bằng cách xác minh danh tính qua:
- Email đã đăng ký với tài khoản AWS.
- Số điện thoại đã đăng ký.

{{%notice note%}}
Vì vậy, trước khi bật MFA, hãy đảm bảo rằng: Email và số điện thoại trong tài khoản AWS là chính xác và bạn còn quyền truy cập.
{{%/notice%}}

Để tìm hiểu về cách đăng nhập bằng các yếu tố xác thực thay thế, hãy xem [Điều gì xảy ra nếu thiết bị MFA bị mất hoặc ngừng hoạt động ?](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_lost-or-broken.html). Để tắt tính năng này, hãy liên hệ với [bộ phận Hỗ trợ AWS](https://console.aws.amazon.com/support/home#/).

### Kích hoạt thiết bị MFA ảo cho tài khoản người dùng gốc trong AWS 
1. Sử dụng địa chỉ email và mật khẩu tài khoản AWS của bạn để đăng nhập với tư cách là người dùng gốc của tài khoản AWS vào [bảng điều khiển IAM](https://console.aws.amazon.com/iam/).
   
2. Thực hiện một trong những thao tác sau:
- Tùy chọn 1: Chọn Bảng điều khiển và trong ngăn Liên kết nhanh, chọn **Thông tin xác thực bảo mật của tôi**.
- Tùy chọn 2: Ở bên phải thanh điều hướng, hãy chọn tên tài khoản của bạn và chọn **Security Credentials**. Nếu cần, hãy chọn **Continue to Security Credentials**. Sau đó, mở rộng phần **Multi-Factor Authentication (MFA**) trên trang.
![security_credentials](/images/2.SecurityFoundations/2_SC.png)

3. Tiếp theo, chọn vào "Assign MFA device" để kết nối thiết bị MFA của bạn 
![assign_MFA](/images/2.SecurityFoundations/3_assign_MFA.png)

4. Tiếp theo, chọn loại thiết bị MFA:
- Đặt tên thiết bị: ```MyMFADevice```
- Chọn: **Authenticator app**
![select_device](/images/2.SecurityFoundations/4_select_device.png)
Các lựa chọn bao gồm:
- **Virtual MFA device**: Sử dụng ứng dụng xác thực như Google Authenticator
- **Hardware TOTP token**: Sử dụng thiết bị phần cứng chuyên dụng
- **Security key**: Sử dụng khóa bảo mật FIDO

1. Cuối cùng, cài đặt thiết bị MFA:
- Chọn **Show QR code**
- Nhập 2 mã MFA liên tiếp bên dưới:
    - Nhập mã từ ứng dụng ảo của bạn.
    - Chờ 30 giây và nhập mã thứ hai.
![setup_device](/images/2.SecurityFoundations/5_setup_device.png)

### Cấu hình tài khoản liên hệ thay thế
Các liên hệ thay thế cho phép AWS liên hệ với người khác về các sự cố liên quan đến tài khoản, ngay cả khi bạn không có mặt.
1. Đầu tiên, đđăng nhập vào AWS với tư cách người dùng gốc và mở trang cài đặt tài khoản AWS
![setup_account](/images/2.SecurityFoundations/6_setup_account.png)

2. Tiếp theo, điều hướng đến phần cấu hình danh bạ thay thế.
![setup_account](/images/2.SecurityFoundations/7_alternate_contacts.png.png)

3. Tiếp theo, nhập thông tin liên hệ để thanh toán, vận hành và bảo mật.
4. Cuối cùng, Chọn **Cập nhật**.

### Xóa khóa truy cập người dùng gốc của tài khoản AWS của bạn
Khóa truy cập (gồm Access Key ID và Secret Access Key) được dùng để thực hiện các yêu cầu tới AWS qua chương trình (ví dụ: dùng AWS CLI hoặc SDK). Tuy nhiên, Tuyệt đối không sử dụng khóa truy cập của người dùng gốc, vì khóa truy cập này có toàn quyền với mọi dịch vụ và tài nguyên, bao gồm cả thông tin thanh toán. Bạn không thể giới hạn quyền khi sử dụng khóa truy cập của người dùng gốc, nên rất rủi ro về mặt bảo mật.

**Phương pháp truy cập an toàn**:
- Không tạo khóa truy cập cho người dùng gốc, trừ khi thực sự cần thiết.
- Đăng nhập AWS Management Console bằng email và mật khẩu người dùng gốc.
- Tạo một người dùng IAM với quyền quản trị.
- Sử dụng người dùng IAM đó để tạo khóa truy cập nếu cần.
- Xóa khóa truy cập người dùng gốc càng sớm càng tốt để bảo vệ tài khoản.
- Xoay vòng (thay mới) hoặc xóa khóa trong mục Thông tin xác thực bảo mật (Security Credentials) của AWS Management Console.
- **Lưu ý**: Bạn cần đăng nhập bằng thông tin người dùng gốc (email và mật khẩu) để thực hiện việc này.

1. Ở bên phải thanh điều hướng, hãy chọn tên tài khoản của bạn và chọn **Security Credentials**
![security_credentials](/images/2.SecurityFoundations/2_SC.png)

2. Xóa khóa truy cập người dùng gốc.
![delete_accesske](/images/2.SecurityFoundations/8_delete_accesskey.png)

{{%notice note%}}
Không bao giờ chia sẻ mật khẩu tài khoản AWS hoặc khóa truy cập của bạn với bất kỳ ai.
{{%/notice%}}

### Thay đổi định kỳ mật khẩu người dùng gốc của tài khoản AWS
1. Sử dụng địa chỉ email và mật khẩu tài khoản AWS của bạn để đăng nhập vào AWS Management Console với tư cách là người dùng gốc.
{{%notice note%}}
Nếu trước đó bạn đã đăng nhập vào bảng điều khiển bằng thông tin xác thực người dùng IAM, trình duyệt của bạn có thể nhớ tùy chọn này và mở trang đăng nhập dành riêng cho tài khoản của bạn. Bạn không thể sử dụng trang đăng nhập người dùng IAM để đăng nhập bằng thông tin xác thực người dùng gốc của tài khoản AWS. Nếu bạn thấy trang đăng nhập người dùng IAM, hãy nhấp vào Đăng nhập bằng thông tin xác thực tài khoản gốc gần cuối trang để quay lại trang đăng nhập chính. Từ đó, bạn có thể nhập địa chỉ email và mật khẩu tài khoản AWS của mình.
{{%/notice%}}

2. Ở góc trên bên phải của bảng điều khiển, chọn tên hoặc số tài khoản của bạn rồi chọn **Tài khoản**.
![security_credentials](/images/2.SecurityFoundations/2_SC.png)

3. Trong ngăn Cài đặt tài khoản, chọn **Hành động**, chọn **Chỉnh sửa địa chỉ email và mật khẩu**.
![update_email_password](/images/2.SecurityFoundations/9_update_email_password.png)

4. Yêu cầu điền mã MFA để điều hướng tới trang cài đặt địa chỉ email và mật khẩu, chọn **Chỉnh sửa**, sau đó nhập mật khẩu hiện tại, mật khẩu mới và xác nhận mật khẩu mới (tương tự với địa chỉ email)
![account_detai](/images/2.SecurityFoundations/10_account_detail.png)

5. Chọn **Lưu thay đổi** để lưu mật khẩu mới của bạn.

{{%notice note%}}
Chọn mật khẩu mạnh. Mặc dù bạn có thể thiết lập chính sách mật khẩu tài khoản cho người dùng IAM, nhưng chính sách đó không áp dụng cho người dùng gốc tài khoản AWS của bạn. AWS yêu cầu mật khẩu của bạn phải đáp ứng các điều kiện sau: - Có tối thiểu 8 ký tự và tối đa 128 ký tự. - Bao gồm tối thiểu ba trong số các loại ký tự sau: chữ hoa, chữ thường, số và ! @ # $ % ^ & * () <> [] {} | _ + - =ký hiệu. - Không giống với tên tài khoản AWS hoặc địa chỉ email của bạn.
{{%/notice%}}

**Để bảo vệ mật khẩu của bạn, điều quan trọng là phải tuân theo các biện pháp tốt nhất sau**:
- Thay đổi mật khẩu định kỳ và giữ bí mật mật khẩu của bạn, vì bất kỳ ai biết mật khẩu của bạn đều có thể truy cập vào tài khoản của bạn.
- Sử dụng mật khẩu khác trên AWS so với mật khẩu bạn sử dụng trên các trang web khác.
- Tránh sử dụng mật khẩu dễ đoán, như secret, password, amazon hoặc 123456, thứ như từ điển, tên, địa chỉ email của bạn hoặc thông tin cá nhân khác có thể dễ dàng lấy được.

### Cấu hình Chính sách Mật khẩu Mạnh cho Người dùng của Bạn
1. Đăng nhập vào AWS Management Console và [bảng điều khiển IAM](https://console.aws.amazon.com/iam/).
2. Trong ngăn điều hướng, chọn Cài đặt tài khoản.
3. Trong ngăn Chính sách mật khẩu, chọn Chỉnh sửa ở góc trên bên phải.
![password_policy](/images/2.SecurityFoundations/11_password_policy.png)
4. Trong ngăn Chỉnh sửa chính sách mật khẩu, bạn có thể chọn IAM mặc định hoặc tạo chính sách mật khẩu Tùy chỉnh của riêng bạn.
![password_policy](/images/2.SecurityFoundations/12_edit_pasword_policy.png)
5. Chọn **Lưu thay đổi** để lưu chính sách mật khẩu.