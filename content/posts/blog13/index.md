---
title: "Build a Hierarchy Model for Building Energy Saving Facing Engineering Data Differentiation"
date: 2023-03-24T20:40:01+08:00
draft: false
mermaid: true
author: Carry HE
---

# Background

Increasing accumulated engineering data are attracting researchers to feed real data to mathematical modes representing physical systems due to the boring previous practice where relevant crowds chose train models using simulation data.

However, the uncontrollability of engineering big data causes other troubles for us. The diversity of engineering data makes it difficult to build models for buildings. Of course, modeling one by one is a plausible way to avoid the problem of the differentiation of inputs, but it will make this industry more labor-intensive rather than brain-intensive. Alternatively, building a relatively general mathematical model for most of the buildings around the world makes data preprocessing important unprecedentedly. (*Don't lose hope, although GPT can theoretically analyze the status quo of every building's energy consumption. I still believe someplace has room to maneuver.*)

# Prototype

Traditionally, if we wanna know how to reduce energy consumption or spike the energy efficiency for certain buildings in the future, we have to know the future energy consumption which would follow the current pattern, which means it is really important to build an energy prediction model that fits different kinds of building. Given the diversity of engineering big data, we can build a hierarchy model to output different scale results, like the next merely illustrative flowchart.

{{<mermaid>}}
flowchart TD
    A[Engineering Big Data] --> B(Classification)
    B -->|input 1| C[cursory-scale data]
    B -->|input 2| D[middle-scale data]
    B -->|input 3| E[fine-scale data]
    C -->|output 1| F[cursory-scale analysis]
    D -->|output 2| G[middle-scale analysis]
    E -->|output 3| H[fine-scale analysis]
{{</mermaid>}}