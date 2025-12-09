---
title: "Blog 3"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Các phương pháp fine-tuning nâng cao trên Amazon SageMaker AI

bởi Ilan Gleiser, Deeksha Razdan, và Prashanth Ramaswamy | vào ngày 11 tháng 7 năm 2025 | trong [Amazon SageMaker AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-ai/), [Trí tuệ nhân tạo](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/), [Các phương pháp hay nhất](https://aws.amazon.com/blogs/machine-learning/category/post-types/best-practices/), [Liên kết cố định](https://aws.amazon.com/blogs/machine-learning/advanced-fine-tuning-methods-on-amazon-sagemaker-ai/), [Bình luận](https://aws.amazon.com/blogs/machine-learning/advanced-fine-tuning-methods-on-amazon-sagemaker-ai/#Comments) | [Chia sẻ](https://aws.amazon.com/blogs/machine-learning/advanced-fine-tuning-methods-on-amazon-sagemaker-ai/#)

Bài đăng này cung cấp nền tảng lý thuyết và những hiểu biết thực tế cần thiết để điều hướng sự phức tạp của việc phát triển LLM trên [Amazon SageMaker AI](https://aws.amazon.com/sagemaker/ai/), giúp các tổ chức đưa ra lựa chọn tối ưu cho các trường hợp sử dụng cụ thể, các ràng buộc về tài nguyên và mục tiêu kinh doanh của họ.

Chúng tôi cũng đề cập đến ba khía cạnh cơ bản của việc phát triển LLM: các giai đoạn cốt lõi của vòng đời, phổ các phương pháp fine-tuning, và các kỹ thuật alignment (căn chỉnh) quan trọng nhằm đảm bảo việc triển khai AI một cách có trách nhiệm. Chúng tôi khám phá cách các phương pháp Parameter-Efficient Fine-Tuning (PEFT) như LoRA và QLoRA đã dân chủ hóa việc tùy chỉnh mô hình, để các tổ chức thuộc mọi quy mô có thể tùy chỉnh các mô hình lớn theo nhu cầu cụ thể của họ. Ngoài ra, chúng tôi xem xét các phương pháp alignment như Reinforcement Learning from Human Feedback (RLHF) và Direct Preference Optimization (DPO), giúp đảm bảo các hệ thống mạnh mẽ này hoạt động phù hợp với các giá trị của con người và yêu cầu của tổ chức. Cuối cùng, chúng tôi tập trung vào knowledge distillation (chưng cất tri thức), cho phép huấn luyện mô hình hiệu quả thông qua phương pháp thầy/trò, nơi một mô hình nhỏ hơn học hỏi từ một mô hình lớn hơn, trong khi mixed precision training (huấn luyện độ chính xác hỗn hợp) và các kỹ thuật gradient accumulation (tích lũy gradient) tối ưu hóa việc sử dụng bộ nhớ và xử lý batch, giúp có thể huấn luyện các mô hình AI lớn với tài nguyên tính toán hạn chế.

Trong suốt bài đăng, chúng tôi tập trung vào việc triển khai thực tế trong khi giải quyết các cân nhắc quan trọng về chi phí, hiệu suất và hiệu quả vận hành. Chúng tôi bắt đầu với pre-training, giai đoạn nền tảng nơi các mô hình có được sự hiểu biết ngôn ngữ rộng rãi. Sau đó, chúng tôi xem xét continued pre-training, một phương pháp để điều chỉnh các mô hình cho các lĩnh vực hoặc nhiệm vụ cụ thể. Cuối cùng, chúng tôi thảo luận về fine-tuning, quá trình mài giũa các mô hình này cho các ứng dụng cụ thể. Mỗi giai đoạn đóng một vai trò quan trọng trong việc định hình các mô hình ngôn ngữ lớn (LLMs) thành những công cụ tinh vi mà chúng ta sử dụng ngày nay, và việc hiểu các quy trình này là chìa khóa để nắm bắt toàn bộ tiềm năng và hạn chế của các mô hình ngôn ngữ AI hiện đại.

Nếu bạn mới bắt đầu với các mô hình ngôn ngữ lớn hoặc đang tìm cách tận dụng nhiều hơn từ các dự án LLM hiện tại của mình, chúng tôi sẽ hướng dẫn bạn mọi thứ bạn cần biết về các phương pháp fine-tuning trên Amazon SageMaker AI.

## Pre-training

Pre-training là nền tảng của việc phát triển LLM. Trong giai đoạn này, các mô hình học các khả năng hiểu và tạo ngôn ngữ tổng quát thông qua việc tiếp xúc với lượng dữ liệu văn bản khổng lồ. Quá trình này thường bao gồm việc huấn luyện từ đầu trên các bộ dữ liệu đa dạng, thường bao gồm hàng trăm tỷ token lấy từ sách, bài báo, kho mã nguồn, trang web và các nguồn công khai khác.

Pre-training dạy cho mô hình các mẫu ngôn ngữ và ngữ nghĩa rộng lớn, chẳng hạn như ngữ pháp, ngữ cảnh, kiến thức thế giới, khả năng suy luận và dự đoán token, sử dụng các kỹ thuật học tự giám sát như masked language modeling (ví dụ, BERT) hoặc causal language modeling (ví dụ, GPT). Ở giai đoạn này, mô hình không được điều chỉnh cho bất kỳ nhiệm vụ hạ nguồn (downstream task) cụ thể nào mà thay vào đó xây dựng một biểu diễn ngôn ngữ đa năng có thể được điều chỉnh sau này bằng các phương pháp fine-tuning hoặc PEFT.

Pre-training rất tốn kém tài nguyên, đòi hỏi năng lực tính toán đáng kể (thường trên hàng ngàn GPU hoặc chip [AWS Trainium](https://aws.amazon.com/ai/machine-learning/trainium/)), các framework huấn luyện phân tán quy mô lớn, và việc quản lý dữ liệu cẩn thận để cân bằng giữa hiệu suất với các mối quan tâm về thiên vị, an toàn và độ chính xác.

**Continued pre-training** (còn được gọi là domain-adaptive pre-training hoặc intermediate pre-training) là quá trình lấy một mô hình ngôn ngữ đã được pre-trained và tiếp tục huấn luyện nó trên các kho dữ liệu chuyên ngành hoặc liên quan đến nhiệm vụ trước khi fine-tuning. Không giống như pre-training hoàn toàn từ đầu, phương pháp này xây dựng dựa trên các khả năng hiện có của một mô hình đa năng, cho phép nó tiếp thu các mẫu, từ vựng hoặc ngữ cảnh mới liên quan đến một lĩnh vực cụ thể.

Bước này đặc biệt hữu ích khi các mô hình phải xử lý thuật ngữ chuyên ngành hoặc cú pháp độc đáo, đặc biệt trong các lĩnh vực như luật, y học hoặc tài chính. Phương pháp này cũng rất cần thiết khi các tổ chức cần điều chỉnh đầu ra của AI phù hợp với các tiêu chuẩn tài liệu nội bộ và cơ sở kiến thức độc quyền của họ. Ngoài ra, nó còn là một giải pháp hiệu quả để giải quyết các khoảng trống về ngôn ngữ hoặc đại diện văn hóa bằng cách cho phép huấn luyện tập trung vào các phương ngữ, ngôn ngữ hoặc nội dung khu vực ít được đại diện.

Để tìm hiểu thêm, hãy tham khảo qua các tài liệu sau:

  * [Huấn luyện trước các mô hình ngôn ngữ bộ gen bằng AWS HealthOmics và Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/pre-training-genomic-language-models-using-aws-healthomics-and-amazon-sagemaker/)
  * [Tùy chỉnh mô hình trên Amazon Bedrock bằng dữ liệu của riêng bạn, sử dụng phương pháp tinh chỉnh và huấn luyện trước tiếp nối](https://aws.amazon.com/blogs/aws/customize-models-in-amazon-bedrock-with-your-own-data-using-fine-tuning-and-continued-pre-training/)

## Các phương pháp Alignment cho LLMs

Việc alignment các LLM là một bước quan trọng để đảm bảo các hệ thống mạnh mẽ này hoạt động phù hợp với các giá trị và sở thích của con người. AWS cung cấp hỗ trợ toàn diện để triển khai các kỹ thuật alignment khác nhau, mỗi kỹ thuật cung cấp các cách tiếp cận riêng biệt để đạt được mục tiêu này. Sau đây là các phương pháp chính.

### Reinforcement Learning from Human Feedback

Reinforcement Learning from Human Feedback (RLHF) là một trong những phương pháp alignment mô hình đã được thiết lập vững chắc nhất.  Phương pháp này biến đổi sở thích của con người thành một tín hiệu phần thưởng đã học để định hướng hành vi của mô hình. Quá trình RLHF bao gồm ba giai đoạn riêng biệt. Đầu tiên, chúng tôi thu thập dữ liệu so sánh, nơi người chú thích con người chọn giữa các đầu ra khác nhau của mô hình cho cùng một prompt. Dữ liệu này tạo nền tảng để huấn luyện một **reward model**, học cách dự đoán sở thích của con người. Cuối cùng, chúng tôi fine-tune mô hình ngôn ngữ bằng cách sử dụng **Proximal Policy Optimization (PPO)**, tối ưu hóa nó để tối đa hóa phần thưởng được dự đoán.

**Constitutional AI** là một phương pháp alignment đổi mới giúp giảm sự phụ thuộc vào phản hồi của con người bằng cách cho phép các mô hình tự phê bình và cải thiện đầu ra của chính chúng. Phương pháp này bao gồm việc huấn luyện các mô hình để nội tại hóa các nguyên tắc hoặc quy tắc cụ thể, sau đó sử dụng các nguyên tắc này để định hướng việc tạo ra và tự cải thiện. Giai đoạn học tăng cường tương tự như RLHF, ngoại trừ việc các cặp phản hồi được tạo ra và đánh giá bởi một mô hình AI, thay vì con người.

Để tìm hiểu thêm, hãy tham khảo qua các tài liệu sau:

  * [Tinh chỉnh các mô hình ngôn ngữ lớn bằng học tăng cường từ phản hồi của con người hoặc AI](https://aws.amazon.com/blogs/machine-learning/fine-tune-large-language-models-with-reinforcement-learning-from-human-or-ai-feedback/)
  * [Cải thiện các LLM của bạn bằng học máy sử dụng RLHF trên Amazon Sagemaker](https://aws.amazon.com/blogs/machine-learning/improving-your-llms-with-rlhf-on-amazon-sagemaker/)
  * [Phản hồi chất lượng cao của con người cho các ứng dụng AI tạo sinh của bạn từ Amazon SageMaker Ground Truth Plus](https://aws.amazon.com/blogs/machine-learning/high-quality-human-feedback-for-your-generative-ai-applications-from-amazon-sagemaker-ground-truth-plus/)

### Direct Preference Optimization

Direct Preference Optimization (DPO) là một giải pháp thay thế cho RLHF, cung cấp một con đường đơn giản hơn để alignment mô hình. DPO giảm bớt nhu cầu về mô hình hóa phần thưởng rõ ràng và các vòng lặp huấn luyện RL phức tạp, thay vào đó trực tiếp tối ưu hóa chính sách của mô hình để phù hợp với sở thích của con người thông qua một phương pháp học có giám sát đã được sửa đổi.

Sự đổi mới chính của DPO nằm ở việc xây dựng bài toán học sở thích như một bài toán phân loại. Với các cặp phản hồi trong đó một phản hồi được ưa thích hơn phản hồi kia, DPO huấn luyện mô hình để gán xác suất cao hơn cho các phản hồi được ưa thích. Phương pháp này duy trì các kết nối lý thuyết với RLHF trong khi đơn giản hóa đáng kể quá trình triển khai. Khi triển khai các phương pháp alignment, hiệu quả của DPO phụ thuộc nhiều vào chất lượng, khối lượng và sự đa dạng của bộ dữ liệu sở thích. Các tổ chức phải thiết lập các quy trình mạnh mẽ để thu thập và xác thực phản hồi của con người trong khi giảm thiểu các thiên vị tiềm ẩn trong các sở thích được gán nhãn.

Để tìm hiểu thêm về DPO, xem [Căn chỉnh Meta Llama 3 theo sở thích của con người bằng DPO trên Amazon SageMaker Studio và Amazon SageMaker Ground Truth](https://aws.amazon.com/blogs/machine-learning/align-meta-llama-3-to-human-preferences-with-dpo-amazon-sagemaker-studio-and-amazon-sagemaker-ground-truth/)

## Các phương pháp Fine-tuning trên AWS

Fine-tuning biến một mô hình đã được pre-trained thành một mô hình xuất sắc trong các nhiệm vụ hoặc lĩnh vực cụ thể. Giai đoạn này bao gồm việc huấn luyện mô hình trên các bộ dữ liệu được quản lý cẩn thận, đại diện cho trường hợp sử dụng mục tiêu. Fine-tuning có thể bao gồm từ việc cập nhật tất cả các tham số của mô hình đến các phương pháp hiệu quả hơn chỉ sửa đổi một tập hợp nhỏ các tham số. [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/) cung cấp các khả năng fine-tuning cho các mô hình nền tảng (FMs) được hỗ trợ, và [Amazon SageMaker Model Training](https://aws.amazon.com/sagemaker/ai/train/) cung cấp sự linh hoạt cho các triển khai fine-tuning tùy chỉnh cùng với việc huấn luyện các mô hình ở quy mô lớn mà không cần quản lý cơ sở hạ tầng.

Về cốt lõi, fine-tuning là một quá trình **học chuyển giao**, nơi kiến thức hiện có của mô hình được tinh chỉnh và chuyển hướng sang các nhiệm vụ hoặc lĩnh vực cụ thể. Quá trình này đòi hỏi sự cân bằng cẩn thận giữa việc bảo tồn các khả năng chung của mô hình trong khi kết hợp kiến thức mới, chuyên biệt.

### Supervised Fine-Tuning

Supervised Fine-Tuning (SFT) liên quan đến việc cập nhật các tham số của mô hình bằng cách sử dụng một bộ dữ liệu được quản lý gồm các cặp đầu vào-đầu ra phản ánh hành vi mong muốn. SFT cho phép kiểm soát hành vi chính xác và đặc biệt hiệu quả khi mô hình cần tuân theo các hướng dẫn cụ thể, duy trì giọng văn hoặc cung cấp các định dạng đầu ra nhất quán, làm cho nó trở nên lý tưởng cho các ứng dụng đòi hỏi độ tin cậy và tuân thủ cao. Trong các ngành công nghiệp được quản lý chặt chẽ như y tế hoặc tài chính, SFT thường được sử dụng sau continued pre-training, giai đoạn này giúp mô hình tiếp xúc với khối lượng lớn văn bản chuyên ngành để xây dựng sự hiểu biết về ngữ cảnh. Mặc dù continued pre-training giúp mô hình tiếp thu ngôn ngữ chuyên ngành (như thuật ngữ lâm sàng hoặc pháp lý), SFT dạy nó cách thực hiện các nhiệm vụ cụ thể như tạo bản tóm tắt xuất viện, điền vào các mẫu tài liệu hoặc tuân thủ các hướng dẫn của tổ chức. Cả hai bước thường là cần thiết: continued pre-training đảm bảo mô hình hiểu lĩnh vực, và SFT đảm bảo nó hoạt động theo yêu cầu. Tuy nhiên, vì nó cập nhật toàn bộ mô hình, SFT đòi hỏi nhiều tài nguyên tính toán hơn và việc xây dựng bộ dữ liệu cẩn thận.

Để tìm hiểu thêm về SFT, hãy tham khảo qua các tài liệu sau:

  * [Tinh chỉnh có giám sát trên các tác vụ huấn luyện của SageMaker](https://github.com/aws-samples/Easy_Fintune_LLM_using_SageMaker_with_LLama_Factory)
  * [Các công thức của SageMaker HyperPod](https://github.com/aws/sagemaker-hyperpod-recipes)

### Parameter-Efficient Fine-Tuning

Parameter-Efficient Fine-Tuning (PEFT) đại diện cho một tiến bộ đáng kể trong việc tùy chỉnh mô hình, giúp các tổ chức tùy chỉnh các mô hình lớn trong khi **giảm đáng kể yêu cầu tính toán và chi phí**.  Bảng sau tóm tắt các loại PEFT khác nhau.

| Loại PEFT | Dịch vụ AWS | Cách hoạt động | Lợi ích |
| :--- | :--- | :--- | :--- |
| **LoRA** (Low-Rank Adaptation) | SageMaker Training (triển khai tùy chỉnh) | Thay vì cập nhật tất cả các tham số của mô hình, LoRA chèn các ma trận phân rã hạng thấp (rank decomposition matrices) có thể huấn luyện vào các lớp transformer, giảm số lượng tham số có thể huấn luyện. | Hiệu quả về bộ nhớ, tiết kiệm chi phí, mở ra khả năng tùy chỉnh các mô hình lớn hơn. |
| **QLoRA** (Quantized LoRA) | SageMaker Training (triển khai tùy chỉnh) | Kết hợp lượng tử hóa (quantization) mô hình với LoRA, tải mô hình cơ sở ở độ chính xác 4-bit trong khi tùy chỉnh nó với các tham số LoRA có thể huấn luyện. | Giảm yêu cầu bộ nhớ hơn nữa so với LoRA tiêu chuẩn. |
| **Prompt Tuning** (Additive) | SageMaker Training (triển khai tùy chỉnh) | Thêm một bộ nhỏ các token prompt có thể học vào trước các embedding đầu vào; chỉ những token này được huấn luyện. | Tinh chỉnh nhẹ và nhanh, tốt cho việc tùy chỉnh theo nhiệm vụ cụ thể với tài nguyên tối thiểu. |
| **P-Tuning** (Additive) | SageMaker Training (triển khai tùy chỉnh) | Sử dụng một prompt sâu (một vector embedding có thể điều chỉnh được truyền qua một MLP) thay vì các token rời rạc, tăng cường khả năng biểu đạt của các prompt. | Biểu cảm hơn prompt tuning, hiệu quả trong các cài đặt tài nguyên thấp. |
| **Prefix Tuning** (Additive) | SageMaker Training (triển khai tùy chỉnh) | Thêm các vector liên tục có thể huấn luyện (prefixes) vào trước các khóa và giá trị attention trong mỗi lớp transformer, giữ nguyên mô hình cơ sở. | Hiệu quả cho các nhiệm vụ có ngữ cảnh dài, tránh fine-tuning toàn bộ mô hình và giảm nhu cầu tính toán. |

Việc lựa chọn một phương pháp PEFT có ảnh hưởng đáng kể đến sự thành công của quá trình hiệu chỉnh mô hình. Mỗi kỹ thuật đều có những ưu điểm khác biệt, khiến nó đặc biệt phù hợp với những kịch bản cụ thể. Trong các phần sau, chúng tôi sẽ cung cấp một phân tích toàn diện về thời điểm nên sử dụng các phương pháp PEFT khác nhau.

**Low-Rank Adaptation**

Low-Rank Adaptation (LoRA) nổi trội trong các kịch bản đòi hỏi sự tùy chỉnh đáng kể theo nhiệm vụ cụ thể trong khi vẫn duy trì hiệu quả tính toán hợp lý. Nó đặc biệt hiệu quả trong các trường hợp sử dụng sau:

  * **Tùy chỉnh theo lĩnh vực cho các ứng dụng doanh nghiệp:** Khi tùy chỉnh các mô hình cho các từ vựng và quy ước ngành chuyên biệt, như các lĩnh vực pháp lý, y tế hoặc tài chính, LoRA cung cấp đủ năng lực để học các mẫu chuyên ngành trong khi giữ chi phí huấn luyện ở mức có thể quản lý được.
  * **Tùy chỉnh đa ngôn ngữ:** Các tổ chức mở rộng mô hình của họ sang các ngôn ngữ mới thấy LoRA đặc biệt hiệu quả. Nó cho phép mô hình học các sắc thái riêng của ngôn ngữ trong khi vẫn bảo tồn kiến thức chung của mô hình cơ sở.

Để tìm hiểu thêm, hãy tham khảo qua các tài liệu sau:

  * [Tăng tốc tinh chỉnh Mixtral MOE trên Amazon SageMaker với QLoRA](https://aws.amazon.com/blogs/machine-learning/accelerating-mixtral-moe-fine-tuning-on-amazon-sagemaker-with-qlora/)
  * [Tinh chỉnh LLaMA 2 nhanh chóng và tiết kiệm chi phí với AWS Trainium](https://aws.amazon.com/blogs/machine-learning/fast-and-cost-effective-llama-2-fine-tuning-with-aws-trainium/)
  * [Tinh chỉnh PEFT cho Llama 3 trên SageMaker HyperPod với AWS Trainium](https://aws.amazon.com/blogs/machine-learning/peft-fine-tuning-of-llama-3-on-sagemaker-hyperpod-with-aws-trainium/)
  * [Phục vụ LoRA đa người thuê (multi-tenant) hiệu quả và tiết kiệm chi phí với Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/efficient-and-cost-effective-multi-tenant-lora-serving-with-amazon-sagemaker/)

**Prompt tuning**

Prompt tuning lý tưởng trong các kịch bản đòi hỏi sự tùy chỉnh nhiệm vụ nhẹ nhàng, có thể chuyển đổi. Với prompt tuning, bạn có thể lưu trữ nhiều vector prompt cho các nhiệm vụ khác nhau mà không cần sửa đổi chính mô hình. Các trường hợp sử dụng bao gồm:

  * **Tương tác khách hàng được cá nhân hóa:** Các công ty cung cấp nền tảng phần mềm dịch vụ (SaaS) có thể sử dụng prompt tuning để cá nhân hóa hành vi phản hồi cho các khách hàng khác nhau mà không cần huấn luyện lại mô hình.
  * **Chuyển đổi nhiệm vụ trong các hệ thống đa người thuê:** Trong các hệ thống nơi nhiều tác vụ xử lý ngôn ngữ tự nhiên (NLP) cần được phục vụ từ một mô hình duy nhất, prompt tuning cho phép chuyển đổi tác vụ nhanh chóng với chi phí tối thiểu.

Để tìm hiểu thêm, xem [Tinh chỉnh prompt cho mô hình hóa ngôn ngữ nhân quả](https://huggingface.co/docs/peft/main/en/task_guides/clm-prompt-tuning).

**P-tuning**

P-tuning mở rộng prompt tuning bằng cách biểu diễn các prompt dưới dạng các embedding liên tục được truyền qua một mạng nơ-ron nhỏ có thể huấn luyện (thường là một MLP). Nó phù hợp cho các nhiệm vụ phức tạp và các mô hình nhỏ hơn. Trường hợp sử dụng chính là:

  * **Tổng quát hóa lĩnh vực trong điều kiện tài nguyên thấp:** P-tuning có thể trích xuất hiệu suất tốt hơn cho các nhiệm vụ cụ thể mà không cần các bộ dữ liệu fine-tuning lớn.

Để tìm hiểu thêm, xem [P-tuning](https://huggingface.co/docs/peft/en/package_reference/p_tuning).

**Prefix tuning**

Prefix tuning thêm các vector liên tục có thể huấn luyện, còn gọi là prefixes, vào trước các cặp khóa-giá trị trong mỗi lớp attention của một transformer, trong khi giữ nguyên mô hình cơ sở. Prefix tuning nổi trội trong các nhiệm vụ được hưởng lợi từ việc điều kiện hóa trên các ngữ cảnh dài, chẳng hạn như tóm tắt tài liệu hoặc mô hình hóa hội thoại. Một trường hợp sử dụng là:

  * **Hệ thống hội thoại:** Các công ty xây dựng hệ thống hội thoại với các giọng điệu khác nhau (ví dụ: thân thiện so với trang trọng) có thể sử dụng prefix tuning để kiểm soát tính cách và sự mạch lạc qua các lượt tương tác mà không thay đổi mô hình cơ sở.

Để tìm hiểu thêm, xem [Tinh chỉnh tiền tố cho sinh văn bản có điều kiện](https://huggingface.co/docs/peft/main/en/task_guides/seq2seq-prefix-tuning).

## Tối ưu hóa LLM

Tối ưu hóa LLM là một khía cạnh quan trọng trong vòng đời phát triển của chúng, cho phép huấn luyện hiệu quả hơn, giảm chi phí tính toán và cải thiện tính linh hoạt khi triển khai.

### Quantization

Quantization là quá trình ánh xạ một tập hợp lớn các giá trị đầu vào sang một tập hợp nhỏ hơn các giá trị đầu ra (ví dụ: từ 32-bit xuống 8-bit). Trong học máy (ML), quantization đặc biệt quan trọng để triển khai các mô hình trên các thiết bị có tài nguyên hạn chế. Một trong những kỹ thuật được sử dụng nhiều nhất là **Quantized Low-Rank Adaptation (QLoRA)**.

QLoRA là một kỹ thuật fine-tuning hiệu quả, kết hợp các phương pháp quantization và LoRA. Nó sử dụng quantization 4-bit để giảm mức sử dụng bộ nhớ của mô hình. QLoRA mang lại những lợi ích đáng kể, bao gồm giảm tới 75% mức sử dụng bộ nhớ, khả năng fine-tune các mô hình lớn trên GPU tiêu dùng, và hiệu suất tương đương với fine-tuning toàn bộ.

Để tìm hiểu thêm, hãy tham khảo qua các tài liệu sau:

  * [Tinh chỉnh tương tác Falcon-40B và các LLM khác trên notebook của Amazon SageMaker Studio bằng QLoRA](https://aws.amazon.com/blogs/machine-learning/interactively-fine-tune-falcon-40b-and-other-llms-on-amazon-sagemaker-studio-notebooks-using-qlora/)
  * [Tinh chỉnh Llama 2 bằng QLoRA và triển khai trên Amazon SageMaker với AWS Inferentia2](https://aws.amazon.com/blogs/machine-learning/fine-tune-llama-2-using-qlora-and-deploy-it-on-amazon-sagemaker-with-aws-inferentia2/)

### Knowledge distillation

Knowledge distillation là một kỹ thuật nén mô hình đột phá, trong đó một mô hình "**học sinh**" nhỏ hơn học cách bắt chước hành vi tinh vi của một mô hình "**giáo viên**" lớn hơn.  Bằng cách học không chỉ từ các nhãn thực tế mà còn từ các phân phối xác suất của mô hình giáo viên, mô hình học sinh có thể đạt được hiệu suất đáng kể trong khi duy trì kích thước nhỏ hơn nhiều. Điều này làm cho nó vô giá cho các ứng dụng thực tế khác nhau, từ việc cung cấp năng lượng cho các tính năng AI trên thiết bị di động đến việc cho phép các giải pháp điện toán biên và triển khai Internet of Things (IoT).

Để tìm hiểu thêm về knowledge distillation, hãy tham khảo qua các tài liệu sau:

  * [Hướng dẫn về Chưng cất Mô hình trên Amazon Bedrock (bản xem trước)](https://aws.amazon.com/blogs/machine-learning/a-guide-to-amazon-bedrock-model-distillation-preview/)
  * [Sử dụng Llama 3.1 405B để tạo dữ liệu tổng hợp và chưng cất nhằm tinh chỉnh các mô hình nhỏ hơn](https://aws.amazon.com/blogs/machine-learning/use-llama-3-1-405b-to-generate-synthetic-data-for-fine-tuning-tasks/)

### Mixed precision training

Mixed precision training là một kỹ thuật tối ưu hóa tiên tiến, cân bằng giữa hiệu quả tính toán và độ chính xác của mô hình. Bằng cách kết hợp thông minh các độ chính xác số học khác nhau—chủ yếu là định dạng dấu phẩy động 32-bit (FP32) và 16-bit (FP16)—phương pháp này cách mạng hóa cách chúng ta huấn luyện các mô hình AI phức tạp.  Kỹ thuật này đã trở thành một yếu tố thay đổi cuộc chơi trong ngành AI, cho phép tốc độ huấn luyện nhanh hơn tới ba lần, giảm đáng kể dung lượng bộ nhớ và tiêu thụ điện năng thấp hơn.

Để tìm hiểu thêm, hãy tham khảo qua các tài liệu sau:

  * [Huấn luyện độ chính xác hỗn hợp với FP8 trên các instance P5 bằng Transformer Engine](https://docs.aws.amazon.com/sagemaker/latest/dg/model-parallel-core-features-v2-mixed-precision.html#model-parallel-core-features-v2-mixed-precision-fp8-training-on-p5)
  * [Huấn luyện độ chính xác hỗn hợp với các kiểu dữ liệu half-precision bằng PyTorch FSDP](https://docs.aws.amazon.com/sagemaker/latest/dg/model-parallel-core-features-v2-mixed-precision.html#model-parallel-core-features-v2-mixed-precision-half-precision)
  * [Huấn luyện hiệu quả các mô hình có độ dài chuỗi lớn bằng tính năng song song hóa mô hình của Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/efficiently-train-models-with-large-sequence-lengths-using-amazon-sagemaker-model-parallel/)

### Gradient accumulation

Gradient accumulation là một kỹ thuật mạnh mẽ giải quyết những thách thức của việc huấn luyện các mô hình lớn với tài nguyên tính toán hạn chế. Các nhà phát triển có thể mô phỏng các kích thước batch lớn hơn bằng cách tích lũy các gradient qua nhiều lượt truyền xuôi và ngược nhỏ hơn trước khi thực hiện cập nhật trọng số.  Hãy nghĩ về nó như việc chia nhỏ một batch lớn thành các mini-batch nhỏ hơn, dễ quản lý hơn trong khi vẫn duy trì động lực huấn luyện hiệu quả của batch lớn hơn. Kỹ thuật này đã dân chủ hóa việc huấn luyện các mô hình AI tinh vi, giúp các nhà nghiên cứu và nhà phát triển có tài nguyên GPU hạn chế có thể làm việc trên các dự án học sâu tiên tiến.

Để tìm hiểu thêm, hãy tham khảo qua các tài liệu sau:

  * [Tinh chỉnh hiệu quả mô hình ngôn ngữ protein ESM 2 với Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/efficiently-fine-tune-the-esm-2-protein-language-model-with-amazon-sagemaker/)
  * [Huấn luyện LLM toàn trình trên các cụm instance hơn 100 node bằng AWS Trainium](https://aws.amazon.com/blogs/machine-learning/end-to-end-llm-training-on-instance-clusters-with-over-100-nodes-using-aws-trainium/)

## Kết luận

Khi fine-tuning các mô hình ML trên AWS, bạn có thể chọn công cụ phù hợp cho nhu cầu cụ thể của mình. AWS cung cấp một bộ công cụ toàn diện cho các nhà khoa học dữ liệu, kỹ sư ML và người dùng doanh nghiệp để đạt được các mục tiêu ML của họ. AWS đã xây dựng các giải pháp để hỗ trợ các cấp độ tinh vi khác nhau của ML, từ các công việc huấn luyện SageMaker đơn giản để fine-tuning FM cho đến sức mạnh của SageMaker HyperPod cho các nghiên cứu tiên tiến.

Chúng tôi mời bạn khám phá các tùy chọn này, bắt đầu với những gì phù hợp với nhu cầu hiện tại của bạn, và phát triển cách tiếp cận của bạn khi những nhu cầu đó thay đổi. Hành trình của bạn với AWS chỉ mới bắt đầu, và chúng tôi ở đây để hỗ trợ bạn trên mọi bước đường.

-----

### Về các tác giả:

**Ilan Gleiser** là Chuyên gia Chính về AI Tạo sinh (Principal GenAI Specialist) tại AWS, thuộc đội ngũ WWSO Frameworks. Ông tập trung vào việc phát triển các kiến trúc AI tạo sinh có khả năng mở rộng và tối ưu hóa quá trình huấn luyện cũng như suy luận của các mô hình nền tảng. Với nền tảng sâu rộng về AI và học máy, trong 5 năm qua, Ilan đã xuất bản hơn 30 bài viết trên blog và triển khai hơn 100 nguyên mẫu về học máy và HPC (Tính toán hiệu năng cao) trên toàn cầu. Ilan có bằng thạc sĩ về kinh tế toán.

**Prashanth Ramaswamy** là Kiến trúc sư Học sâu Cấp cao (Senior Deep Learning Architect) tại Trung tâm Sáng tạo AI Tạo sinh của AWS (AWS Generative AI Innovation Center), nơi ông chuyên về tùy chỉnh và tối ưu hóa mô hình. Trong vai trò của mình, ông thực hiện tinh chỉnh (fine-tuning), kiểm chuẩn (benchmarking) và tối ưu hóa các mô hình bằng cách sử dụng AI tạo sinh cũng như các giải pháp AI/ML truyền thống. Ông tập trung vào việc hợp tác với khách hàng của Amazon để xác định các trường hợp sử dụng tiềm năng và đẩy nhanh tác động của các giải pháp AI nhằm đạt được các kết quả kinh doanh quan trọng.

**Deeksha Razdan** là Nhà khoa học Ứng dụng (Applied Scientist) tại Trung tâm Sáng tạo AI Tạo sinh của AWS, nơi cô chuyên về tùy chỉnh và tối ưu hóa mô hình. Công việc của cô xoay quanh việc nghiên cứu và phát triển các giải pháp AI tạo sinh cho nhiều ngành công nghiệp khác nhau. Cô có bằng thạc sĩ khoa học máy tính tại UMass Amherst. Ngoài công việc, Deeksha thích hòa mình với thiên nhiên.
