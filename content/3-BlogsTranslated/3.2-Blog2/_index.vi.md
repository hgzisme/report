---
title: "Blog 2"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# KINEXON và AWS Tiên phong trong Công nghệ Theo dõi Vận động viên được Thiết kế riêng cho Thể thao Nữ

bởi Tiến sĩ Simone Kreyer, Frank Mullerat, Jana Hubel, và Bailey Thompson | vào ngày 22 tháng 3 năm 2024 | trong [các chuyên mục Phân tích](https://aws.amazon.com/blogs/apn/category/analytics/), [Giải pháp cho Khách hàng](https://aws.amazon.com/blogs/apn/category/post-types/customer-solutions/), [Đa dạng](https://aws.amazon.com/blogs/apn/category/diversity-equity-inclusion/), [Công bằng và Hòa nhập](https://aws.amazon.com/blogs/apn/category/diversity-equity-inclusion/), [Nền tảng (100)](https://aws.amazon.com/blogs/apn/category/learning-levels/foundational-100/), [Các ngành công nghiệp](https://aws.amazon.com/blogs/apn/category/industries/), [Internet vạn vật](https://aws.amazon.com/blogs/apn/category/internet-of-things/), [Quản lý & Quản trị](https://aws.amazon.com/blogs/apn/category/management-and-governance/), [Công cụ quản lý](https://aws.amazon.com/blogs/apn/category/management-tools/), [Truyền thông & Giải trí](https://aws.amazon.com/blogs/apn/category/industries/entertainment/), [Thể thao](https://aws.amazon.com/blogs/apn/category/industries/sports/), [Lãnh đạo tư tưởng](https://aws.amazon.com/blogs/apn/category/post-types/thought-leadership/), [Liên kết cố định](https://aws.amazon.com/blogs/apn/kinexon-and-aws-are-pioneering-player-tracking-technology-tailored-for-womens-sports/), [Bình luận](https://aws.amazon.com/blogs/apn/kinexon-and-aws-are-pioneering-player-tracking-technology-tailored-for-womens-sports/#Comments) | [Chia sẻ](https://aws.amazon.com/vi/blogs/apn/kinexon-and-aws-are-pioneering-player-tracking-technology-tailored-for-womens-sports/#)

Bởi **Tiến sĩ Simone Kreyer**, Chánh văn phòng – KINEXON
Bởi **Jana Hubel**, Trưởng phòng Tư vấn Khoa học Thể thao, Thể thao Nữ – KINEXON
Bởi **Frank Mullerat**, Kiến trúc sư Giải pháp Đối tác – AWS
Bởi **Bailey Thompson**, Kiến trúc sư Giải pháp Đối tác – AWS

Thể thao nữ thường bị bỏ qua khi nói đến việc nâng cao thành tích thông qua phân tích dữ liệu thể thao.

Khi nhận ra rằng hầu hết các nghiên cứu trong lĩnh vực y học thể thao và khoa học thể dục, vốn là nền tảng cho việc huấn luyện và công nghệ thể thao thành tích cao, đều chủ yếu dựa trên nam giới, thì rõ ràng là phụ nữ xứng đáng nhận được những tiến bộ công nghệ tương tự dựa trên các nghiên cứu và phát hiện của riêng họ.

Bài viết này mô tả sự hợp tác giữa Amazon Web Services (AWS) và [KINEXON](https://www.kinexon.com/) cùng cách tiếp cận độc đáo của chúng tôi đối với công nghệ theo dõi vận động viên được thiết kế riêng cho phụ nữ.

Cả AWS và KINEXON đều đi đầu trong lĩnh vực phân tích dữ liệu thể thao trực tiếp, và chúng tôi sẽ chia sẻ cách hai công ty này hợp tác với một mục tiêu chung—*thách thức hiện trạng* trong thể thao nữ.

KINEXON là một [Đối tác của AWS](https://partners.amazonaws.com/partners/0010h00001cCwdWAAS/KINEXON%20GmbH) và là công ty công nghệ hàng đầu thế giới cung cấp các giải pháp phân tích và hiệu suất cho các đội thể thao và giải đấu, cũng như các giải pháp Internet vạn vật (IoT) thời gian thực chuyên dụng cho Công nghiệp 4.0.
![KINEXON](/images/3-BlogsTranslated/3.2-Blog2/figure1.png)

## Thiết kế Công nghệ Theo dõi Vận động viên dành riêng cho Nữ giới

Khi tùy chỉnh công nghệ theo dõi và phân tích vận động viên dành cho nữ, [những khác biệt độc đáo về sinh lý và cơ sinh học giữa nam và nữ](https://kinexon.com/blog/sports-tech-equality)—chẳng hạn như chu kỳ kinh nguyệt, biến động nội tiết tố, vóc dáng và các số đo cơ thể (như trọng tâm thấp hơn), và nhiều yếu tố khác—cần phải được xem xét.

Chuyên môn của KINEXON trong công nghệ theo dõi vận động viên, kết hợp với sức mạnh điện toán đám mây của AWS, đã mở đường cho những điều chỉnh sản phẩm và các cải tiến mới trong lĩnh vực này.
![AWS](/images/3-BlogsTranslated/3.2-Blog2/figure2.png)

## Những tiến bộ công nghệ ban đầu

Một trong những động lực chính trong việc tùy chỉnh phân tích dữ liệu thể thao theo nhu cầu của phụ nữ là hiểu và sử dụng thông tin về chu kỳ kinh nguyệt và tình trạng sức khỏe cá nhân của một vận động viên. [Thông qua một bảng câu hỏi hàng ngày](https://kinexon.com/blog/sports-data-analytics-empowering-women-athletes), giờ đây có thể kết hợp dữ liệu hiệu suất với thông tin cá nhân và từ đó tính toán các khuyến nghị về khối lượng vận động (load) cho từng cá nhân.

Tùy thuộc vào giai đoạn chu kỳ mà một vận động viên đang trải qua, kết hợp với thông tin về tình trạng sức khỏe cá nhân của cô ấy, ứng dụng của KINEXON sẽ hiển thị một kế hoạch quản lý khối lượng vận động được cá nhân hóa trên một bảng điều khiển (dashboard) có thể truy cập trên các thiết bị di động như điện thoại thông minh và máy tính bảng.

Quản lý khối lượng vận động là một khái niệm quan trọng trong thể thao, vì nó giúp theo dõi và điều chỉnh cường độ tập luyện hoặc thi đấu của một vận động viên. Bảng điều khiển, được hiển thị trong Hình 1 dưới đây, cung cấp một giao diện thân thiện với người dùng để các vận động viên và huấn luyện viên theo dõi và quản lý khối lượng vận động được đề xuất.

Điều này giúp ngăn ngừa chấn thương đồng thời hướng dẫn các vận động viên đạt đến hiệu suất đỉnh cao. Do chu kỳ kinh nguyệt và vóc dáng khác nhau, các vận động viên nữ có [nguy cơ bị chấn thương đầu gối nghiêm trọng](https://kinexon.com/blog/acl-tears-in-women-athletes) như đứt dây chằng chéo trước (ACL) cao gấp sáu lần. Đây là một ví dụ cho thấy tại sao đã đến lúc cần phải quan tâm đến những khác biệt tự nhiên giữa nam và nữ và chú ý đến nhu cầu của từng cá nhân.

![Demand planner](/images/3-BlogsTranslated/3.2-Blog2/figure3.png)
*Hình 1 – Công cụ lập kế hoạch nhu cầu (Demand planner) là một phần của phần mềm KINEXON.*

Một khía cạnh khác mà KINEXON và AWS cùng nhau thực hiện là thiết lập các ngưỡng (thresholds) có ý nghĩa hơn cho thể thao nữ. Trong công nghệ thể thao, các ngưỡng hiệu suất dùng để tự động phát hiện các sự kiện thể chất quan trọng và đơn giản hóa việc phân tích. Do việc thu thập dữ liệu trong thể thao nam đã được thực hiện rộng rãi hơn trong nhiều năm, việc áp dụng các ngưỡng theo tiêu chuẩn quốc gia và quốc tế cho nam giới thường dễ dàng hơn.

Thông qua nhiều năm theo dõi hiệu suất của KINEXON với các đội nữ, công ty đã có thể thiết lập các ngưỡng khác biệt chỉ dựa trên dữ liệu lịch sử do các vận động viên nữ tạo ra. Đây là một phần khác của các tiêu chuẩn mới mà KINEXON và AWS đang thiết lập.

## Thúc đẩy Bình đẳng trong Công nghệ Thể thao

Trong khi ăn mừng những tiến bộ công nghệ này, điều quan trọng là phải thừa nhận bối cảnh rộng lớn hơn của phụ nữ trong thể thao. Những thách thức vẫn còn rất nhiều, chẳng hạn như thiếu nguồn lực và cơ hội không bình đẳng cho phụ nữ trong lĩnh vực công nghệ thể thao.

Để cải thiện điều kiện cho các vận động viên và đội nữ trong thể thao, AWS và KINEXON đã đặt ra ba mục tiêu chính:

- Lắng nghe và học hỏi
- Sáng tạo và tạo tác động
- Kết nối và cung cấp thông tin

### Mục tiêu #1 – Lắng nghe và học hỏi

Các vận động viên và huấn luyện viên là những người hiểu rõ nhất nơi nào tiềm năng chưa được khai thác. Tuy nhiên, trong thể thao nữ, việc sử dụng công nghệ theo dõi vận động viên và phân tích dữ liệu vẫn chưa phổ biến vì nhiều lý do.

AWS và KINEXON đang tạo điều kiện cho các đội tuyển tiêu biểu được lựa chọn—chẳng hạn như đội từng tham dự Women’s Champions League [TSG Hoffenheim](https://hs.kinexon.com/spo-tsg-hoffenheim-women-case-study), câu lạc bộ tiên phong của Đức [Viktoria Berlin](https://kinexon.com/blog/fc-viktoria-to-become-a-kinexon-and-aws-flagship-team), đội bóng rổ nữ NCAA từ [Đại học bang Florida](https://kinexon.com/blog/florida-state-basketball-next-aws-flagship-womens-team), và đội bóng chuyền hàng đầu của Ý [Savino Del Bene Volley Scandicci](https://kinexon-sports.com/blog/savino-del-bene-scandicci-volleyball-selected-as-third-kinexon-and-aws-flagship-team/)—sử dụng công nghệ giúp họ tích hợp phân tích vào thói quen hàng ngày.

Đối với tất cả các giải pháp của KINEXON, có nhiều cảm biến khác nhau được các vận động viên đeo để theo dõi dữ liệu trong các buổi tập hoặc trận đấu. Các cảm biến này có thể được đeo trong một chiếc áo vest được thiết kế riêng cho nữ hoặc bằng cách sử dụng một túi đựng cảm biến mà vận động viên có thể gắn vào áo ngực thể thao cá nhân của mình, như trong Hình 2.

![Demand planner](/images/3-BlogsTranslated/3.2-Blog2/figure4.png)
*Hình 2 – Vận động viên gắn cảm biến KINEXON để ghi lại dữ liệu.*

Các chuyên gia tư vấn công nghệ và khoa học thể thao của KINEXON làm việc chặt chẽ với các đội, tham gia vào các tương tác và hợp tác cá nhân. Mục tiêu của họ là triển khai công nghệ tiên tiến, xác định các chỉ số có ý nghĩa thông qua các cuộc thảo luận kỹ lưỡng, và tạo ra các báo cáo toàn diện và được cá nhân hóa.

Cuối cùng, họ trao quyền cho các huấn luyện viên và đội bóng để sử dụng dữ liệu một cách hiệu quả trong khi cung cấp những thông tin chi tiết cần thiết dựa trên thông tin khách quan về vận động viên. Đổi lại, các câu lạc bộ và đội thể thao học hỏi được về nhu cầu và tiềm năng của các vận động viên. Cách tiếp cận này đảm bảo các vận động viên nữ và đội của họ được tham gia tích cực vào việc phát triển và cải tiến các giải pháp công nghệ thể thao.

Dưới đây, Hình 3 cho thấy giải pháp GPS của KINEXON, bao gồm đế sạc và các cảm biến. Các vận động viên có thể dễ dàng lấy cảm biến ra và đặt chúng vào túi trước khi buổi tập bắt đầu. Tất cả các cảm biến có thể được bật và tắt ngay tại đế sạc. Đế sạc cũng có thể được sử dụng để sạc các cảm biến; ví dụ, trong khi di chuyển.

![Demand planner](/images/3-BlogsTranslated/3.2-Blog2/figure5.png)
*Hình 3 – Cảm biến GNSS của KINEXON.*

### Mục tiêu #2 – Sáng tạo và tạo tác động

Ý tưởng và thông tin chi tiết từ các đội tuyển tiêu biểu và các đội nữ trên toàn cầu chỉ là bước khởi đầu. Thông qua sự hợp tác của chúng tôi, AWS và KINEXON theo dõi chặt chẽ các yêu cầu của các đội thể thao nữ và kiểm tra tính khả thi của chúng, đồng thời cùng nhau phát triển các giải pháp hiệu quả, có thể đạt được để tạo ra tác động có thể đo lường được.

Một cải tiến khác giúp việc quản lý khối lượng vận động trở nên dễ dàng, linh hoạt và tùy biến hơn—thậm chí là theo định hướng chu kỳ. [Các bảng điều khiển quản lý khối lượng vận động dành riêng cho nữ](https://kinexon.com/solutions/sports-analytics-for-women-athletes#results) đầu tiên của AWS và KINEXON dựa trên chu kỳ kinh nguyệt và tình trạng sức khỏe của vận động viên. Thêm vào đó, [công cụ lập kế hoạch khối lượng vận động theo chu kỳ](https://kinexon.com/blog/menstrual-cycle-oriented-performance-training-in-womens-sports) mới được phát triển có thể được sử dụng bởi bất kỳ đội nào chỉ trong năm bước đơn giản.

Những tính năng này đi kèm với tất cả các giải pháp theo dõi vận động viên của KINEXON, chạy trên nền tảng AWS và có thể áp dụng cho cả môi trường trong nhà và ngoài trời.

Các bảng điều khiển theo định hướng chu kỳ mới có khả năng:

- Kết hợp các phản hồi cá nhân về triệu chứng, giai đoạn chu kỳ và khối lượng vận động đã lên kế hoạch.
- Cho phép mỗi huấn luyện viên tùy chỉnh bảng điều khiển của họ để theo dõi các chỉ số mà họ đánh giá cao nhất trong mỗi buổi tập.

Việc lập kế hoạch khối lượng vận động giúp có thể kết hợp dữ liệu chu kỳ và việc kiểm soát tập luyện, đồng thời cung cấp cho huấn luyện viên và vận động viên một cái nhìn tổng quan đơn giản/rõ ràng.

![Demand planner](/images/3-BlogsTranslated/3.2-Blog2/figure6.png)
*Hình 4 – Bảng điều khiển lập kế hoạch nhu cầu – Theo dõi chu kỳ x Giám sát khối lượng vận động.*

### Mục tiêu #3 – Kết nối và cung cấp thông tin

Chia sẻ kinh nghiệm và kiến thức có thể giúp ích cho bất kỳ đội nào, đó là lý do tại sao chúng tôi coi trọng và thúc đẩy việc chia sẻ thông tin, các nghiên cứu hiện tại và kiến thức một cách cởi mở. AWS và KINEXON tích cực tìm kiếm và khuyến khích sự trao đổi, luôn cố gắng đóng góp vào việc cải thiện tính chuyên nghiệp trong thể thao nữ. Chúng tôi cam kết xây dựng một cộng đồng hỗ trợ nơi kiến thức được chia sẻ và sự tiến bộ được tạo ra.

Hãy xem [bộ phim tài liệu của KINEXON](https://www.youtube.com/watch?v=YOUR_DOCUMENTARY_LINK_HERE) để theo dõi hành trình của các đội tuyển tiêu biểu được AWS lựa chọn.
*Leveling the Playing Field for Women Athletes | Episode 1*

## Kết luận

Sự hợp tác giữa AWS và KINEXON không chỉ về công nghệ—mà còn về việc thúc đẩy sự bình đẳng trong thể thao. Nỗ lực này hứa hẹn sẽ trao quyền cho phụ nữ trong thể thao bằng cách cung cấp cho họ những công cụ, kiến thức và sự hỗ trợ cần thiết để họ tỏa sáng.

Khi công việc tiếp tục phát triển, tương lai của thể thao nữ trông tươi sáng hơn bao giờ hết. Nếu bạn muốn tìm hiểu thêm về các giải pháp theo dõi vận động viên của KINEXON và cách nó có thể giúp đội thể thao của bạn, hãy [liên hệ với KINEXON](https://www.kinexon.com/contact) hoặc [yêu cầu một bản demo miễn phí](https://www.kinexon.com/request-demo).

![Connect with KINEXON](/images/3-BlogsTranslated/3.2-Blog2/figure7.png)

---

## KINEXON – Giới thiệu Đối tác AWS

**KINEXON** là một Đối tác của AWS và là công ty công nghệ hàng đầu thế giới cung cấp các giải pháp phân tích và hiệu suất cho các đội thể thao và giải đấu, cũng như các giải pháp IoT thời gian thực chuyên dụng cho Công nghiệp 4.0.

 [Liên hệ KINEXON](https://www.kinexon.com/contact) | [Tổng quan về Đối tác](https://aws.amazon.com/partners/kinexon/) | [Các case study](https://aws.amazon.com/solutions/case-studies/)

**THẺ:** [Bài viết của Đối tác AWS](https://aws.amazon.com/blogs/apn/tag/apn-partner-guest-post/), [Kiến trúc sư Giải pháp Đối tác AWS](https://aws.amazon.com/blogs/apn/tag/aws-partner-solutions-architects/), [Câu chuyện Thành công của Đối tác AWS](https://aws.amazon.com/blogs/apn/tag/apn-partner-success-stories/), [KINEXON](https://aws.amazon.com/blogs/apn/tag/aws-partner-solutions-architects/)
