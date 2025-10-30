---
title: "Đề Xuất"
date: 2025-09-09
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# NỀN TẢNG CHO CÁC KHÓA HỌC TRỰC TUYẾN

### 1. Tóm Tắt Dự Án
Nền tảng FocusLearn là một hệ thống e-learning tiên tiến được thiết kế để cung cấp trải nghiệm học tập có cấu trúc và tính tương tác cao cho khách hàng. Nền tảng có một hệ thống quản trị (backend) toàn diện để tạo khóa học (CRUD), quản lý người dùng và xem xét bài tập, được bổ sung bởi một giao diện người dùng (frontend) lấy người dùng làm trung tâm để đăng ký, mua khóa học và theo dõi tiến độ. Điểm khác biệt chính là chế độ "Focus Mode" tích hợp, giúp người dùng tập trung bằng cách kết hợp bộ đếm thời gian Pomodoro, tích hợp Google Calendar để lên lịch học và một môi trường không bị phân tâm. Hơn nữa, một hệ thống danh sách công việc (to-do list) sáng tạo cho phép người dùng tạo các tác vụ có thể thực hiện được liên kết trực tiếp với các mốc thời gian cụ thể trong video khóa học, với tùy chọn tích hợp AI để tăng cường quản lý tác vụ và củng cố kiến thức.

### 2. Bối Cảnh Vấn Đề
### Vấn đề là gì?
-   **Học Tập Thụ Động và Tương Tác Kém:** Các nền tảng e-learning truyền thống thường thúc đẩy việc tiêu thụ nội dung video một cách thụ động. Học viên xem bài giảng mà không có sự tham gia tích cực, dẫn đến khả năng ghi nhớ thông tin kém và tỷ lệ bỏ dở khóa học cao.
-   **Thiếu Kết Nối Giữa Nội Dung và Hành Động:** Có một sự thiếu kết nối đáng kể giữa tài liệu học tập và các tác vụ có thể thực hiện. Học viên gặp khó khăn trong việc tạo ghi chú hoặc danh sách công việc có tổ chức liên kết trực tiếp trở lại các khái niệm cụ thể trong video, làm cho việc ôn tập trở nên kém hiệu quả và việc áp dụng vào thực tế trở nên khó khăn.
-   **Sự Mất Tập Trung và Quản Lý Thời Gian Kém:** Môi trường học tập kỹ thuật số tràn ngập các yếu tố gây xao lãng. Người học thiếu các công cụ tích hợp để quản lý thời gian học tập hiệu quả, chặn các yếu tố gây gián đoạn và cấu trúc các buổi học để đạt được sự tập trung và năng suất tối ưu, dẫn đến việc học bị phân mảnh và không hiệu quả.

### Giải Pháp
-   FocusLearn được xây dựng trên kiến trúc serverless của AWS để mang lại sự linh hoạt, khả năng mở rộng và hiệu quả về chi phí.
-   Hệ thống tận dụng AWS Amplify, Lambda, API Gateway, DynamoDB, S3, và Cognito để tạo ra một môi trường học tập trực tuyến an toàn, chi phí thấp và hiệu suất cao.
-   Người dùng có thể đăng ký, tham gia các khóa học, quản lý các tác vụ học tập và truy cập các công cụ học tập tương tác—tất cả đều nằm trong một cơ sở hạ tầng cloud-native, khả dụng trên toàn cầu.


### Lợi Ích và Tỷ Suất Hoàn Vốn (ROI)
-   Phương pháp serverless giảm thiểu chi phí vận hành và bảo trì thủ công.
-   Tự động mở rộng quy mô dựa trên hoạt động của người dùng.
-   Sử dụng Gói Miễn phí của AWS và mô hình định giá theo mức sử dụng, giữ chi phí trung bình dưới $100/tháng.
-   Tăng cường sự tương tác và khả năng ghi nhớ thông qua các tính năng năng suất tích hợp.


### 3. Kiến Trúc Giải Pháp

![NỀN TẢNG CHO CÁC KHÓA HỌC TRỰC TUYẾN](/images/2-Proposal/architecture.png)

### Các Dịch Vụ AWS Được Sử Dụng
|       Loại hình       |                  Dịch vụ AWS                   |                          Chức năng                          |
| :-------------------: | :--------------------------------------------: | :---------------------------------------------------------: |
|   Lưu trữ Frontend    |        AWS Amplify hoặc S3 + CloudFront        |   Lưu trữ và phân phối trang web tĩnh (frontend Next.js)    |
|   Tính toán Backend   |                   AWS Lambda                   | Chạy logic API và các chức năng quản lý khóa học serverless |
|      Quản lý API      |               Amazon API Gateway               |       Xử lý các yêu cầu HTTP giữa frontend và backend       |
|     Cơ sở dữ liệu     | Amazon DynamoDB (NoSQL) hoặc Aurora Serverless |   Lưu trữ hồ sơ người dùng, dữ liệu khóa học và giao dịch   |
|  Xác thực người dùng  |                 Amazon Cognito                 |     Quản lý đăng ký, đăng nhập và token của người dùng      |
|    Email/Thông báo    |                Amazon SES / SNS                |  Gửi email xác minh, đặt lại mật khẩu và cảnh báo khóa học  |
|        Lưu trữ        |                   Amazon S3                    |         Lưu trữ video, hình ảnh, tài liệu khóa học          |
|  Phân phối nội dung   |               Amazon CloudFront                |        Tăng tốc độ phân phối nội dung trên toàn cầu         |
|  Giám sát & Bảo mật   |     CloudWatch, IAM, AWS Shield (Standard)     |      Logs, chỉ số, quyền truy cập và bảo vệ chống DDoS      |
| Tên miền & Định tuyến |                    Route 53                    |         Quản lý tên miền tùy chỉnh và chứng chỉ SSL         |

### Thiết Kế Thành Phần
#### 1. Frontend:
-   Xây dựng bằng Next.js và được lưu trữ trên AWS Amplify để triển khai liên tục.
-   Sử dụng CloudFront CDN để truy cập nhanh trên toàn cầu.
#### 2. Backend:
-   REST APIs thông qua API Gateway → kích hoạt các hàm Lambda.
-   Mỗi hàm Lambda xử lý các hoạt động CRUD cho người dùng, khóa học, tiến độ và thanh toán.
#### 3. Cơ sở dữ liệu:
-   DynamoDB lưu trữ dữ liệu người dùng và tiến độ học tập.
-   Aurora Serverless là tùy chọn cho dữ liệu quan hệ như giao dịch.
#### 4. Xác thực người dùng:
-   Cognito quản lý đăng nhập (email/mật khẩu, Google OAuth).
-   Tích hợp với frontend thông qua module Amplify Auth.
#### 5. Lưu trữ:
-   Tài liệu khóa học (video, tài liệu) được lưu trên S3 với các quy tắc vòng đời (Glacier cho dữ liệu cũ).
-   Quyền truy cập được kiểm soát thông qua các URL được ký trước (pre-signed URLs).
#### 6. Giám sát & Ghi log:
-   CloudWatch giám sát việc sử dụng, chi phí và lỗi.
-   Thiết lập AWS Budgets để cảnh báo khi chi phí dưới $100/tháng.


### 4. Lộ Trình Kỹ Thuật
**Các Giai Đoạn Triển Khai**

| Giai đoạn                    |                        Chi tiết Triển khai                        |
| ---------------------------- | :---------------------------------------------------------------: |
| Thiết lập Hạ tầng            |        Cấu hình Amplify, S3, và CloudFront để triển khai.         |
| Triển khai Backend           |       Triển khai Lambda + API Gateway cho các API khóa học.       |
| Cấu hình Cơ sở dữ liệu       | Tạo các bảng DynamoDB cho người dùng, khóa học, và giao dịch mua. |
| Tích hợp Xác thực người dùng |      Thiết lập Cognito cho user pool và liên kết danh tính.       |
| Thiết lập Thông báo          |       Tích hợp SES để xác minh email và cập nhật khóa học.        |
| Giám sát                     |        Cấu hình các dashboard và cảnh báo trên CloudWatch.        |
| Kiểm thử                     |   Thực hiện kiểm thử chức năng và tải cho 10.000 yêu cầu/ngày.    |

### 5. Tiến Độ và Các Mốc Quan Trọng
**Tiến Độ Dự Án**
-   Trước Thực Tập (Tháng 0): 1 tháng để lập kế hoạch và xem xét các dự án cũ.
-   Trong Thực Tập (Tháng 1-3): 3 tháng.
    -   Tháng 1: Nghiên cứu AWS và nâng cấp phần cứng.
    -   Tháng 2: Thiết kế và điều chỉnh kiến trúc.
    -   Tháng 3: Triển khai, kiểm thử và ra mắt.
-   Sau Ra Mắt: Tối đa 1 năm để nghiên cứu.


### 6. Ước Tính Ngân Sách
Bạn có thể xem ước tính ngân sách chi tiết tại [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01).  
Hoặc bạn có thể tải xuống [Tệp Ước Tính Ngân Sách](../attachments/budget_estimation.pdf).

### Chi Phí Hạ Tầng

| Dịch vụ                      |     Chi phí ($)      | Mô tả                        |
| ---------------------------- | :------------------: | ---------------------------- |
| Amplify / S3 + CloudFront    |          5           | Lưu trữ + CDN                |
| API Gateway + Lambda         |          10          | Yêu cầu API & tính toán      |
| DynamoDB / Aurora Serverless |          15          | CSDL khóa học & người dùng   |
| Cognito + SES                |          2           | Xác thực + email             |
| Giám sát / IAM / Route 53    |          5           | Chỉ số, DNS, vai trò         |
| **Trung bình**               |  **≈ $37 / Tháng**   | **Lưu lượng thấp**           |
|                              | **≈ $80–90 / Tháng** | **Lưu lượng trung bình/cao** |


### 7. Đánh Giá Rủi Ro
#### Ma Trận Rủi Ro
-   **Vượt chi phí:** Tác động Trung bình, Xác suất Trung bình.
-   **Suy giảm hiệu năng:** Tác động Trung bình, Xác suất Thấp.
-   **Vi phạm bảo mật:** Tác động Cao, Xác suất Thấp.
-   **Thời gian ngừng hoạt động:** Tác động Trung bình, Xác suất Thấp.
-   **Mất dữ liệu:** Tác động Trung bình, Xác suất Thấp.


#### Chiến Lược Giảm Thiểu
-   **Chi phí:** Sử dụng AWS Budgets và Cảnh báo.
-   **Hiệu năng:** Tự động mở rộng quy mô cho Lambda và DynamoDB.
-   **Bảo mật:** Bật xác thực đa yếu tố (MFA) trên Cognito và nguyên tắc phân quyền tối thiểu (least privilege) trên IAM.
-   **Thời gian ngừng hoạt động:** Sử dụng nhiều Vùng sẵn sàng (Multi-AZ), bộ đệm CDN.
-   **Dữ liệu:** Bật chế độ phiên bản (Versioning) và sao lưu trên S3.


#### Kế Hoạch Dự Phòng
-   Quay lại các phương pháp thủ công nếu AWS gặp sự cố.
-   Sử dụng CloudFormation để hoàn tác các thay đổi liên quan đến chi phí.


### 8. Kết Quả Mong Đợi
#### Cải Tiến Kỹ Thuật: 
-   Nền tảng hoàn toàn serverless, có khả năng mở rộng với chi phí vận hành tối thiểu.
-   Xác thực an toàn và khả năng mở rộng theo thời gian thực.
-   Cải thiện sự tương tác thông qua các công cụ học tập tương tác.

#### Giá Trị Dài Hạn
-   Hoạt động bền vững dưới $100/tháng ở quy mô nhỏ.
-   Hỗ trợ hơn 10.000 yêu cầu hoạt động/ngày.
-   Sẵn sàng cho việc đề xuất khóa học dựa trên AI trong các phiên bản tương lai.
-   Sẵn sàng tích hợp AI để tóm tắt thông tin khóa học.
-   Cải thiện danh sách công việc (to-do list) để ghi chú tại các mốc thời gian cụ thể của video.