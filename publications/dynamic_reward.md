---
layout: default

scholar: true

title: "Simpler is Better: Finding the Best Reward Function in Long Chain-of-Thought Reinforcement Learning for Small Language Models"

authors:
  - "Luning Wang"
  - "Zichen Zhang"
  - "Junkuan Liu"

year: 2025

pdf_url: "/files/dynamic_reward.pdf"

abstract: >
  Large Language Models (LLMs) have evolved rapidly in
  recent years, with Reinforcement Learning (RL)
  playing a critical role in improving reasoning
  capabilities.

  Recent models such as DeepSeek-R1 demonstrate strong
  performance on complex reasoning tasks including
  mathematical problem solving and coding through the
  use of verifiable rule-based rewards.

  Prior work further explores the mechanics of long
  chain-of-thought (CoT) reasoning and proposes reward
  shaping methods, such as cosine rewards with
  repetition penalties, to stabilize CoT growth while
  encouraging emergent reasoning behaviors including
  branching and backtracking.

  However, the effects of different reward functions on
  Small Language Models (SLMs), typically under 7B
  parameters, remain underexplored.

  In this work, we systematically study the influence
  of different reward strategies on small models.

  We first propose a dynamic reward function that
  extends the concept of cosine rewards, and then
  compare several reward mechanisms including normal,
  cosine, and dynamic rewards on selected SLMs.

  Through detailed experimentation and analysis, we
  provide insights that may benefit future research on
  reinforcement learning for small language models.

permalink: /publications/dynamic_reward/
---

# Simpler is Better: Finding the Best Reward Function in Long Chain-of-Thought Reinforcement Learning for Small Language Models

## Authors

Luning Wang, Zichen Zhang, Junkuan Liu

## Abstract

Large Language Models (LLMs) have recently achieved
strong reasoning performance through Reinforcement
Learning (RL) and long chain-of-thought (CoT)
reasoning. This paper studies how different reward functions
affect the reasoning behavior of Small Language
Models (SLMs), particularly models under 7B
parameters. We propose a dynamic reward function extending
cosine rewards and compare multiple reward
strategies on reasoning benchmarks.

## Paper

[Download PDF](https://wln20.github.io/files/dynamic_reward.pdf)
