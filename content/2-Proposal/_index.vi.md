---
title: "Đề xuất Dự án"
date: 2025-09-09
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Nền tảng SnapResume

## 1. Tóm tắt Dự án

SnapResume là một nền tảng xây dựng hồ sơ năng lực (CV/Resume) thông minh, được hỗ trợ bởi AI, giúp người tìm việc tạo ra các hồ sơ chuyên nghiệp, chuẩn ATS (Applicant Tracking System) một cách nhanh chóng và hiệu quả. Nền tảng cung cấp các mẫu thiết kế hiện đại, công cụ chỉnh sửa trực quan và hệ thống đề xuất thông minh giúp tối ưu hóa nội dung phù hợp với mô tả công việc.

Điểm khác biệt chính là việc tích hợp Công cụ Tìm kiếm & Đề xuất bằng AI sử dụng **AWS Bedrock** (Claude 3 Sonnet), cho phép hệ thống tự động phân tích mô tả công việc và đề xuất các phần hồ sơ phù hợp nhất từ kho dữ liệu kinh nghiệm của người dùng. Hệ thống được xây dựng hoàn toàn trên kiến trúc Serverless, đảm bảo khả năng mở rộng vô hạn và chi phí tối ưu.

## 2. Bài toán Cần giải quyết

### Vấn đề là gì?

*   **Khó khăn trong Trình bày**: Người tìm việc thường mất hàng giờ để định dạng văn bản trong Word hoặc các công cụ thiết kế phức tạp mà vẫn không đạt được vẻ ngoài chuyên nghiệp.
*   **Khó khăn trong chọn lọc thông tin**: Ứng viên thường có nhiều kinh nghiệm nhưng không biết chọn lọc những gì liên quan nhất đến vị trí ứng tuyển cụ thể. Việc gửi một CV "chung chung" cho mọi công ty làm giảm cơ hội trúng tuyển.
*   **Không vượt qua được ATS**: Các CV thiết kế thủ công thường chứa các yếu tố đồ họa hoặc cấu trúc bảng biểu khiến hệ thống quét hồ sơ tự động (ATS) của nhà tuyển dụng không thể đọc được nội dung.

### Giải pháp

SnapResume giải quyết các vấn đề này bằng một ứng dụng web React hiện đại trên nền tảng AWS Serverless.

*   **Trình chỉnh sửa trực quan**: Giao diện kéo thả hoặc điền biểu mẫu đơn giản, xem trước thời gian thực (Real-time Preview).
*   **AI Smart Matcher**: Sử dụng **AWS Bedrock** để phân tích độ phù hợp giữa kinh nghiệm của ứng viên và yêu cầu công việc, từ đó đề xuất danh sách các kỹ năng và dự án nên đưa vào CV.
*   **Chuẩn ATS**: Các mẫu được thiết kế để thân thiện với máy đọc nhưng vẫn đẹp mắt với người đọc.
*   **Quản lý tập trung**: Lưu trữ thư viện các sections và cho phép "lắp ghép" thành nhiều phiên bản CV khác nhau tùy theo nhu cầu.

## 3. Kiến trúc Giải pháp

Hệ thống sử dụng kiến trúc Serverless và Event-driven trên AWS.
![AWS Architecture](/images/2-Proposal/SnapResume.png)

### Tổng quan Kiến trúc

*   **Frontend**: React + Vite + Ant Design (hosting trên Amplify và tăng tốc với CloudFront).
*   **API Layer**: Amazon API Gateway + AWS Lambda (Node.js/TypeScript).
*   **Database**: Amazon DynamoDB lưu trữ User, Resume, Section, Template.
*   **Authentication**: Amazon Cognito (User Pools & Identity Pools).
*   **AI Engine**: Amazon Bedrock (Claude 3 Sonnet) cho các tác vụ phân tích và đề xuất.
*   **Storage**: Amazon S3 để lưu trữ ảnh đại diện, tệp PDF.

## 4. Triển khai Kỹ thuật

### Stack Công nghệ

*   **Frontend**: ReactJS, Ant Design, CSS Modules, html2pdf.js cho việc xuất PDF.
*   **Backend**: NodeJS, TypeScript, Express (chạy trong Lambda).
*   **IaC**: Terraform để quản lý toàn bộ hạ tầng.

### Các Giai đoạn

1.  **Giai đoạn 1: Core Foundation** (Đã hoàn thành)
    *   Thiết lập hạ tầng AWS (Terraform).
    *   Xây dựng Authentication (Cognito).
    *   CRUD cơ bản cho Hồ sơ & Sections (DynamoDB + Lambda).
2.  **Giai đoạn 2: Editor & Templates** (Đã hoàn thành)
    *   Phát triển giao diện Editor Universal (Extension/Web).
    *   Xây dựng hệ thống Template động.
    *   Tính năng xuất PDF (html2pdf.js).
3.  **Giai đoạn 3: AI Integration & Polish** (Đang thực hiện)
    *   Tích hợp Amazon Bedrock cho tính năng "AI Recommendation".
    *   Tối ưu hóa UX/UI (Features Page, Editor Flow).
    *   Extension Integration (Web Clipper flow).

## 5. Ước tính Ngân sách (Chi phí AWS)

Mô hình định giá Serverless giúp chi phí tỉ lệ thuận với mức sử dụng. Chi phí AI tập trung vào việc phân tích dữ liệu đầu vào lớn (Input Tokens).

### Giả định

*   1 Resume "Match" = 1 lần gọi AI (Phân tích JD + Toàn bộ Sections).
*   1 lần gọi AI Analysis = ~2.000 input tokens (JD + Sections) + ~500 output tokens (JSON Result).
*   Giá Bedrock (Claude 3 Sonnet): $3.00/1M input, $15.00/1M output.
*   Chi phí AI/Lần phân tích: ~ $0.0135 (340 VND).

| Dịch vụ             | Mô hình Tính giá | Lưu lượng Thấp (MVP) | Lưu lượng Trung bình |
| :------------------ | :--------------- | :------------------- | :------------------- |
| **Quy mô**          |                  | **< 500 Users/tháng** | **~ 5.000 Users/tháng** |
| Amazon S3           | Lưu trữ          | $0.28                | $0.77                |
| CloudFront          | CDN              | Free Tier               | Free Tier               |
| API GW + Lambda     | Compute          | Free Tier            | $2.80                |
| DynamoDB            | Database         | Free Tier            | $6.25               |
| Cognito             | Auth             | Free Tier            | Free Tier            |
| Amazon Bedrock (AI) | Tokens           | ?               | ?             |
| WAF + Route53       | Security         | $12.60               | $12.60               |
| **Tổng Chi phí / Tháng** |          | **~ $12.88**       | **~ $13.37**     |

## 6. Đánh giá Rủi ro

### Rủi ro Bảo mật & Riêng tư (Cao)

*   **Vấn đề**: Feature Recommendation yêu cầu gửi toàn bộ dữ liệu Sections của user lên Bedrock để phân tích.
*   **Giảm thiểu**:
    *   AWS Bedrock tuân thủ quy định không sử dụng dữ liệu khách hàng để train base model.
    *   Mã hóa dữ liệu tại DynamoDB.

### Rủi ro Chi phí (Trung bình)

*   **Vấn đề**: Người dùng spam nút "Recommend" với JD dài gây tốn token Input lớn.
*   **Giảm thiểu**:
    *   Giới hạn độ dài Input của Job Description.
    *   Quota limits (Ví dụ: 10 lần phân tích/ngày cho tài khoản Free).

#### Rủi ro Kiến trúc (Thấp)

*   **Vấn đề**: Cold start của Lambda làm chậm trải nghiệm người dùng lần đầu.
*   **Giảm thiểu**: Sử dụng Lambda SnapStart (cho Java) hoặc Provisioned Concurrency nếu cần thiết (tuy nhiên Node.js cold start thường khá nhanh).

## 7. Kết quả Dự kiến

*   Sở hữu một nền tảng SaaS hoàn chỉnh cho thị trường tuyển dụng.
*   Giải quyết bài toán "Matching" giữa ứng viên và việc làm thay vì chỉ là công cụ soạn thảo văn bản thuần túy.
*   Tận dụng sức mạnh AI của AWS để tạo giá trị thực tế (Smart Search) thay vì các tính năng "viết hộ" chung chung.




