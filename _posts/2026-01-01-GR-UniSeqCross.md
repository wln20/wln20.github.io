---
title: '统一序列建模与特征交叉——论文精读笔记合集'
date: 2026-01-01
permalink: /posts/2026/01/GR-UniSeqCross/
tags:
  - 推荐系统
  - 特征交叉
  - 长序列建模
---

在以往的精排系统中，序列建模（对于用户历史序列的处理）和特征交叉模块通常是分开的：序列建模是将用户历史序列处理成目标物品感知的表征，例如使用DIN、DIEN、SIM、Longer等来通过target attention思想提取序列中的重要信息；特征交叉是学习非序列特征（如用户画像特征、目标物品特征、上下文特征等）和历史序列特征之间的高阶交叉，例如使用FM、WuKong、RankMixer等进行特征交叉。这种“先建模历史序列再将建模后的序列和其他非序列特征进行交互“的两阶段范式在表征能力、优化难度和系统效率上都有不足。因此，OneTrans等工作希望通过一个单一的模型来统一进行序列建模和特征交叉，从而打破序列特征和非序列特征在模型结构上的隔离。

本部分将持续更新统一序列建模与特征交叉相关工作的精读笔记：

- <a href="/post_html/GR-UniSeqCross/OneTrans.html">统一序列建模与特征交叉 —— 字节 OneTrans 精读笔记</a>（2025.10）
- <a href="/post_html/GR-UniSeqCross/HyFormer.html">统一序列建模与特征交叉 —— 字节 HyFormer 精读笔记</a>（2026.01）
- <a href="/post_html/GR-UniSeqCross/MixFormer.html">统一序列建模与特征交叉 —— 字节 MixFormer 精读笔记</a>（2026.02）


