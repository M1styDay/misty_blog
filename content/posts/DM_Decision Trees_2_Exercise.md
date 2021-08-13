---
title: Decision Trees：Exercise
author: "Misty"
tags: ["Decistion Trees","HKU"]
categories: ["Data Mining"]
date: 2021-04-09
---

# Decision Trees：Exercise

## Question

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210416115012.png)

Construct a decision tree with the following properties:
1. Choose the best split based on GINI index;
2. Stopping rule: when gini value=0 or no further split is possible;
3. Class of a leaf is determined by majority rule. If ties use the default class (NM).

## Answer

### Building Decision Tree

#### Step 1

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210416115233.png)

#### Step 2

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210416121533.png)


#### Step 3

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210416121556.png)



### Predicting

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210416121649.png)




### Post Pruning

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210416121731.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210416121750.png)