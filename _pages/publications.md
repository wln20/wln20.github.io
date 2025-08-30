---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

+ [NeurIPS ENLSP Workshop 2023] **CSKV: Training-Efficient Channel Shrinking for KV Cache in Long-Context Scenarios**. **Luning Wang**, Shiyao Li, Xuefei Ning, Zhihang Yuan, Shengen Yan, Guohao Dai, Yu Wang.

https://arxiv.org/pdf/2409.10593

  **Abstract:** Large Language Models (LLMs) have been widely adopted to process long-context tasks. However, the large memory overhead of the key-value (KV) cache poses significant challenges in long-context scenarios. Existing training-free KV cache compression methods typically focus on quantization and token pruning, which have compression limits, and excessive sparsity can lead to severe performance degradation. Other methods design new architectures with less KV overhead but require significant training overhead. To address the above two drawbacks, we further explore the redundancy in the channel dimension and apply an architecture-level design with minor training costs. Therefore, we introduce CSKV, a training-efficient Channel Shrinking technique for KV cache compression: (1) We first analyze the singular value distribution of the KV cache, revealing significant redundancy and compression potential along the channel dimension. Based on this observation, we propose using low-rank decomposition for key and value layers and storing the low-dimension features. (2) To preserve model performance, we introduce a bi-branch KV cache, including a window-based full-precision KV cache and a low-precision compressed KV cache. (3) To reduce the training costs, we minimize the layer-wise reconstruction loss for the compressed KV cache instead of retraining the entire LLMs. Extensive experiments show that CSKV can reduce the memory overhead of the KV cache by 80% while maintaining the model's long-context capability. Moreover, we show that our method can be seamlessly combined with quantization to further reduce the memory overhead, achieving a compression ratio of up to 95%.

  **项目简介：** 本项研究致力于实现长文本情境下的大语言模型KV Cache压缩。本项研究基于KV Cache存在低秩结构的现象，创新性提出一种基于权重低秩分解和局部信息保护的KV Cache压缩算法，训练后最高可达80%的近无损压缩，进一步集成4bit量化感知训练后最高可达95%的综合压缩比，在当时处于领域内领先水平。本项研究产出专利一项和论文一篇，其中论文被NeurIPS ENLSP Workshop'24接收。

---

+ [ICML 2024] **Evaluating Quantized Large Language Models**. Shiyao Li, Xuefei Ning, **Luning Wang**, Tengxuan Liu, Xiangsheng Shi, Shengen Yan, Guohao Dai, Huazhong Yang, Yu Wang.

  **Abstract:** Post-training quantization (PTQ) has emerged as a promising technique to reduce the cost of large language models (LLMs). Specifically, PTQ can effectively mitigate memory consumption and reduce computational overhead in LLMs. To meet the requirements of both high efficiency and performance across diverse scenarios, a comprehensive evaluation of quantized LLMs is essential to guide the selection of quantization methods. This paper presents a thorough evaluation of these factors by evaluating the effect of PTQ on Weight, Activation, and KV Cache on 11 model families, including OPT, LLaMA2, Falcon, Bloomz, Mistral, ChatGLM, Vicuna, LongChat, StableLM, Gemma, and Mamba, with parameters ranging from 125M to 180B. The evaluation encompasses five types of tasks: basic NLP, emergent ability, trustworthiness, dialogue, and long-context tasks. Moreover, we also evaluate the state-of-the-art (SOTA) quantization methods to demonstrate their applicability. Based on the extensive experiments, we systematically summarize the effect of quantization, provide recommendations to apply quantization techniques, and point out future directions.

https://arxiv.org/pdf/2402.18158.pdf

  **项目简介：** 本项研究对于低比特量化技术对大语言模型性能的影响做了综合全面的评测研究，覆盖张量维度、模型维度、量化方法维度、任务维度等。本项研究为业界首个量化大模型的综合评测工作，产出论文被国际顶级会议ICML'24接收，并获得领域内广泛认可，目前已获得约100次谷歌学术引用。

---

+ [NeurIPS ENLSP Workshop 2023] **LLM-MQ: Mixed-precision Quantization for Efficient LLM Deployment**. Shiyao Li, Xuefei Ning, Ke Hong, Tengxuan Liu, **Luning Wang**, Xiuhong Li, Kai Zhong, Guohao Dai, Huazhong Yang, Yu Wang. 

  **Abstract:** Large Language Models (LLMs) have demonstrated impressive performance across various tasks. Nevertheless, deploying LLMs on edge devices presents significant challenges, primarily due to their substantial model size (e.g., over 10 billion parameters). Low-precision quantization is a promising way to reduce the memory requirement of LLMs. However, directly applying ultra-low-bit quantization to LLMs leads to significant performance degradation and fails to meet a specific weight memory budget. In this paper, we propose LLM-MQ, a Mixed-precision Quantization method, to address the above issues. Our method mainly contains three folds: (1) We propose a sparse outlier protection strategy for low-precision layers by protecting the outliers in FP16 format to maintain the performance. (2) We propose sensitivity-based precision allocation to assign the proper bit-width for each layer within the given budget for weight memory based on their first-order information and quantization error. (3) We develop efficient CUDA core kernels to accelerate mix-precision LLMs by fusing the dequantization and General Matrix-Vector Multiplication (GEMV). With comparable performance on various tasks, LLM-MQ can flexibly quantize LLMs that meet the given budget for weight memory. On NVIDIA T4 GPU, we achieve up to 1.6× end-to-end speedup compared to the pytorch FP16 baseline.

https://nicsefc.ee.tsinghua.edu.cn/%2Fnics_file%2Fpdf%2F5c805adc-b555-499f-9882-5ca35ce674b5.pdf

  **项目简介：** 本项研究基于大模型内部对于低比特量化敏感度分布不均的现象，创新性提出了一种混合量化算法，其中主要包括离群值的高精度保护策略与基于敏感性的位宽分配策略，最高可达2.8bit的近无损压缩，在当时达到领域内先进水平。本项研究产出专利一项和论文一篇，其中论文被NeurIPS ENLSP Workshop'23接收。

---

**个人总结：**

本人在大语言模型领域具有超过两年的科研与工作经验，致力于大模型压缩与大模型推理优化方向，并对于大模型生产部署等具有充足实践经验。此外，本人对于大模型算法调优、大模型智能体等相关方向均有所涉猎，具备大模型全栈知识与技能。

  
