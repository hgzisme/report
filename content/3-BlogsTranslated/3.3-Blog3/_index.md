---
title: "Blog 3"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

## Advanced Fine-Tuning Methods on Amazon SageMaker AI

by Ilan Gleiser, Deeksha Razdan, and Prashanth Ramaswamy | on July 11, 2025 | in [Amazon SageMaker AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-ai/), [Artificial Intelligence](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/), [Best Practices](https://aws.amazon.com/blogs/machine-learning/category/post-types/best-practices/), [Permalink](https://aws.amazon.com/blogs/machine-learning/advanced-fine-tuning-methods-on-amazon-sagemaker-ai/), [Comments](https://aws.amazon.com/blogs/machine-learning/advanced-fine-tuning-methods-on-amazon-sagemaker-ai/#Comments) | [Share](https://aws.amazon.com/blogs/machine-learning/advanced-fine-tuning-methods-on-amazon-sagemaker-ai/#)

This post provides the theoretical foundation and practical insights needed to navigate the complexity of Large Language Model (LLM) development on [Amazon SageMaker AI](https://aws.amazon.com/sagemaker/ai/), helping organizations make optimal choices for their specific use cases, resource constraints, and business goals.

We address three fundamental aspects of LLM development: the core lifecycle stages, the spectrum of fine-tuning methods, and the crucial alignment techniques to ensure responsible AI deployment. We explore how **Parameter-Efficient Fine-Tuning (PEFT)** methods like **LoRA** and **QLoRA** have democratized model customization, allowing organizations of all sizes to tailor large models to their specific needs. Additionally, we examine alignment methods like **Reinforcement Learning from Human Feedback (RLHF)** and **Direct Preference Optimization (DPO)**, which help ensure these powerful systems operate in line with human values and organizational requirements. Finally, we focus on **knowledge distillation**, which enables efficient model training through a teacher/student approach, where a smaller model learns from a larger one, while **mixed precision training** and **gradient accumulation** techniques optimize memory usage and batch handling, making it possible to train large AI models with limited computational resources.

Throughout the post, we focus on practical implementation while addressing key cost, performance, and operational efficiency considerations. We start with **pre-training**, the foundational stage where models gain broad language understanding. Then, we consider **continued pre-training**, an approach to adapt models for specific domains or tasks. Finally, we discuss **fine-tuning**, the process of honing these models for specific applications. Each stage plays a critical role in shaping LLMs into the sophisticated tools we use today, and understanding these processes is key to grasping the full potential and limitations of modern AI language models.

If you are new to large language models or are looking to leverage more from your existing LLM projects, we guide you through everything you need to know about fine-tuning methods on Amazon SageMaker AI.

## Pre-training

Pre-training is the foundation of LLM development. During this phase, models acquire general language understanding and generation capabilities through exposure to massive amounts of text data. This process typically involves training from scratch on diverse datasets, often comprising hundreds of billions of tokens scraped from books, articles, code repositories, websites, and other publicly available sources.

Pre-training teaches the model broad linguistic and semantic patterns, such as grammar, context, world knowledge, reasoning abilities, and token prediction, using self-supervised learning techniques like masked language modeling (e.g., BERT) or causal language modeling (e.g., GPT). At this stage, the model is not tuned for any specific downstream task but rather builds a versatile language representation that can be adapted later with fine-tuning or PEFT methods.

Pre-training is resource-intensive, demanding significant computing power (often across thousands of GPUs or [AWS Trainium](https://aws.amazon.com/ai/machine-learning/trainium/) chips), large-scale distributed training frameworks, and careful data governance to balance performance with bias, safety, and accuracy concerns.

**Continued pre-training** (also known as domain-adaptive pre-training or intermediate pre-training) is the process of taking an already pre-trained language model and continuing its training on specialized or task-relevant data corpora before fine-tuning. Unlike training entirely from scratch, this method builds upon the existing capabilities of a general-purpose model, allowing it to absorb new patterns, vocabulary, or contexts relevant to a specific domain.

This step is particularly useful when models must handle specialized terminology or unique syntax, especially in fields like law, medicine, or finance. This approach is also essential when organizations need to align the AI output with their internal documentation standards and proprietary knowledge base. Additionally, it is an effective solution for addressing linguistic or cultural representation gaps by enabling focused training on underrepresented dialects, languages, or regional content.

For further reading, refer to the following resources:

* [Pre-training genomic language models using AWS HealthOmics and Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/pre-training-genomic-language-models-using-aws-healthomics-and-amazon-sagemaker/)
* [Customize models in Amazon Bedrock with your own data, using fine-tuning and continued pre-training](https://aws.amazon.com/blogs/aws/customize-models-in-amazon-bedrock-with-your-own-data-using-fine-tuning-and-continued-pre-training/)

## Alignment Methods for LLMs

Aligning LLMs is a crucial step to ensure these powerful systems operate in line with human values and preferences. AWS offers comprehensive support for deploying various alignment techniques, each providing distinct approaches to achieve this goal. Here are the key methods.

### Reinforcement Learning from Human Feedback

Reinforcement Learning from Human Feedback (RLHF) is one of the most firmly established model alignment methods.  This method transforms human preferences into a learned reward signal to steer the model's behavior. The RLHF process involves three distinct phases. First, we collect comparison data, where human annotators choose between different model outputs for the same prompt. This data forms the foundation for training a **reward model**, which learns to predict human preferences. Finally, we fine-tune the language model using **Proximal Policy Optimization (PPO)**, optimizing it to maximize the predicted reward.

**Constitutional AI** is an innovative alignment method that reduces the dependency on human feedback by enabling models to critique and improve their own outputs. This approach involves training models to internalize specific principles or rules, which are then used to guide generation and self-improvement. The reinforcement learning phase is similar to RLHF, except the feedback pairs are generated and evaluated by an AI model, rather than humans.

For further reading, refer to the following resources:

* [Fine-tune large language models with reinforcement learning from human or AI feedback](https://aws.amazon.com/blogs/machine-learning/fine-tune-large-language-models-with-reinforcement-learning-from-human-or-ai-feedback/)
* [Improving your LLMs with RLHF on Amazon Sagemaker](https://aws.amazon.com/blogs/machine-learning/improving-your-llms-with-rlhf-on-amazon-sagemaker/)
* [High-quality human feedback for your generative AI applications from Amazon SageMaker Ground Truth Plus](https://aws.amazon.com/blogs/machine-learning/high-quality-human-feedback-for-your-generative-ai-applications-from-amazon-sagemaker-ground-truth-plus/)

### Direct Preference Optimization

Direct Preference Optimization (DPO) is an alternative to RLHF, offering a simpler path to model alignment. DPO lessens the need for explicit reward modeling and complex RL training loops, instead directly optimizing the model's policy to match human preferences through a modified supervised learning approach.

DPO’s key innovation lies in formulating the preference learning problem as a classification problem. Given feedback pairs where one response is preferred over another, DPO trains the model to assign a higher probability to the favored response. This method maintains the theoretical connections to RLHF while significantly simplifying the implementation process. When implementing alignment methods, the effectiveness of DPO highly depends on the quality, volume, and diversity of the preference dataset. Organizations must establish robust processes for gathering and validating human feedback while mitigating potential biases in the assigned preferences.

To learn more about DPO, see [Align Meta Llama 3 to human preferences with DPO on Amazon SageMaker Studio and Amazon SageMaker Ground Truth](https://aws.amazon.com/blogs/machine-learning/align-meta-llama-3-to-human-preferences-with-dpo-amazon-sagemaker-studio-and-amazon-sagemaker-ground-truth/)

## Fine-tuning Methods on AWS

Fine-tuning transforms a pre-trained model into one that excels at specific tasks or domains. This phase involves training the model on carefully curated datasets that represent the target use case. Fine-tuning can range from updating all model parameters to more efficient methods that modify only a small subset of parameters. [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/) offers fine-tuning capabilities for supported foundation models (FMs), and [Amazon SageMaker Model Training](https://aws.amazon.com/sagemaker/ai/train/) provides the flexibility for custom fine-tuning implementations along with training models at scale without infrastructure management.

At its core, fine-tuning is a process of **transfer learning**, where the model's existing knowledge is refined and redirected toward specific tasks or fields. This process requires a careful balance between preserving the model’s general capabilities while incorporating new, specialized knowledge.

### Supervised Fine-Tuning

Supervised Fine-Tuning (SFT) involves updating the model’s parameters using a curated dataset of input-output pairs that reflect the desired behavior. SFT enables precise behavioral control and is especially effective when the model needs to follow specific instructions, maintain a tone, or provide consistent output formats, making it ideal for applications that require high reliability and compliance. In highly regulated industries such as healthcare or finance, SFT is often used after continued pre-training, which exposes the model to large volumes of specialized text to build contextual understanding. While continued pre-training ensures the model understands the domain-specific language (like clinical or legal terminology), SFT teaches it how to perform specific tasks such as generating discharge summaries, filling out document templates, or adhering to organizational guidelines. Both steps are often necessary: continued pre-training ensures the model understands the field, and SFT ensures it acts as required. However, because it updates the entire model, SFT is more computationally demanding and requires careful dataset construction.

For further reading on SFT, refer to the following resources:

* [Supervised fine-tuning on SageMaker training jobs](https://github.com/aws-samples/Easy_Fintune_LLM_using_SageMaker_with_LLama_Factory)
* [SageMaker HyperPod recipes](https://github.com/aws/sagemaker-hyperpod-recipes)

### Parameter-Efficient Fine-Tuning

Parameter-Efficient Fine-Tuning (PEFT) represents a significant advance in model customization, enabling organizations to tailor large models while dramatically **reducing computational requirements and cost**.  The following table summarizes the different types of PEFT.

| PEFT Type | AWS Service | How It Works | Benefits |
| :--- | :--- | :--- | :--- |
| **LoRA** (Low-Rank Adaptation) | SageMaker Training (custom deployment) | Instead of updating all model parameters, LoRA inserts trainable low-rank decomposition matrices into the transformer layers, reducing the number of trainable parameters. | Memory efficient, cost-saving, unlocks the ability to customize larger models. |
| **QLoRA** (Quantized LoRA) | SageMaker Training (custom deployment) | Combines model quantization with LoRA, loading the base model at 4-bit precision while customizing it with trainable LoRA parameters. | Further reduction in memory requirements than standard LoRA. |
| **Prompt Tuning** (Additive) | SageMaker Training (custom deployment) | Adds a small set of learnable prompt tokens to the input embeddings; only these tokens are trained. | Lightweight and fast tuning, good for task-specific customization with minimal resources. |
| **P-Tuning** (Additive) | SageMaker Training (custom deployment) | Uses a deep prompt (an adjustable embedding vector passed through an MLP) instead of discrete tokens, enhancing the expressiveness of the prompts. | More expressive than prompt tuning, effective in low-resource settings. |
| **Prefix Tuning** (Additive) | SageMaker Training (custom deployment) | Appends trainable continuous vectors (prefixes) to the attention keys and values in each transformer layer, leaving the base model frozen. | Effective for long-context tasks, avoids full model fine-tuning and reduces compute needs. |

The choice of a PEFT method significantly influences the success of the model adaptation process. Each technique offers distinct advantages, making it uniquely suited for specific scenarios. In the following sections, we provide a comprehensive analysis of when to use the different PEFT methods.

**Low-Rank Adaptation**

Low-Rank Adaptation (LoRA) excels in scenarios that require significant task-specific customization while maintaining reasonable computational efficiency. It is particularly effective in the following use cases:

* **Domain adaptation for enterprise applications:** When customizing models for specialized industry vocabulary and conventions, such as legal, medical, or financial fields, LoRA provides sufficient capacity to learn domain-specific patterns while keeping training costs manageable.
* **Multilingual customization:** Organizations expanding their models to new languages find LoRA to be particularly effective. It allows the model to learn the language-specific nuances while preserving the general knowledge of the base model.

For further reading, refer to the following resources:

* [Accelerating Mixtral MOE fine-tuning on Amazon SageMaker with QLoRA](https://aws.amazon.com/blogs/machine-learning/accelerating-mixtral-moe-fine-tuning-on-amazon-sagemaker-with-qlora/)
* [Fast and cost-effective LLaMA 2 fine-tuning with AWS Trainium](https://aws.amazon.com/blogs/machine-learning/fast-and-cost-effective-llama-2-fine-tuning-with-aws-trainium/)
* [PEFT fine-tuning of Llama 3 on SageMaker HyperPod with AWS Trainium](https://aws.amazon.com/blogs/machine-learning/peft-fine-tuning-of-llama-3-on-sagemaker-hyperpod-with-aws-trainium/)
* [Efficient and cost-effective multi-tenant LoRA serving with Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/efficient-and-cost-effective-multi-tenant-lora-serving-with-amazon-sagemaker/)

**Prompt tuning**

Prompt tuning is ideal in scenarios that demand lightweight, transferable task customization. With prompt tuning, you can store multiple prompt vectors for different tasks without modifying the model itself. Use cases include:

* **Personalized customer interaction:** Software-as-a-Service (SaaS) companies can use prompt tuning to personalize the response behavior for different customers without retraining the model.
* **Task switching in multi-tenant systems:** In systems where multiple Natural Language Processing (NLP) tasks need to be served from a single model, prompt tuning allows for rapid task switching with minimal overhead.

To learn more, see [Prompt tuning for causal language modeling](https://huggingface.co/docs/peft/main/en/task_guides/clm-prompt-tuning).

**P-tuning**

P-tuning extends prompt tuning by representing prompts as continuous embeddings passed through a small trainable neural network (typically an MLP). It is suitable for complex tasks and smaller models. The key use case is:

* **Domain generalization under low-resource conditions:** P-tuning can elicit better performance for specific tasks without the need for large fine-tuning datasets.

To learn more, see [P-tuning](https://huggingface.co/docs/peft/en/package_reference/p_tuning).

**Prefix tuning**

Prefix tuning appends trainable continuous vectors, or prefixes, to the key-value pairs in each attention layer of a transformer, while keeping the base model frozen. Prefix tuning excels in tasks that benefit from conditioning on long contexts, such as document summarization or conversational modeling. One use case is:

* **Conversational systems:** Companies building conversational systems with varying tones (e.g., friendly versus formal) can use prefix tuning to control personality and coherence across turns without changing the base model.

To learn more, see [Prefix tuning for conditional text generation](https://huggingface.co/docs/peft/main/en/task_guides/seq2seq-prefix-tuning).

## LLM Optimization

LLM optimization is a critical aspect of their development lifecycle, enabling more efficient training, reduced computational cost, and improved deployment flexibility.

### Quantization

Quantization is the process of mapping a large set of input values to a smaller set of output values (e.g., from 32-bit to 8-bit). In machine learning (ML), quantization is particularly important for deploying models on resource-constrained devices. One of the most utilized techniques is **Quantized Low-Rank Adaptation (QLoRA)**.

QLoRA is an efficient fine-tuning technique that combines quantization and LoRA methods. It uses 4-bit quantization to reduce the memory usage of the model. QLoRA delivers significant benefits, including up to a 75% reduction in memory usage, the ability to fine-tune large models on consumer GPUs, and performance comparable to full fine-tuning.

For further reading, refer to the following resources:

* [Interactively fine-tune Falcon-40B and other LLMs on Amazon SageMaker Studio notebooks using QLoRA](https://aws.amazon.com/blogs/machine-learning/interactively-fine-tune-falcon-40b-and-other-llms-on-amazon-sagemaker-studio-notebooks-using-qlora/)
* [Fine-tune Llama 2 using QLoRA and deploy it on Amazon SageMaker with AWS Inferentia2](https://aws.amazon.com/blogs/machine-learning/fine-tune-llama-2-using-qlora-and-deploy-it-on-amazon-sagemaker-with-aws-inferentia2/)

### Knowledge distillation

Knowledge distillation is a groundbreaking model compression technique in which a smaller "**student**" model learns to mimic the sophisticated behavior of a larger "**teacher**" model.  By learning not just from the ground truth labels but also from the teacher model's probability distributions, the student model can achieve substantial performance while maintaining a much smaller size. This makes it invaluable for various practical applications, from powering on-device AI features to enabling edge computing and Internet of Things (IoT) deployments.

For further reading on knowledge distillation, refer to the following resources:

* [A guide to Amazon Bedrock model distillation (preview)](https://aws.amazon.com/blogs/machine-learning/a-guide-to-amazon-bedrock-model-distillation-preview/)
* [Use Llama 3.1 405B to generate synthetic data for fine-tuning tasks](https://aws.amazon.com/blogs/machine-learning/use-llama-3-1-405b-to-generate-synthetic-data-for-fine-tuning-tasks/)

### Mixed precision training

Mixed precision training is an advanced optimization technique that balances computational efficiency and model accuracy. By intelligently combining different numerical precisions—primarily 32-bit (FP32) and 16-bit (FP16) floating-point formats—this method revolutionizes how we train complex AI models. [Image illustrating the concept of Mixed Precision Training showing FP32 and FP16 usage for different parameters and operations] This technique has become a game-changer in the AI industry, enabling up to three times faster training speeds, significant reductions in memory footprint, and lower power consumption.

For further reading, refer to the following resources:

* [Mixed precision training with FP8 on P5 instances using Transformer Engine](https://docs.aws.amazon.com/sagemaker/latest/dg/model-parallel-core-features-v2-mixed-precision.html#model-parallel-core-features-v2-mixed-precision-fp8-training-on-p5)
* [Mixed precision training with half-precision data types using PyTorch FSDP](https://docs.aws.amazon.com/sagemaker/latest/dg/model-parallel-core-features-v2-mixed-precision.html#model-parallel-core-features-v2-mixed-precision-half-precision)
* [Efficiently train models with large sequence lengths using Amazon SageMaker model parallel](https://aws.amazon.com/blogs/machine-learning/efficiently-train-models-with-large-sequence-lengths-using-amazon-sagemaker-model-parallel/)

### Gradient accumulation

Gradient accumulation is a powerful technique that addresses the challenges of training large models with limited computational resources. Developers can simulate larger batch sizes by accumulating gradients over several smaller forward and backward passes before performing a weight update. [Image illustrating the Gradient Accumulation process where multiple mini-batches are processed before a single, large-batch equivalent weight update] Think of it as breaking down one large batch into smaller, more manageable mini-batches while preserving the effective training dynamics of the larger batch. This technique has democratized the training of sophisticated AI models, enabling researchers and developers with limited GPU resources to work on cutting-edge deep learning projects.

For further reading, refer to the following resources:

* [Efficiently fine-tune the ESM 2 protein language model with Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/efficiently-fine-tune-the-esm-2-protein-language-model-with-amazon-sagemaker/)
* [End-to-end LLM training on instance clusters with over 100 nodes using AWS Trainium](https://aws.amazon.com/blogs/machine-learning/end-to-end-llm-training-on-instance-clusters-with-over-100-nodes-using-aws-trainium/)

## Conclusion

When fine-tuning ML models on AWS, you can select the right tool for your specific needs. AWS offers a comprehensive suite of tools for data scientists, ML engineers, and business users to achieve their ML goals. AWS has built solutions to support different levels of ML sophistication, from simple SageMaker training jobs for FM fine-tuning to the power of SageMaker HyperPod for cutting-edge research.

We invite you to explore these options, starting with what fits your current needs, and evolving your approach as those needs change. Your journey with AWS is just beginning, and we are here to support you every step of the way.

---

### About the Authors:

**Ilan Gleiser** is a Principal GenAI Specialist at AWS, part of the WWSO Frameworks team. He focuses on developing scalable GenAI architectures and optimizing the training and inference of foundation models. With a deep background in AI and machine learning, Ilan has published over 30 blog posts and implemented over 100 ML and HPC (High-Performance Computing) prototypes globally in the last 5 years. Ilan holds a master's degree in mathematical economics.

**Prashanth Ramaswamy** is a Senior Deep Learning Architect in the AWS Generative AI Innovation Center, where he specializes in model customization and optimization. In his role, he performs fine-tuning, benchmarking, and optimization of models using generative AI as well as traditional AI/ML solutions. He focuses on collaborating with Amazon customers to identify potential use cases and accelerate the impact of AI solutions to achieve critical business outcomes.

**Deeksha Razdan** is an Applied Scientist in the AWS Generative AI Innovation Center, where she specializes in model customization and optimization. Her work revolves around researching and developing generative AI solutions for various industries. She holds a master's degree in computer science from UMass Amherst. Outside of work, Deeksha enjoys spending time in nature.
