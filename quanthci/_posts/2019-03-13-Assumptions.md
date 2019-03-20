---
layout: post
title: "Statistical Assumptions"
date: 2019-03-13
---
The following is an exploration of the statistical assumptions of linear models.

## Preparation
For the purpose of this analysis, the dataset used presents the following setup, similar to the previous post:
* IV1: device
* IV2: lighting
* DV: reading time

The residuals are added using **add_residuals**, on top of the linear model constructed similar to the last post. 

## Visualizing the residuals
Using **gplot** :
<p align="center">
<img src="/assets/images/resid_device.png" width="400">
<img src="/assets/images/resid_lighting.png" width="400">
</p>

Using **qqplot** :
<p align="center">
<img src="/assets/images/qqplot.png" width="400">
</p>

## Normality assumption: Lillefors test
The null hypothesis is: residuals are normally distributed.
The results for the Lillefors test, using **lillene.test** from **nortest** package have a p-value of 0.3991, which is higher than 0.05, which can be interpreted as the residuals being aproximately normally distributed.

## Equal variance assumption
### Brown-Forsythe test
The null hypothesis is: variance of the groups are roughly the same.
Using **levene.test** from **lawstat**, with the difference from median (not from mean), the p-values are:
* 0.9405 for device
* 0.9584 for lighting

Both are above 0.05, being interpreted as roughly equal variance.

### Non-constant variance score test
Using **ncvtest** from **car**, the results were 0.72234 for the p-value and 0.1262595 for the chiquare value.

## Transformations
### Log transformations
In case the statistical assumptions aren't met, the data can be transformed. One such example is the log transformation, for example (even though it is not the case):
```
m_log <- lm(log(ReadingTime) ~ Device, data = data)
```

### Aligned Rank Transform
The results are computed and displayed using: **art** from **ARTool**, **sigmaHat** from **car**,**confint** from **tidy**.
To get the aligned ranks, for example:
```
art_Device = art_result$aligned.ranks$Device
```

Below is a plot depicting Cohen's ds and their confidence intervals:
<p align="center">
<img src="/assets/images/cohend.png" width="400">
</p>

## Comparison of residuals:
<p align="center">
<img src="/assets/images/comparison_resid.png" width="400">
</p>

## Generalized linear model
Another dataset was used for this purpose, reporting the following:
* Admission to university: (0=No, 1=Yes)
* GRE score

The model is fit and predictions are plotted using: **Anova** from **car** and **add_predictions** from modelr.
```
m_logit_cont <- glm(admit_fct ~ gre, data = gpa_admit, family = binomial(link = "logit"))
anova_cont <- Anova(m_logit_cont, type = "II")
anova_cont
```

Below is a plot depicting the predictions of admission based on GRE score:
<p align="center">
<img src="/assets/images/prediction.png" width="400">
</p>

The full code can be viewed at [this link](https://github.com/bianca-stancu/QuantHCI2019/blob/master/linear_models.R).

