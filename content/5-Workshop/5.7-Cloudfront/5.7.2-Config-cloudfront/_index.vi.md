---
title : "Cấu hình Cloudfront"
date: 2025-09-09
weight : 2
chapter : false
pre : " <b> 5.7.2 </b> "
---

Sử dụng bảng điều khiển quản lý AWS để tạo **CloudFront distribution** và cấu hình dịch vụ này phục vụ **s3 Bucket** mà chúng ta đã tạo trước đó.

1. Mở bảng điều khiển CLoudfront
    -   Ở AWS Console, tìm kiếm **CloudFront**

    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/1.png)

    Từ bảng điều khiển, nhấn vào Create a CloudFront distribution.
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/2.png)

2. Cấu hình Cloudfront
    -   Trong giao diện chọn kế hoạch, chọn **Free plan**
    -   Chọn Next
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/3.png)

    -   Distribution name: để tên tùy chỉnh (hoặc `workshop-demo`)
    -   Distribution type: chọn **Single website or app**
    -   Chọn Next
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/4.png)

    - Ở trang Specify Origin
        -   Origin type: chọn **Amazon S3**
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/5.png)
         -   Origin: chọn **S3 bucket** đã tạo 
         -  Nhấn **Choose**
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/6.png)
        -   Sau đó nhấn Next
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/7.png)
        -   Tiếp tục Next
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/8.png)
        -   Kiểm tra lại cấu hình, và sau đó chọn **Create distribution**
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/9.png)

Sau đó đợi chờ vài phút để Cloudfront khởi tạo

![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/10.png)

Qua S3, vào **Permissions** và kéo xuống tìm **Bucket policy**
![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/11.png)


#### Optional: Nếu không hoạt động thì thử các cách sau:
1. Tắt Host static website của S3
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/12.png)  
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/13.png)   
2. Sau đó vào cấu hình Cloudfront
    -   Nhấp vào **ID** Cloudfront
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/14.png)

    -   Trong **General**, chọn **Edit**
    -   Thêm `index.html` vào **Default root object**
    -   Sau đó chọn **Save changes**
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/15.png)

Sau đó chờ thêm vài phút để Cloudfront khởi tạo lại, và thử mở lại URL trong trang mới (hoặc trình duyệt mới)
    ![CloudFront](/static/images/5-Workshop/5.7-Cloudfront/5.7.2-Config-Cloudfront/16.png)
