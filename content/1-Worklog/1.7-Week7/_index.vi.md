---
title: "Worklog Tuần 7"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Hoàn thành Module 06
* Làm lab19 & Lab53

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|--------------------|
| 2   |  - Học Module 06 - 01: Database Concepts review   | 20/10/2025 | 20/10/2025      |   [Module 06 - 01](https://www.youtube.com/watch?v=OOD2RwWuLRw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=217)                |
| 3   |    - Học Module 06 - 02: Amazon RDS & Amazon Aurora   | 21/10/2025 | 21/10/2025      |   [Module 06 - 02](https://www.youtube.com/watch?v=qbrobQZrokY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=218)                 |
| 4   |    - Học Module 06 - 03: Redshift - Elasticache  | 22/10/2025 | 22/10/2025      |  [Module 06 - 03](https://www.youtube.com/watch?v=UvdiRW34aNI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=219)                 |
| 5   |  - Làm Lab19: VPC Peering   | 23/10/2025 | 23/10/2025      |  [Lab19](https://000019.awsstudygroup.com/vi/1-introduce/)               |
| 6   |  - Làm Lab57: Khởi đầu với Amazon S3   | 24/10/2025 | 24/10/2025      |   [Lab57](https://000057.awsstudygroup.com/vi/1-introduce/)                |

### Kết quả đạt được tuần 7:

* Module 06 - 01: Database Concepts review
  * Đã ôn tập lại về các khái niệm trong database
    * PK, FK, Database Log, ...
    * Làm quen với các khái niệm mới như Index, Partitions, Execution Plan - Query Plan, Buffers
  * Bước đầu tìm hiểu về Online Transaction Processing (OLTP) và Online Analytical Processing (OLAP)
    * OLTP: trọng tâm là xử lí nhanh, cơ sở dữ liệu được đọc và ghi thường xuyên, logic hệ thống đảm bảo tính toàn vẹn dữ liệu
    * OLAP: trọng tâm là thời gian phản hồi cho các truy vấn phức tạp, áp dụng cho 1 lượng lớn dữ liệu, kết hợp với kho dữ liệu (data warehouse) có thể cung cấp cho nhà phân tích khả năng sử dụng công cụ báo cáo tùy chỉnh để biến dữ liệu thành thông tin 

* Module 06 - 02: Amazon RDS & Amazon Aurora
  * Tìm hiểu về Amazon RDS
    * Được quản lí bởi AWS
    * Có các tính năng như 
      * Tự động sao lưu
      * Tạo bản sao chỉ đọc (Read Replica) phục vụ cho các Read Workload (Reporting)
      * Read Replica có thể tách rời thành 1 Primary Node
      * Mã hóa dữ liệu at rest và in transit
      * Tự động tăng dung lượng lưu trữ (Storage Auto scaling)
      * Thay đổi quy mô (instance size)
    * Có thể chạy với cơ chế tự động fail over, hay còn được gọi là Multi AZ
    * Dùng cho các ứng dụng OLTP
  * Tìm hiểu về Amazon Aurora
    * Là cơ sở dữ liệu được tối ưu tại hạ tầng lưu trữ bên dưới, cho hiệu năng đọc và ghi song song cao
    * Có các tính năng như 
      * Back Track - Phục hồi DB về thời điểm trước đó
      * Clone - Tạo bản sao
      * Glabal Database
      * Multi Master
    * Aurora phân loại và gom các dữ liệu liên quan (Clustering) nằm trong nhiều AZ

* Module 06 - 03: Redshift - Elasticache
  * Học và tìm hiểu về dịch vụ data warehouse Redshift
    * Lõi là Postgre SQL, được tối ưu cho OLAP
    * Sử dụng kiến trúc Masive-Parallel Processing (MPP) Database
    * Dữ liệu được chia (partition) và lưu trữ tại Compute node
    * Leader node điều phối và tổng hợp truy vấn
    * Lưu trữ data dưới dạng **columnar storage**
    * Dùng SQL và các driver JDBS, ODBC
    * Hỗ trợ các tính năng tối ưu hóa chi phí 
      * Transient cluster
      * Redshift spectrum - Dữ liệu không cần phân tích nhiều thì sẽ được đẩy ra khỏi compute node và được lưu vào S3
  * Học và tìm hiểu về ElastiCache
    * Hỗ trợ 2 engine: Redis và Memcached
    * Được đặt trước cơ sở dữ liệu để cache dữ liệu, giảm tải cho lớp cơ sở dữ liệu
    * Dùng ElastiCache thì phải viết và quản lý caching logic trên ứng dụng

* Lab19: VPC Peering
  * Đã thực hiện tạo Cloudfront Template, cấu hình SG, và tạo 2 máy chủ EC2
  * Tạo Peer Connection giữa 2 VPC, và cấu hình Route Table để SSH tới máy chủ 
  * Đã ping thành công sau khi tạo VPC Peering

* Lab57: Amazon S3
  * Đã làm quen được với việc tạo bucket, lưu/xóa/chuyển dữ liệu trong S3
  * Tìm hiểu về Bucket ACL, Bucket Policy, Bucket Versioning
  * Thực hiện host static website trên S3
  * Thực hiện tăng tốc host static website bằng CloudFront
  * Thực hiện sao chép dữ liệu S3 Object sang region khác
