---
title : "Tạo và kiểm tra vai trò nhà phát triển"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.1.2 </b> "
---
### Tạo vai trò nhà phát triển
Tạo vai trò cho các nhà phát triển, để nhà phát triển có quyền tạo vai trò và chính sách, với ranh giới quyền và tiền tố đặt tên được áp dụng.

1. Đăng nhập vào AWS Management Console với tư cách là người dùng IAM đã bật MFA để có thể đảm nhận vai trò trong tài khoản AWS của bạn và mở [bảng điều khiển IAM](https://console.aws.amazon.com/iam/).
    
2. Trong ngăn điều hướng, chọn Vai trò rồi chọn **Create**.

3. Chọn **Tài khoản AWS khác**, sau đó nhập **ID tài khoản của bạn** và đánh dấu vào **Yêu cầu MFA**, sau đó chọn **Tiếp theo. Tại bước này, chọn thực thi MFA là phương pháp hay nhất.
![select_trusted_entity](/images/3.connect/3.1/4_select_trusted_entity.png)

4. Trong trường tìm kiếm, hãy bắt đầu nhập ```createrole``` rồi đánh dấu vào ô bên cạnh chính sách ``createrole-restrict-region-boundary``.
![add_createrole](/images/3.connect/3.1/5_add_createrole.png)

5. Xóa bộ lọc **createrole** và bắt đầu nhập ```iam-res```, sau đó đánh dấu vào ô bên cạnh chính sách ``iam-restricted-list-read``, rồi chọn **Next**.
![add-iam_rlr](/images/3.connect/3.1/6_add-iam_rlr.png)

6. Nhập tên ```developer-restricted-iam``` cho Tên vai trò và chọn **Tạo vai trò**.
![role_name](/images/3.connect/3.1/7_role_name.png)

7. Kiểm tra vai trò bạn đã tạo bằng cách chọn **developer-restricted-iam** trong danh sách. 
![choose_new_role](/images/3.connect/3.1/8_choose_new_role.png)

1. Ghi lại cả **ARN vai trò** và **liên kết đến bảng điều khiển**.
![copy_arn](/images/3.connect/3.1/9_copy_arn.png)

1. Vai trò hiện đã được tạo và sẵn sàng để thử nghiệm!

### Xác nhận vai trò của nhà phát triển thử nghiệm
Bây giờ bạn sẽ sử dụng người dùng IAM đã bật MFA để đảm nhận vai trò iam mới dành cho nhà phát triển bị hạn chế.

1. Đăng nhập vào [AWS Management Console](https://console.aws.amazon.com ) với tư cách là người dùng IAM có bật MFA. 

2. Trong bảng điều khiển, hãy nhấp vào tên người dùng của bạn trên thanh điều hướng ở góc trên bên phải. Nó thường trông như thế này: username@account_ID_number_or_aliassau đó chọn Chuyển đổi vai trò. Ngoài ra, bạn có thể dán liên kết vào trình duyệt mà bạn đã ghi lại trước đó.

3. Trên trang Chuyển đổi vai trò, nhập số ID tài khoản hoặc bí danh tài khoản và tên của vai trò developer-restricted-iam mà bạn đã tạo ở bước trước. (Tùy chọn) Nhập văn bản mà bạn muốn hiển thị trên thanh điều hướng thay cho tên người dùng của bạn khi vai trò này đang hoạt động. Một tên được đề xuất, dựa trên thông tin tài khoản và vai trò, nhưng bạn có thể thay đổi thành bất kỳ tên nào có ý nghĩa với bạn. Bạn cũng có thể chọn màu để làm nổi bật tên hiển thị.

4. Chọn Chuyển đổi vai trò . Nếu đây là lần đầu tiên chọn tùy chọn này, một trang sẽ xuất hiện với nhiều thông tin hơn. Sau khi đọc, hãy chọn Chuyển đổi vai trò . Nếu bạn xóa cookie của trình duyệt, trang này có thể xuất hiện lại.
![swtich_role](/images/3.connect/3.1/10_swtich_role.png)