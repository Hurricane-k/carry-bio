---
title: "My Attempts to Build a Rule-Based, Relatively Convenient Data-Preprocessing Framework for HVAC Engineering Data"
date: 2023-04-13T10:39:32+08:00
draft: false
mermaid: true
author: Carry HE
---


# Background

Large-scale Language Model (LLM) is eye-catching all around the world. It outshines other AI branches in reputation. In other words, describing LLM as the masterpiece set is ok. Some ideas derived from LLM also inspire other branches, like Prompt Learning. OpenAI has stirred up the madness that many tech giants put much effort into LLM. I want to talk about Chinese LLM especially. There is no debate that [BAIDU WenXiYiYan](https://yiyan.baidu.com) got its moment recently. Some people analyzed the technical or knowledge gap between the Chinese generative pre-trained transformer model (C-GPT) and OpenAI GPT. We cannot ignore that the excellent corpus is different in quantity and quality.

<div align=center><img src="blog15-bg1Eng.png"></div>

<div align=center><img src="blog15-bg2Eng.png"></div>

Clearly, the valuable data accounts for a small percentage, which is not limited to the natural language model. In terms of HVAC engineering data, the shortage is more severe. Some phenomena can explain that:

1. The building energy consumption monitoring platforms are at the initial stage of development. There are many differences among platforms in quality, which is a typical feature. People put much more emphasis on the quantity of the platforms with the sacrifice of the quality.
  
2. The Covid-19 pandemic pauses or breaks the consistent record more or less, including building energy consumption and other relevant data. The inconsistent data would put some obstacles to data analysis and mining. But look on the bright side; it might be an opportunity to challenge some existing AI methods in practice.
  
3. Some maintainers are not equipped with enough expertise to find some platform-related problems in time, which would make platforms record tons of abnormal data over a long period.

# Analysis for Status Quo of HVAC Engineering Data

# Reference

1. [The Chinese online comunities are dying out, and who is killing the future of China's AI? [What is the obstacle of domestic ChatGPT]](https://www.bilibili.com/video/BV1Nm4y1z7AT?share_source=copy_web)