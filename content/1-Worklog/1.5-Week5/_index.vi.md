---
title: "Worklog Tuần 5"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Học Module 04
* Làm lab10
* Dịch blog nộp bài


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                               | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo                                                                                                                                                                                                               |
| --- | --------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | - Học Module 04-01: Dịch vụ lưu trữ đám mây <br>- Học Module 04-02: Amazon Simple Storage Service ( S3 ) - Access Point - Storage Class                                                               | 06/10/2025   | 06/10/2025      | [Module 04 - 01](https://www.youtube.com/watch?v=hsCfP0IxoaM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=103) & [Module 04 - 02](https://www.youtube.com/watch?v=_yunukwcAwc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=104)<br>                                                                                                                                   |
| 3   | - Học Module 04 - 03: S3 Static Website & CORS - Control Access - Object Key & Performance - Glacier | 07/10/2025   | 07/10/2025      | [Module 04 - 03](https://www.youtube.com/watch?v=mPBjB6Ltl_Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=105)                                                                                                                                                                                    |
| 4   | - Làm lab10                                                                        | 08/10/2025   | 08/10/2025      | [Lab10](https://000010.awsstudygroup.com/)                                                                                                                                                                                    |
| 5   | - Dịch blog AWS                                                                  | 09/10/2025   | 09/10/2025      |                                                                                                                                                                                                                               |
| 6   | - Tiếp tục dịch blog và nộp bài dịch blog                           | 10/10/2025   | 10/10/2025      |  |


### Kết quả đạt được tuần 5:

* Module 04 - 01: Dịch vụ lưu trữ đám mây
  * Bước đầu vào tìm hiểu về dịch vụ S3 và các dịch vụ liên quan như:
    * Amazon Storage Gateway
    * Snow Family
    * Disaster Recovery on AWS
    * AWS backup

* Module 04 - 02: Amazon Simple Storage Service ( S3 ) - Access Point - Storage
  * Tìm hiểu về dịch vụ S3
  * Hiểu về khái niệm Access Point
  * Tìm hiểu về các class lưu trữ của S3:
    * S3 Standard
    * S3 Standard IA
    * S3 Intelligence Tiering
    * S3 One Zone IA
    * S3 Glacier / Deep Archive
  
* Module 04 - 03: S3 Static Website & CORS - Control Access - Object Key & Performance - Glacier
  * Hiểu về cách S3 host static website 
  * Hiểu về khái niệm Single Page Application:
  * Controll Access vào S3:
    * Dùng S3 Access Control List
    * Dùng S3 Bucket policy
    * Dùng IAM Policy
  * Tìm hiểu về 2 tính năng của S3:
    * Endpoint
    * Versioning
  * Hiểu được các S3 lưu trữ dữ liệu 
    * Object key
    * Partitioning sâu bên trong s3 để lưu trữ dữ liệu, khi dữ liệu lưu trữ tăng thì partition sẽ tự chia ra tự động để lưu trữ, gián tiếp làm giảm hiệu năng S3
  * Tối ưu hóa hiệu năng S3 bằng random prefix: lưu trữ ở trên nhiều partitions nhất có thể
  * Tìm hiểu về Glacier

* Đã làm bài lab10, những gì đạt được
  * Được tìm hiểu qua dịch vụ CloudFormation của AWS
  * Thực hành tạo template, cấu hình lại SG, và kết nối với EC2 Instance bằng Remote Desktop Gateway Server (RDGW)
  * Thực hành tạo Directory Service
  * Tìm hiểu về Route 53
    * Tạo Outbound rule cho Route53
    * Tạo Resolver Rules
    * Tạo Inbound Rule cho Route 53
  * Sau đó kiểm tra kết nối thành công
  * Đã thực hiện được kết nối giữa môi trường on-premise đến với môi trường AWS qua Directory Service và Remote Desktop Gateway Server

