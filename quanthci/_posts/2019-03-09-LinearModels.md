---
layout: post
title: "Linear Models"
date: 2019-03-09
---
The following is an exploration of models, in the following scenarios:
* One independent variable
* Two independent variables
* Two independent variables with interaction

## Preparation
Load the dataset and transform the independent variables into factors using the **mutate** function from the **dplyr** package.

For the purpose of this analysis, the dataset used presents the following setup:
* IV1: device
* IV2: lighting
* DV: reading time

## Visualizing the data
For an initial view of the data, it can be plotted with the respect to the dependent variable using the **ggplot2** package. Below are example of plots of both IVs and each one separately, with respect to the reading time.

<img src="/assets/images/device_lighting.png" width="400">
<img src="/assets/images/device.png" width="400">
<img src="/assets/images/lighting.png" width="400">