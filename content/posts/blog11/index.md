---
title: "What did I Learn from the first time of Engineering Data Preprocessing"
date: 2023-03-10T15:24:03+08:00
draft: false
mermaid: true
author: Carry HE
---

# Background

When I was Year Two student in my master's study, it was the first time to explore the potential of engineering big data related to building HVAC systems. Before that, I was used to using synthetic data to verify ideas due to its ***controllability***. If you have ever had similar experiences, you can understand what I mean. Although I was intuitively afraid of being involved in do with engineering data, I had no idea what is the core problem until I got a task.

# What's the task?

A property agency found that ***the frequency of fans in cooling towers is consistent all year around***, which means there was plenty of room to improve its operation for sake of energy-saving. As we all know, the building's thermal load changes along with the ambient temperature. The partial thermal load means the lower frequency still is able to process the thermal load. We can save energy consumption and reduce carbon emissions without sacrificing thermal comfort. The above analysis makes everything clear.

**The goal is a strategy for controlling the frequency of fans in cooling towers**. In order to make strategy easy to operate, my initial plan is to make a look-up table.

# What's the data we can make full use of?

The agency provided me with the data collected in half of the year 2020. Apart from every 15-minute electricity consumption, water temperature, water flow, the status of core equipment, and real-time frequency are available.

{{<mermaid>}}
mindmap
  root(("equipment & data"))
    Chillers
      Electricity Consumption
        every 15 min for each chiller
        every 15 min for all chillers
      Operation
        on or off
        current percentage
    Chilled Water Pumps
      Electricity Consumption
        every 15 min for each pump
        every 15 min for all pumps
      Main Water Flow in Chilled Water Loop
      real ime frequency of every pump
    Cooling Water Pumps
      Electricity Consumption
        every 15 min for each pump
        every 15 min for all pumps
      main water flow in cooling water loop
      real time frequency of every pump      
    Cooling Tower
      Electricity Consumption
        every 15 min for each fan
        every 15 min for all fans
      Main Leaving Water Temperature
      real ime frequency of every fan
    Others
      Ambient Temperature
      Relative Humidity
{{</mermaid>}}