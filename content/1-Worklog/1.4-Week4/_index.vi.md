---
title: "Worklog Tuần 4"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Hoàn thành Module 3
* Hoàn thành lab07 và lab09

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc       | Ngày bắt đầu | Ngày hoàn thành | Nguồn tham khảo |
|-----|-----------------|--------------|-----------------|-----------------|
| 2   | - Học Module 03-01-05: User Data | 29/09/2025   | 29/09/2025      |  [Module 03-01-05](https://www.youtube.com/watch?v=_v_43Wi7zjo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=77)               |
| 3   | - Học Module 03-01-06: Meta Data | 30/09/2025   | 30/09/2025      |   [Module 03-01-06](https://www.youtube.com/watch?v=Ew3QRaKJQSA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=78)              |
| 4   | - Học Module 03-01-07: EC2 Auto Scaling | 1/09/2025    | 1/09/2025       |  [Module 03-01-07](https://www.youtube.com/watch?v=bbLcPitXJSY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=79)               |
| 5   | - Học Module 03-02: EC2 Autoscaling - EFS/FSx - Lightsail - MGN | 2/09/2025    | 2/09/2025       |     [Module 03-02](https://www.youtube.com/watch?v=hFVYG8WqfU0&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=80)            |
| 6   | - Làm lab 07 <br>- Làm lab 09  | 3/09/2025    | 3/09/2025       |  [Lab07](https://000007.awsstudygroup.com/vi/) <br> [Lab09](https://000009.awsstudygroup.com/vi/)               |


### Kết quả đạt được tuần 4:
*   Module 03-01-05: User Data
    *   Hiểu được khái niệm về User Data
    *   Tùy thuộc vào hệ điều hành sẽ có các cách sử dụng khác nhau
        *   bash shell script (Linux)
        *   powershell (Windows)

*   Module 03-01-06: Meta Data
    *   Hiểu được khái niệm về Meta data
    *   Dùng thông tin EC2 Meta data để thiết lập hostname cho EC2 Instance Linux với EC2 User data 

*   Module 03-01-07: EC2 Auto Scaling
    *   Hiểu được tính năng EC2 Auto Scaling
    *   Sử dụng với điều kiệm cụ thể (scaling policy)
    *   Các ý chính của EC2 Auto Scaling:
        *   Hỗ trợ tăng giảm số lượng EC2 Instace
        *   Tự đăng kí EC2 Instance vào Elastic Load Balancer (ELB)
        *   Có thể hoạt động trên nhiều AWS AZ
        *   Có nhiều Pricing Option khác nhau

*   Module 03-02: EC2 Autoscaling - EFS/FSx - Lightsail - MGN
    *   Xem qua về sơ đồ kiến trúc khi áp dụng EC2 Auto Scaling
    *   Tìm hiểu về các Pricing Options khác nhau:
        *   On-demand
        *   Reserved Instance
        *   Saving plans
        *   Spot Instance
    *   Tìm hiểu về Lightsail, sự khác nhau giữa Lightsail Instance và EC2 Instance
        *   Lightsail chạy trong 1 VPC đặc biệt, có thể kết nối tới VPC thông thường thông qua tính năng VPC Peering
        *   Xem qua về sơ đồ kiến trúc của Lightsail
    *   Tìm hiểu về EFS/FSX
        *   Hiểu được khái niệm về EFS
            *   Biết được về khái niệm NFSv4 Network Volume
            *   Xem qua sơ đồ kiến trúc của EFS
        *   Hiểu được về khái niệm FSX
            *   Biết được về khái niệm NTFS, Server Message Box (SMB), tính năng deduplication của FSX
            *   Xem sơ qua về sơ đồ kiến trúc của FSX
    *   Tìm hiểu về AWS Application Migration Service (MGN)
        *   Hiểu về MGN và mục đích sử dụng của nó
        *   Xem qua về sơ đồ kiến trúc của AWS MGN
