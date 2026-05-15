---
layout: publication

title: "Simpler is Better: Finding the Best Reward Function in Long Chain-of-Thought Reinforcement Learning for Small Language Models"

authors:
  - "Luning Wang"
  - "Zichen Zhang"
  - "Junkuan Liu"

year: 2025

pdf_url: "/files/dynamic_reward.pdf"

abstract: "Large Language Models (LLMs) have been evolving rapidly in recent years. A critical technology that contributes to this development is Reinforcement Learning (RL). Recently, strong LLMs like DeepSeek-R1, which show very promising performance on complex reasoning tasks such as solving math and coding problems, have adopted verifiable rules-based rewards. Rule-based rewards are pre-defined, so they are more interpretable and controllable by developers and could be adapted for different reasoning tasks. Subsequent paper further discuss the mechanics of long CoT reasoning, and propose to use reward shaping to stabilize and control CoT length while improving accuracy. Specifically, they propose cosine reward with a repetition penalty, which could stabilize CoT growth while encouraging emergent reasoning behaviors such as branching and backtracking. However, there lacks the discussion on the effect of those different types of rewards on small language models (SLMs), which typically have a parameter size $<$7B and could behave differently from those large models. Therefore, We focus on the effect of different rewards on small models. We first propose a dynamic reward that extends the concept of cosine reward, and then experiment several kinds of rewards (normal, cosine, dynamic) on the chosen SLMs. With careful observation and analysis, we provide several key insights which could benefit future studies in this field."

permalink: /publications/dynamic_reward/
---

This page hosts the paper PDF for Google Scholar indexing.
