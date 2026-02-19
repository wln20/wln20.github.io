---
title: '生成式排序——论文精读笔记合集'
date: 2026-01-01
permalink: /posts/2026/01/GR-Ranking/
tags:
  - 生成式推荐
  - 生成式排序
---

生成式排序（Generative Ranking）是一类借助生成式模型思想来解决排序问题的推荐策略，它将传统推荐中“匹配已有候选”或“基于分数预测→排序”的思想，转化为一种基于序列化建模直接生成排序结果的方式。

本部分将持续更新生成式排序相关工作的精读笔记：

- <a href="/post_html/GR-Ranking/HSTU.html">生成式排序 —— Meta HSTU 精读笔记</a>（2024.02）
- <a href="/post_html/GR-Ranking/GenRank.html">生成式排序 —— 小红书 GenRank 精读笔记</a>（2025.05）
- <a href="/post_html/GR-Ranking/MTGR.html">生成式排序 —— 美团 MTGR 精读笔记</a>（2025.05）

注：本部分主要关注的是在范式上将判别式打分任务转化为生成式范式的工作，如HSTU中将“预测target item的得分”重构为“预测target item的下一个action”。
