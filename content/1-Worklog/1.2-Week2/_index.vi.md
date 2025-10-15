---
title: "Worklog Tuần 2"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Học xong Module 2
* Hiểu được những gì có trong bài học và chuẩn bị làm lab để hiểu sâu hơn về cách thực hành, vận dụng trong thực tế

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo                                                                                                |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------------------------------------------------------------------------------------------- |
| 2   | -Học Module 02 - 01                                                                                                                         | 15/9/2025    | 15/9/2025       | [Module 02 - 01](https://www.youtube.com/watch?v=O9Ac_vGHquM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=26) |
| 3   | -Học Module 02 - 02                                                                                                                         | 16/9/2025    | 16/9/2025       | [Module 02 - 02](https://www.youtube.com/watch?v=BPuD1l2hEQ4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=26) |
| 4   | -Học Module 02 - 03                                                                                                                         | 17/9/2025    | 17/9/2025       | [Module 02 - 03](https://www.youtube.com/watch?v=CXU8D3kyxIc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=27) |
| 5   | Tìm hiểu thêm về các dịch vụ VPC <br>&emsp;+ VPC <br>&emsp;+ Subnet <br>&emsp;+ Route Table <br>&emsp;+ Elastic IP <br> &emsp;+ Nat Gateway | 18/9/2025    | 18/9/2025       |                                                                                                                |
| 6   | Em có việc bận ngày này ạ                                                                                                                   | 19/9/2025    | 19/9/2025       |                                                                                                                |

### Kết quả đạt được tuần 2:

* Đã tìm, học và hiểu về VPC 
  * Mục đích chính của việc sử dụng VPC là thường dùng để phân tách môi trường.

* Hiểu thêm về subnet
  * Public subnet, private subnet
  * VPC cho phép tạo ra nhiều mạng ảo và chia các mạng ảo thành mạng con (được gọi là subnet)
  * Biết được về 5 địa chỉ IP trong mỗi subnet

* Đã tìm hiểu qua về bảng định tuyến (route table):
  * Hiểu được bảng định tuyến là gì
  * Hiểu được về Default Route Table, và Custom Route Table
  * Hiểu được cơ bản là cần phải thiết lập Custom Route Table để cho các máy chủ có thể kết nối với Internet bên ngoài

* Hiểu về Elastic Network Interface (ENI):
  * Hiểu được cơ bản về ENI: khi tạo hoặc bật máy chủ trong VPC, mỗi máy chủ được cấp 1 địa chỉ tài nguyên không được gắn trực tiếp vào tài nguyên máy chủ, mà được gắn vào các card mạng Elastic Network Interface.
  * ENI là 1 card mạng ảo có thể chuyển sang các EC2 Instance khác

* Hiểu về Elastic IP Address (EIP):
  * Hiểu được cơ bản về EIP: là 1 địa chỉ IPv4 tĩnh
  * Và khi không được sử dụng EIP sẽ charge phí -> cần chú ý khi làm việc có liên quan đến EIP để tránh trường hợp trừ tiền oan

* Hiểu về VPC Endpoint:
  * Hiểu được các khái niệm cơ bản về chúng
  * Hiểu về 2 loại Endpoint:
    * Interface Endpoint
    * Gateway Endpoint

* Hiểu về Internet Gateway và NAT Gateway
  * Hiểu được các khái niệm cơ bản của Internet Gateway: giúp cho các máy chủ có thể kết nối ra ngoài Internet
  * Hiểu được NAT Gateway là gì
  * Điểm khác biệt giữa NAT Gateway và Internet Gateway là:
    * NAT Gateway chỉ nhận kết nối chiều ra và không nhận kết nối chiều vào
    * Khi tạo bảng định tuyến (custom route table) thì 
      * Internet Gateway: Destination - Target của nó là địa chỉ <public ID của Public Subnet> - <địa chỉ Internet> (id của Internet Gateway)
      * NAT Gateway: Destination của NAT Gateway được đặt trong public subnet nối với ID 0.0.0.0/0, nhưng Target của NAT Gateway là igw-id -> NAT Gateway thường dùng để cho các máy chủ trong môi trường Private Subnet kết nối ra được bên ngoài Internet.

* Hiểu về Security Hub và Network Access Control List (NACL)
  * 

* Đã đọc và tìm hiểu thêm về các dịch vụ VPC để biết cách sử dụng và quản lí chúng trong các dự án thực tế

