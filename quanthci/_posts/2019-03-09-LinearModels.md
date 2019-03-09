---
layout: post
title: "Linear Models"
date: 2019-03-09
---
The following is an exploration of models, in the following scenarios:
* One independent variable
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

## Linear models
Following is an overview of the different way to analyze the data using the package **stats**.

### One IV
If only one indepedent variable is analyzed, for example the Device in the current case, the model will be formulated as:
```
lm(ReadingTime ~ Device, data = data)
```

The results can then be viewed as a table or in a textual form, such as:
> The effect of Device is significant (F(2, 57) = 3.91, p < .05) and can be considered as medium (Partial Omega-squared = 0.090).

### Two IVs
The models for two independent variables can either take or not account of the interaction factor. A simple model, without accounting the interaction between the two variables, is:
```
lm(ReadingTime ~ Device + Lighting, data = data)
```
In order to formulate a model that does account for the interaction, the following should be performed:
```
lm(ReadingTime Device * Lighting, data = data)
```

Below is the table depicting the results: 
<img src="/assets/images/anova_interaction.png" width="400">

> The effect of Lighting is significant (F(3, 48) = 6.49, p < .001) and can be considered as large (Partial Omega-squared = 0.22). The effect of Device is significant (F(2, 48) = 4.65, p < .05) and can be considered as medium (Partial Omega-squared = 0.11). The interaction between Lighting and Device is not significant (F(6, 48) = 0.047, p > .1) and can be considered as medium (Partial Omega-squared = 0.11).