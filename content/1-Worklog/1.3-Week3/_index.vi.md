---
title: "Worklog Tuần 3"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
* Tiếp tục học tập và tìm hiểu thêm về các dịch vụ của AWS
* Tìm hiểu về dịch vụ EC2
* Làm bài lab03

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                                                                         | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo                                                                                                                                                                                                                |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 2   | - Làm các bài Lab03:<br>&emsp;+ Tạo VPC<br>&emsp;+ Tạo Route Table<br>&emsp;+ Tạo Security Group<br>&emsp;+ Tạo Subnet<br>&emsp;+ Biết về Network Access Control List<br>&emsp;+ Tạo EC2 Intances<br>&emsp;+ Kiểm tra kết nối<br>&emsp;+ Tạo NAT Gateway<br>&emsp;+ Tạo Endpoint kết nối với NAT Gateway<br>&emsp; | 22/09/225    | 22/09/2025      | [Lab03](https://000003.awsstudygroup.com/)                                                                                                                                                                                     |
| 3   | - Học Module 03-01-01: Instance type                                                                                                                                                                                                                                                                 | 23/09/2025   | 23/09/2025      | [Module 03-01-01](https://www.youtube.com/watch?v=e7XeKdOVq40&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=73)   |
| 4   | - Học Module 03-01-02: AMI / Backup / Key Pair                                                                                                                                      | 24/09/2025   | 24/09/2025      |    [Module 03-01-02](https://www.youtube.com/watch?v=yAR6QRT3N1k&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=74)                                                                                                                                                                                                                            |
|5   |               - Học Module 03-01-03: Elastic book store                                                                                                                                                                             | 25/09/2025   | 25/09/2025      | [Module 03-01-03](https://www.youtube.com/watch?v=hKr_TfGP7NY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=75)                                                                                                                                                                                    |
| 6   | - Học Module 03-01-04: Instance Store                                                                                                                                                                                                                                                                                      | 26/09/2025   | 26/09/2025      | [Module 03-01-04](https://www.youtube.com/watch?v=6IHNDJ85aoQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=76)                                                                                                                                                                                              |

### Kết quả đạt được tuần 3:
*   Đã làm và hoàn thành lab03, những gì đã đạt được:
    *   Biết cách tạo VPC, subnet
    *   Cấu hình Route table, Security Group, biết về NACL
    *   Tạo được EC2 Instance và kiểm tra kết nối
        *   Sử dụng MobaXterm
    *   Tạo NAT Gateway và Endpoint kết nối
        *   Đồng thời cũng kiểm tra kết nối Endpoint

 *  Module 03-01-01: Instance Type
    *   Hiểu được Instance type là gì 
    *   Hiểu được các yếu tố của EC2 Instance
    *   Hardware Node
        *   Có tính năng Placement Option
        *   Hypervisor
        *   PV: Paravirtulization
        *   HVM: Hardware Virtual Machine
        *   KVM: Nitro
        *   AZ 
  
*   Module 03-01-02: AMI / Backup / Key
    *   Hiểu được AMI(Amazon Machine Image) là gì
    *   Hiểu được các để backup các EC2 Instance thông qua việc tạo Snapshot
    *   Biết được Keypair là gì và công dụng của nó

*   Module 03-01-03: Elastic book store
    *   Hiểu được EBS là gì
    *   Hiểu được các EBS và EC2 được kết nối với nhau
    *   Biết được EBS có 2 loại đĩa: HDD và SSD
    *   Đã tìm hiểu qua về lí do khiến EBS có thể đạt đến high avaiability 99.999%
    *   Được biết về Optimised EBS Instances
    *   Tính năng EBS Multi attach: EBS có thể được gán vào các EC2 chạy trên Hypervisor Nitro
    *   Back up EBS bằng cách snapshot vào S3 

*   Module 03-01-04: Instance Store
    *   Hiểu được Instance Store là gì
    *   Hiểu được sự khác nhau giữa EBS và Instance Store
    *   Hiểu được sự liên hệ giữa Instance store và EC2
    *   Trường hợp sử dụng của Instance store: dùng khi cần hiệu năng cực cao lên đến hàng triệu IOPS: 
        *   Swap
        *   Paging
        *   Buffer / Cache
        *   Log
