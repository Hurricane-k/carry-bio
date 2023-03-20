---
title: "How to Build a Loop to Train Agents in Virtual Environments for Building Energy-Efficiency Improvement"
date: 2023-03-19T15:42:13+08:00
draft: false
mermaid: true
author: Carry HE
---

# Background

Researchers have proven the potential of (Deep) Reinforcement Learning in improving building energy efficiency. The maturity of digital infrastructure motivates more and more companies to embark on deploying RL / DRL in reality because we are stuck in PID control for so long! During my internship, I summarized how to train RL in a virtual environment that is created by the actual building, which sounds like a hot concept '[MPC (Model Predictive Control)](https://www.sciencedirect.com/science/article/pii/S1367578820300584)', but they are essentially different.

RL only needs one environment, regardless of the virtual or actual environment. Here, the emphasis is put on a virtual environment just for pre-training agents. In another word, if we train RL in the actual environment, the whole building operation would be so unstable to get complaints that are what we don't want. But in MPC, a virtual environment (or we can say, model) is a bridge connecting the control algorithms (can be RL or other methods) and the actual environment. The former Sequence diagram illustrates the workflow of RL/DRL, and the latter shows the simplified workflow of MPC.

{{<mermaid align="center">}}
sequenceDiagram
    Control Method->> Environment: command N based on the feedback from N-1
    Environment-->>Control Method: feedback N based on the commnand from N

    Control Method->> Environment: command N+1 based on the feedback from N
    Environment-->>Control Method: feedback N+1 based on the commnand from N+1

    Control Method->> Environment: command N+2 based on the feedback from N+1
    Environment-->>Control Method: feedback N+2 based on the commnand from N+2
{{</mermaid>}}
&nbsp;

{{<mermaid>}}
sequenceDiagram 
    Environment ->> Model: Information N+1 based on information iteration N——update Model
    Model ->> Control Method: Output N+1 based on information N+1&information iteration N
    Control Method-->> Environment: Command N+1 based on Output N+1

    Environment ->> Model: Information N+2 effected by Output N+1&Command N+1——update Model
    Model ->> Control Method: Output N+2 based on information N+2
    Control Method-->> Environment: command N+2 based on Output N+2

    Environment ->> Model: Information N+3 effected by Output N+2&Command N+2——update Model
    Model ->> Control Method: Output N+3 based on information N+3
    Control Method-->> Environment: command N+3 based on Output N+3
{{</mermaid>}}
&nbsp;

# References

1. Drgoňa, J. et al. (2020) All you need to know about model predictive control for buildings. *Annual reviews in control.* [Online] 50190–232