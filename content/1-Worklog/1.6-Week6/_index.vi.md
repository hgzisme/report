---
title: "Worklog Tuần 6"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Tiếp tục học Module 04
* Học Module 05
* Chuẩn bị thực hành các bài lab 

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Học Module 04 - 04: Snow Family - Storage Gateway - Backup                                                                                             | 13/10/2025   | 13/10/2025      | [Module 04 - 04](https://www.youtube.com/watch?v=YXn8Q_Hpsu4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=106) |
| 3   |   - Học Module 05 - 01: Share Responsibility Model <br> - Học Module 05 - 02: Amazon Identity and Access management                                          | 14/10/2025   | 14/10/2025      | [Module 05 - 01](https://www.youtube.com/watch?v=tsobAlSg19g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=150) <br> [Module 05 - 02](https://www.youtube.com/watch?v=N_vlJGAqZxo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=151)  |
| 4   | - Học Module 05 - 03:  Amazon Cognito <br> - Học Module 05 - 04: AWS Organization | 15/10/2025   | 15/10/2025      | [Module 05 - 03](https://www.youtube.com/watch?v=pZ2fgEFK3Vs&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=152) <br> [Module 05 - 04](https://www.youtube.com/watch?v=5oQY8Rogz9Y&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=153) |
| 5   | - Sửa dịch blog và nộp bổ sung bài dịch còn thiếu <br>- Học Module 05 - 05: AWS Identity Center (SSO) <br> - Học Module 05 - 06: Amazon Key Management Service               | 16/10/2025   | 16/10/2025      | [Module 05 - 05](https://www.youtube.com/watch?v=NW1xrMkNMjU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=154) <br> [Module 05 - 06](https://www.youtube.com/watch?v=GMihNQojhZc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=155)  |
| 6   |    - Học Module 05 - 07: AWS Security Hub <br> - Học Module 05 - 08: Hands-on and Additional research                                                              | 17/10/2025   | 17/10/2025      | [Module 05 - 07](https://www.youtube.com/watch?v=clj2E0rNBEs&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=156) <br> [Module 05 - 08](https://www.youtube.com/watch?v=0SdpD2GPYz4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=157) |


### Kết quả đạt được tuần 6:
* Module 04 - 04: Snow Family - Storage Gateway - Backup
    *   Tìm hiểu được về Snow Family:
        *   Snowball
        *   Snowball Edge
        *   Snowmobile 
    *   Tìm hiểu về Storage Gateway: một giải pháp lưu trữ Hybrid, kết hợp giữa việc lưu trữ trên môi trường truyền thống on-premise và môi trường cloud AWS
        *   File Gateway: lưu trữ và truy xuất đối tượng trong S3 bằng Network File Sharing (NFS) và Server Managing Block (SMB)
        *   Volume Gateway: sử dụng giao thức iSCSI để lưu trữ dữ liệu dạng khối trên S3, truy cập bằng EBS snapshot (tự động bằng AWS Backup) từ đó tạo thành EBS Volums
        *   Tape Gateway: cung cấp cho ứng dụng sao lưu 1 giao hiện thư viện băng từ ảo (Virtual Tape Library) iSCSI, dữ liệu tape ảo được lưu trữ trong Amazon S3 hoặc Amazon Galicer
    *   Học về Storage Gateway 
    *   Tìm hiểu về Disaster Recovery
        *   Recovery Time Object (RTO) Thời gian ngắn nhất khôi phục một dịch vụ trở lại
        *   Recovery Point Object (RPO) Thời gian tối đa mà ta chấp nhận dữ liệu bị mất
    *   Tìm hiểu về 4 chiến lược khôi phục
        *   Sao lưu và khôi phục
        *   Pilot Light (Active - Standby)
        *   Low capacity Active - Active
        *   Full capacity Active - Active
    *   Tìm hiểu về AWS Backup: 
        *   Là một dịch vụ quản lý các tác vụ sao lưu
        *   Có thể được cấu hình và lập lịch (backup schedule)
        *   Có chính sách sao lưu (backup retention)
        *   Giám sát các hoạt động sao lưu cho các tài nguyên trên AWS như EBS, EC2, Amazon RDS, Amazon DynamoDB, Amazon EFS, AWS Storage Gateway Volumes

* Module 05 - 01: Share Responsibility Model
    *   Tìm hiểu về mô hình chia sẻ trách nhiệm 
    *   Tùy vào từng loại hình dịch vụ, trách nhiệm bảo mật sẽ khác nhau:
        *   Các dịch vụ ở mức hạ tầng => của khách hàng
        *   Các dịch vụ quản lý ở mức kết hợp => của cả khách hàng và AWS
        *   Các dịch vụ quản lý hoàn toàn bởi AWS 

* Module 05 - 02: Amazon Identity and Access management
    *   Tìm hiểu sau hơn về dịch vụ IAM, hiểu và nắm được khái niệm của IAM User, Group, Role, Policy (Identity based policy và Resource based policy)  

* Module 05 - 03:  Amazon Cognito
    *   Hiểu được công dụng của Cognito: giúp xác thực, cấp phép và quản lí người dùng
    *   Hiểu được 2 thành phần chính của Cognito:
        *   User Pool: Là thư mục người dùng cung cấp các tùy chọn đăng kí và đăng nhập
        *   Identity Pool: Cung cấp cho người dùng quyền đăng nhập vào các dịch vụ AWS khác
        *   Kết hợp giữa User Pool và Identity Pool để truy cập trực tiếp vào các dịch vụ của AWS

* Module 05 - 04: AWS Organization
    *   Tìm hiểu về AWS Organization
        *   Hiểu về Organization Unit (có thể tạo tài khoản AWS mới và phân bổ tài nguyên, sắp xếp các AWS account), Consolidated Billing
        *   Service Control Policies (SCP)
            *   Có thể áp dụng lên các OU, AWS Account
            *   SCP chỉ giới hạn quyền tối đa cho các IAM User hoặc IAM Role trong OU hoặc AWS Account được gán 
            *   Cho phép thiết lập deny-based policy

* Module 05 - 05: AWS Identity Center (SSO)
    *   Tìm hiểu về AWS Identity Center
    *   Biết về khái niệm Permission Set: là khả năng truy cập mà User và Group có đối với các tài khoản AWS trong AWS Organization

* Module 05 - 06: Amazon Key Management Service
    *   Tìm hiểu về dịch vụ mã hóa dữ liệu KMS
        *   Customer Managed Key (CMK)
        *   Data Key : Loại khóa được dùng bên ngoài AWS KMS để mã hóa dữ liệu

* Module 05 - 07: AWS Security Hub
    *   Tìm hiểu về Security Hub và các tính năng của nó
    *   Security Hub chạy liên tục, kiểm tra cấu hình dịch vụ và kiểm tra bảo mật dựa trên các best practice của AWS




