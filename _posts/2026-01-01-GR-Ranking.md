---
title: '生成式排序——论文精读笔记合集'
date: 2026-01-01
permalink: /posts/2026/01/GR-Ranking/
tags:
  - 推荐系统
  - 生成式排序
---

生成式排序（Generative Ranking）是一类借助生成式模型思想来解决排序问题的推荐策略，它通常在训练阶段采用“预测下一个行为”等生成式任务作为目标之一，结合传统的目标如CTR分数预测等，在训练阶段让模型学会预测“用户针对给定目标物品会有什么反应”。在推理阶段则本实际上还是一个分数预测器，本质上可以理解为利用Transformer架构建模用户历史并和目标物品做交叉，从而在深刻理解用户兴趣的情况下作出预测，和传统DLRM在推理阶段的表现其实差不多。

本部分将持续更新生成式排序相关工作的精读笔记：

- <a href="/post_html/GR-Ranking/HSTU.html">生成式排序 —— Meta HSTU 精读笔记</a>（2024.02）
- <a href="/post_html/GR-Ranking/GenRank.html">生成式排序 —— 小红书 GenRank 精读笔记</a>（2025.05）
- <a href="/post_html/GR-Ranking/MTGR.html">生成式排序 —— 美团 MTGR 精读笔记</a>（2025.05）

注：本部分主要关注的是在范式上将判别式打分任务转化为生成式范式（主要在训练阶段）的工作，如HSTU中将“预测target item的得分”重构为“预测target item的下一个action”。
