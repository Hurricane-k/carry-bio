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
&nbsp;

# Energy-Saving analysis based on key parameters

To out best knowledge, If we only have cursory-scale data in hand, the cursory-scale energy consumption is the corresponding output. For example, we could define the corresponding cursory-scale output as `total electricity consumption of HVAC`, the corresponding middle-scale output as `total electricity consumption of the chiller group`, and the corresponding fine-scale as <font color=green>other data</font>, like `water flow`,`water temperature leaving chiller #1`. As a side note, the range of <font color=green>other data</font> are too much broad, no planned models to predict the future situation of 'other data' we mentioned data. If we have them, just take as the full advantage of them as you can. As the previous papers proposed, instead of many parameters, a few parameters (we can say 'key parameters') can predict `total electricity consumption of HVAC` , I listed some results in the mindmap. However, the more advaced control deployed in building, many keys parameters are not fixed numbers, or cannot be presented by number. Some related study might as well follow the development of the construction industry. And the similar methods could be used to find which are the key paramters to perdict middle-scale output other than `total electricity consumption of HVAC`

{{<mermaid>}}
mindmap
  root((accuracy in prediction))
    relatively high 
      the type of plant
      the type of end use
      the type of water system
      building shape coefficient
      building area
      average summer temperature
      building sceduled time
      equipment density
      window wall ratio
      designated indoor summer temperature
      occupancy desnity
      lighting density
    middle
      the type of plant
      building area
      average summer temperature
      building sceduled time
      equipment density
      window wall ratio
      designated indoor summer temperature
      occupancy desnity
    relative low
      the type of plant
      building area
      average summer temperature
      building sceduled time
      equipment density
      window wall ratio
{{</mermaid>}}
&nbsp;

The key parameters (as model inputs) and the corresponding output have determined the structure of the mathematical models. You can try various models to pick up one of them based on the model performance. In order to finish the whole prcoess, the simulation data would replace the real enigneering data and train the mathematical models. How to get the enough simulation data that meet our requiement? That is the one thing I'm gonna talk about in the next section.

# Reference
1. Zhu, M. The construction of minimum variable set for energy prediction models of office building. Tongji University,2018.
2. Sha, H., Xu, P., Yan, C. et al. Development of a key-variable-based parallel HVAC energy predictive model. Build. Simul. 15, 1193–1208 (2022).