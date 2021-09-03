---
title: Naive Bayes Class：Content
author: "Misty"
tags: ["Naive Bayes Class","HKU"]
categories: ["Data Mining"]
date: 2021-04-16
---

# Naive Bayes Class

## Bayes Classifier

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417185443.png)

### Example of Bayes Theorem

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417190339.png)

### Bayesian Classifiers

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417190608.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417190624.png)

## Naïve Bayes Classifier

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417190646.png)

### How to Estimate Probabilities from Data?

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417190930.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417190946.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417191006.png)

### Example of Naïve Bayes Classifier

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417191045.png)

### Note on Probability Density Functions

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417191113.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417191128.png)

## Naïve Bayes Classifier

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417191202.png)

### Example of Naïve Bayes Classifier

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417191241.png)

## Handling Missing values

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210417191312.png)

## Summary

* Robust to isolated noise points
* Handle missing values by ignoring the instance during probability estimate calculations
* Robust to irrelevant attributes 
* Independence assumption:
    * independence when class is given. 
        * Note: weaker assumption than full independence!
    * may not always hold
        * Use other techniques such as Bayesian Belief Networks (BBN)
