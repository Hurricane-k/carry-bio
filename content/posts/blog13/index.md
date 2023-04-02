---
title: "Build a Hierarchy Model for Building Energy Saving Facing Engineering Data Differentiation"
date: 2023-03-24T20:40:01+08:00
draft: false
math: true
mermaid: true
author: Carry HE
---

<div align=center><img src="blog13-cover.jpg"></div>

# Background

Increasing accumulated engineering data are attracting researchers to feed real data to mathematical modes representing physical systems due to the boring previous practice where relevant crowds chose train models using simulation data.

However, the uncontrollability of engineering big data causes other troubles for us. The diversity of engineering data makes it difficult to build models for buildings. Of course, modeling one by one is a plausible way to avoid the problem of the differentiation of inputs, but it will make this industry more labor-intensive rather than brain-intensive. Alternatively, building a relatively general mathematical model for most of the buildings around the world makes data preprocessing important unprecedentedly. (*Don't lose hope, although GPT can theoretically analyze the status quo of every building's energy consumption. I still believe someplace has room to maneuver.*)

# Prototype

Traditionally, if we wanna know how to reduce energy consumption or spike the energy efficiency for certain buildings, endless field studies cannot be avoided because the energy consumption would be accessed much easier than <font color=red>other data</font>, like water temperature (e.g. Low deltaT). But other data is the deep root of low energy efficiency. If we can get model where <font color=red>other data</font> is defined as inputs and energy consumption, we can use some methods in calculating <font color=red>other data</font> inversely. <font color=red>Other data</font> is included in key paramters we will mention later. <font color=red>Other data</font> can help us to know why the energy efficiency is low or high. So building a energy consumption estimation model is imperative. Given the diversity of engineering big data, we can build a hierarchy model to output ***different scale energy consumption***.

{{<mermaid>}}
flowchart LR
    A[Engineering\n Big Data] --> B(Classification)
    B --> C["cursory-scale\n energy\n consumption"]
    B --> D["middle-scale\n energy\n consumption"]
    B --> E["fine-scale\n other data"]
    C --> F["total electricity\n consumption of HVAC"]
    C --> FF["total electricity\n consumption of plant"]
    D --> G["total electricity\n consumption of\n the chiller group"]
    D --> GG["total electricity\n consumption of\n other equipment"]
    D --> GGG["total electricity\n consumption of\n other equipment groups"]
    E --> H["data about operation"]
    E --> HH["data except operation"]
    H --> I["water temperature"]
    H --> II["water flow"]
    H --> III[...]
    HH --> J[key paramters]
    HH --> JJ[other than\n key parameters]
{{</mermaid>}}

To our best knowledge, If we only have cursory-scale data in hand, the cursory-scale energy consumption is the corresponding output. For example, we could define the corresponding cursory-scale output as `total electricity consumption of HVAC`, the corresponding middle-scale output as `total electricity consumption of the chiller group`. In terms of <font color=red>other data</font>, like `water flow`, `water temperature leaving chiller #1`. The range is too much broad, If we have them, just take as full advantage of them as you can.

{{<mermaid>}}
flowchart TD
    A[Hierarchy Model] --> B[cursory-scale energy consumption]
    A --> C[middle-scale energy comsuption]
    A --> D[data about operation]
    B & C --> E[energy consumption \nestimation model\n respectively]
    E --> F[reserve calculate\n key parameters]
    F --> G[comparison with\n recommended threshold] 
    D --> H[data preprocessing]
    H --> J[check the operaiton\n of HVAC system]
    {{</mermaid>}}
&nbsp;


# Energy-Saving analysis based on key parameters

As the previous papers proposed, instead of many parameters, a few parameters (we can say 'key parameters') can predict `total electricity consumption of HVAC` , I listed some results in the mindmap. However, with the more advanced control deployed in buildings, many key parameters are not fixed numbers or cannot be presented by number. Some related studies might as well follow the development of the construction industry. And similar methods could be used to find which are the key parameters to predict middle-scale output other than `total electricity consumption of HVAC`

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

The key parameters (as model inputs) and the corresponding output have determined the structure of the mathematical models. You can try various models to pick up one of them based on the model performance. In order to finish the whole process, the simulation data would replace the real engineering data and train the mathematical models. How to get enough simulation data that meet our requirements? That is the one thing I'm gonna talk about in the next section.

# Generation of Simulation Data based on Latin Hypercube Sampling

You can get the basic knowledge about Latin hypercube sampling [online](https://en.wikipedia.org/wiki/Latin_hypercube_sampling). We plan put most of emphasis on the practice. First, I'll introduce the toolkits engaged.

1. Coding Language is Python, and the core third party package is [pyDOE](https://pythonhosted.org/pyDOE/randomized.html). However, there are other alternatives. For example, [scipy](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.qmc.LatinHypercube.html) has the similar function `scipy.stats.qmc.LatinHypercube`. According to the chosen key parameters and their respective range, you can get many sets of samples.
  
2. [Grasshopper](https://en.wikipedia.org/wiki/Grasshopper_3D#:~:text=Grasshopper%20is%20a%20visual%20programming,dragging%20components%20onto%20a%20canvas.) is a tool that can generate models based on the sampling results in a short period of time. You might have heard a buzzword '[**Parametric Design**]()'. In this step, you can turn to your Lab's mates for help. But, if you are really interested in this part and can't wait to do in person, Video tutorials wait you to explore (I will give you [a merely illustrative example](https://www.youtube.com/watch?v=cPUJ99mJAoE)). But, more importantly, you need to use other plug-in to convert the parametric designs to the file format supported by some certain simulation softwares. You can check [this website](https://www.food4rhino.com/en/app/ladybug-tools) to find something useful. I am not really familar with this, only help you to this point. Cooperation sometimes really is valuable.
  
3. I choose to export parametric desgin results as `.idf` files, which is supported by EnergyPlus. In order to save the simulation time consuming in EnergyPlus, [*Running in parallel process in Eppy*](https://eppy.readthedocs.io/en/latest/runningeplus.html#Running-in-parallel-processes) will surprise you. My first hand experience is that parallel process cannot be run on Windows OS. But that can work out on Linux OS. So I choose Linux OS ultimately.
  
4. After fininshing the parallel process, You can use these data to build models to predict different scale energy comsumption. From Linear Regression to other fancy algorithms, you can find corresponding python package to achieve your goals.

# How to use Key Parameters to Analyze Building Energy Efficiency

Taken Chinese National Construction Code as an example, Chinese National Construction Code dedicate the recommended threshold for some parameters. I summarized some values in the next table.

| No. | Building type | lighting density | equipment density | ... |
| --- | --- | --- | --- | --- |
| 1   | office building | $\leq 8 Watt/m^2$ | $\leq 15 Watt/m^2$ | ... |
| 2   | hotel | $\leq 6 Watt/m^2$ | $\leq 15 Watt/m^2$ | ... |
| 3   | shopping mall | $\leq 9 Watt/m^2$ | $\leq 13 Watt/m^2$ | ... |
| ... | ... | ... | ... | ... |

Comparison between the recommended threshold and actual value of parameters can help us know if this is the reason why the building energy consumption is high or energy efficiency is low.

As far as how to calculate key parameters (as input of models) inversely, some optimization methods are really helpful, like Particle Swarm Optimization(PSO) and Genetic Algorithm(GA).

# Conclusion

The blog focus is on ***the model-based method to analyze building energy consumption***, which means the cursory/middle-scale energy consumption get their moments. In the near future article, I will introduce how to utilize the fine-scale operation data to point out the operation problem happening to the building HAVC system.

# Acknowledge
1. Thanks for the lab's mates to help me fulfill the part of parametric design.
2. The first picture cited at the beginning is from [Unsplash.com](https://unsplash.com/) and Photographer [*Lukas Blazek*](https://unsplash.com/@goumbik)

# Reference

1. Zhu, M. The construction of minimum variable set for energy prediction models of office building. Tongji University,2018.
2. Sha, H., Xu, P., Yan, C. et al. Development of a key-variable-based parallel HVAC energy predictive model. Build. Simul. 15, 1193–1208 (2022).
3. [Latin hypercube sampling - Wikipedia](https://en.wikipedia.org/wiki/Latin_hypercube_sampling)  
4. [Randomized Designs &mdash; pyDOE 0.3.6 documentation](https://pythonhosted.org/pyDOE/randomized.html)
5. [scipy.stats.qmc.LatinHypercube &#8212; SciPy v1.10.1 Manual](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.qmc.LatinHypercube.html)
6. [Grasshopper 3D - Wikipedia](https://en.wikipedia.org/wiki/Grasshopper_3D#:~:text=Grasshopper%20is%20a%20visual%20programming,dragging%20components%20onto%20a%20canvas.)
7. [Parametric design - Wikipedia](https://en.wikipedia.org/wiki/Parametric_design#:~:text=Parametric%20design%20is%20a%20design,design%20intent%20and%20design%20response.)
8. [Parametric Design | Grasshopper Tutorial | Rhino 3d - YouTube](https://www.youtube.com/watch?v=cPUJ99mJAoE)
9. [Ladybug Tools | Food4Rhino](https://www.food4rhino.com/en/app/ladybug-tools)
10. [Running EnergyPlus from Eppy &#8212; eppy 0.5.62 documentation](https://eppy.readthedocs.io/en/latest/runningeplus.html#Running-in-parallel-processes)