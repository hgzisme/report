---
title: "Event 8"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 4.8. </b> "
--- 

# Bài thu hoạch sự kiện: Building Agentic AI & Context Optimization with Amazon Bedrock

### Mục đích của Sự kiện
- **Khám phá Kiến trúc Agentic AI**: Cung cấp cái nhìn toàn diện về xu hướng AI Agent (AI đại diện/tác nhân), chuyển dịch từ các mô hình ngôn ngữ lớn (LLM) thụ động sang các hệ thống AI chủ động có khả năng thực thi tác vụ.
- **Làm chủ Amazon Bedrock Agents**: Hiểu sâu về dịch vụ cốt lõi của AWS giúp xây dựng và triển khai các Agent an toàn, có khả năng kết nối dữ liệu và thực hiện hành động.
- **Kỹ thuật Điều phối Nâng cao (Advanced Orchestration)**: Học hỏi các kỹ thuật chuyên sâu (Level 300) về việc điều phối nhiều Agent và tối ưu hóa ngữ cảnh (Context Optimization) để giải quyết các bài toán phức tạp.
- **Thực hành Triển khai (Hands-on)**: Trải nghiệm thực tế quy trình xây dựng một Agentic Workflow từ ý tưởng đến triển khai thông qua phần CloudThinker Hack.

### Danh sách Diễn giả
- Nguyen Gia Hung - Head of Solutions Architect (AWS)
- Kien Nguyen - Solutions Architect (AWS)
- Viet Pham - Founder & CEO
- Thang Ton - Co-Founder & COO (CloudThinker)
- Henry Bui - Head of Engineering (CloudThinker)
- Kha Van - Community Leader

### Nội dung chính & Điểm nổi bật

#### Nền tảng Công nghệ: AWS Bedrock Agent Core
- **Trọng tâm**: Phiên này đặt nền móng kỹ thuật, giải thích cách Amazon Bedrock Agent hoạt động như một lớp cầu nối giữa LLM, nguồn dữ liệu (Knowledge Bases) và các hành động (Action Groups).
- **Nội dung**:
    - Cách Bedrock Agent phân tích yêu cầu của người dùng, lập kế hoạch (Chain of Thought) và gọi các API cần thiết để thực thi.
    - Sự khác biệt giữa RAG (Retrieval-Augmented Generation) thông thường và Agentic Workflow (RAG + Action).
- **Điểm nhấn chính**: Khả năng của Bedrock trong việc quản lý bộ nhớ và ngữ cảnh hội thoại mà không cần xây dựng hạ tầng phức tạp, giúp đơn giản hóa đáng kể quá trình phát triển Agent.

#### Ứng dụng Thực tế: Xây dựng Agentic Workflow
- **Trọng tâm**: Chuyển từ lý thuyết sang thực tiễn với các Use Case cụ thể.
- **Nội dung**:
    - Quy trình tư duy để thiết kế một luồng công việc cho Agent: Xác định mục tiêu -> Xác định công cụ -> Thiết kế luồng xử lý.
    - Demo cách một Agent giải quyết vấn đề nghiệp vụ cụ thể (ví dụ: tự động hóa quy trình CSKH hoặc xử lý đơn hàng) thay vì chỉ trả lời câu hỏi.
- **Điểm nhấn chính**: Sự minh chứng rõ ràng rằng AI hiện nay không chỉ để "chat" mà là để "làm việc" (Doers, not just Talkers).

#### Chuyên sâu Kỹ thuật: Orchestration & Context Optimization (L300)
- **Trọng tâm**: Đây là phần kỹ thuật sâu nhất (Level 300) do đội ngũ Engineering của CloudThinker trình bày, tập trung vào việc giải quyết các hạn chế của Agent đơn lẻ.
- **Nội dung**:
    - **Multi-Agent Orchestration**: Cách điều phối một "đội quân" các Agent, mỗi Agent chuyên trách một nhiệm vụ (ví dụ: 1 Agent tra cứu, 1 Agent tính toán, 1 Agent tổng hợp) để xử lý các yêu cầu phức tạp.
    - **Context Optimization**: Các kỹ thuật để giữ cho ngữ cảnh hội thoại luôn sạch, chính xác và không bị "trôi" (hallucination) khi hội thoại kéo dài hoặc khi chuyển giao giữa các Agent.
- **Điểm nhấn chính**: Tư duy về "CloudThinker Agentic Orchestration" mở ra hướng đi cho việc xây dựng các hệ thống AI cấp doanh nghiệp bền vững và chính xác cao.

#### Thực hành: CloudThinker Hack
- **Trọng tâm**: Phiên workshop thực hành (Hands-on) để người tham dự tự tay xây dựng sản phẩm.
- **Nội dung**: Hướng dẫn từng bước (step-by-step) để khởi tạo môi trường, cấu hình Bedrock Agent, viết Lambda function cho Action Group và tích hợp vào ứng dụng.
- **Kết quả**: Người tham dự có thể thấy một Agent hoạt động ngay tại lớp học.

### Những gì bạn đã học được

#### Về Kiến trúc Agentic AI
- **Sự chuyển dịch tư duy**: Bạn đã hiểu rằng Agentic AI không chỉ là viết prompt cho ChatGPT. Nó đòi hỏi tư duy kiến trúc hệ thống: làm sao để AI biết khi nào cần dùng công cụ gì và làm sao để kiểm soát đầu ra của nó.
- **Sức mạnh của Orchestration**: Bạn đã học được rằng đối với các tác vụ phức tạp, một Agent "biết tuốt" không hiệu quả bằng một hệ thống gồm nhiều Agent chuyên biệt được điều phối nhịp nhàng.

#### Về Công cụ & Kỹ năng
- **Amazon Bedrock Mastery**: Nắm vững cách cấu hình Agent, Knowledge Base và Action Group trên AWS console.
- **Tối ưu hóa Ngữ cảnh**: Học được các chiến lược để quản lý context window hiệu quả, giúp tiết kiệm chi phí token và tăng độ chính xác của câu trả lời.

#### Về Khả năng Ứng dụng
- **Design Patterns**: Nắm bắt được các mẫu thiết kế (design patterns) phổ biến khi xây dựng ứng dụng AI cho doanh nghiệp, từ khâu tra cứu dữ liệu nội bộ đến thực thi hành động trên các hệ thống ERP/CRM.

### Trải nghiệm tại Sự kiện
Sự kiện "A Comprehensive Journey through Agentic AI" là một hành trình trọn vẹn, đi từ bức tranh lớn (High-level architecture) đến từng dòng code (Hands-on implement). Sự kết hợp giữa nền tảng hạ tầng mạnh mẽ của AWS và kinh nghiệm triển khai thực chiến chuyên sâu từ CloudThinker mang lại giá trị rất lớn. Đặc biệt, phiên Level 300 về Orchestration đã giải đáp được nhiều thắc mắc về cách làm sao để AI hoạt động ổn định trong môi trường Production, thay vì chỉ là các bản demo thử nghiệm.
