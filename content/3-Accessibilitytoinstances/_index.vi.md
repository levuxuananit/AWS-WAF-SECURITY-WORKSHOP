---
title : "Quản lý danh tính và truy cập"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
### Giới thiệu
Để sử dụng dịch vụ AWS, bạn phải cấp cho người dùng và ứng dụng quyền truy cập vào tài nguyên trong tài khoản AWS của mình. Khi bạn chạy nhiều khối lượng công việc hơn trên AWS, bạn cần quản lý danh tính và quyền mạnh mẽ để đảm bảo rằng đúng người có quyền truy cập vào đúng tài nguyên trong đúng điều kiện.

### Nội dung
- [Giới hạn quyền IAM ủy quyền tạo vai trò](./3.1-IAMPermissionBoundariesDelegatingRoleCreation/)
- [Kiểm soát truy cập dựa trên thẻ IAM cho EC2](./3.2-IAMTagBasedAccessControlForEC2/)
- [Triển khai tự động các nhóm và vai trò IAM](./3.3-AutomatedDeploymentOfIAMGroupsAndRoles/)
- [Lambda Cross Account sử dụng chính sách Bucket](./3.4-LambdaCrossAccountUsingBucketPolicy/)
- [Dọn dẹp người dùng IAM tự động](./3.5-AutomatedIAMUserCleanup/)
- [Giả định vai trò IAM của tài khoản chéo Lambda](3.6-LambdaCrossAccountIAMRoleAssumption/)