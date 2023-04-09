---
title: "My First Engagement in Fault Detection with the Help of the Inspection Robot in the Chiller Plant"
date: 2023-04-08T14:45:46+08:00
draft: false
mermaid: true
author: Carry HE
---

# Background

Industrial Fault Detection and Diagnosis (I-FDD) are in the process of deployment in practice, which is inspiring and exciting. For example, the latest inspection robots showed up at the 4th BAIDU OpenI/O QIZHI Developers Conference, which has come to end. The robot is typically designed for the transformer substations, which take into account the complex layout (steps, slope, etc.). It occurs to me that my previous experience, in which I was involved in developing and testing the algorithms for FDD based on the inspection robot in the chiller plant. The recent events indicate the inevitable tendency to digitize the job of inspection. After all, the position related to plant inspection work is uncomfortable for people. The inspection robots can reduce the miserable burden for human beings to a certain degree.

# Goals

Our previous work aims at Fault Detection other than Fault Diagnosis. Both concepts are essentially different. Fault Detection is the foundation of Fault Diagnosis. Fault Diagnosis is the further step of Fault Detection. Our algorithm consists of a few parts: image recognition by RGB images, fault detection by infrared photos, fault detection by RGB images, and fault detection by audio. The inspection objects include the critical components in chiller plants: pipes, chillers, and water pumps. The above description dedicates that the inspection robot needs to be equipped with more than one camera sensor, more than one microphone (or audio sensor), and more than one infrared sensor.

{{<mermaid>}}
flowchart LR
    A[Our Solution\n for Fault Detection] --> B[Data]
    B --> B1[RGB images]
    B --> B2[infrared photos]
    B --> B3[audio]
    B1 --> B11[equipment photos]
    B1 --> B12[dial photos]
    B11 --> C1[equipment\n classification]
    B12 --> C2[inspect the pressure\n of pipes]
    B2 --> C3[inspect the temperature\n of equipment]
    B3 --> C4[detect whether or not\n equipment has problems]
{{</mermaid>}}
&nbsp;

# Details of audio-based Fault Detection

Generally, when a piece of equipment is in good condition, the sound that it generates would smooth. When equipment cannot work well, the sound usually becomes sharp. Our audio-based method utilizes this property. If we can determine the threshold between smooth and sharp sounds, some problems can be detected in time.

The typical signal process inspires this part. Discrete Fourier Transform (DFT) converts audio from the time domain to the frequency domain. Usually, the audio is a mix of the sound from the target and the sound from other equipment. So separating the target's and other equipment's sounds is essential before analyzing the frequency domain. DFT can help us do this. The result of DFT can give us a clear visualization of the frequency domain.

In our audio-based detection, we use the ARIMA model, usually applied in financial analysis, to fit the pump high-, medium-, and low-frequency domain signals. If the audio is non-smooth, the d-order difference operation is first performed to turn it into a smooth time series. For smooth audio, the ARIMA model is used directly. So we can identify smooth and other audio.

# Future Work

1. Regarding our audio-based Fault Detection, sharp sounds cannot represent all problems the engineers would come across. Given the lack of collection of abnormal audio, it is nearly impossible to analyze more sound-related features from equipment that operates in good condition. Deliberately damaging a piece of equipment is unaffordable. If the collection of sounds has more diversity, a more detailed analysis will help to develop a more refined audio-based Fault Detection method.