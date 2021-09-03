---
title: Association：Exercise
author: "Misty"
tags: ["Association","HKU"]
categories: ["Data Mining"]
date: 2021-01-09
---

## Naive Algorithm 

### Pass 1

Support treshold：2

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314185542.png)

### Pass 2

Support treshold：2

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314185634.png)

### Pass 3

Support treshold：2

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314190351.png)

## A-priori Algorithm

### Pass 1

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314190518.png)

### Pass 2

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314190701.png)

### Pass 3

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314190827.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314190913.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314190933.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314190957.png)

## PCY Algorithm

### Input Data

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191315.png)

### Pass 1

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191451.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191534.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191602.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191621.png)

### Pass 2

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191652.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191750.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191810.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210314191832.png)

### The remaining passes

The remaining passes are the same of A-priori

## SON Algorithm

### Introduction

Let s be the support threshold:

* Pass 1:
    1. Divide the dataset into k chunks, let $p_i$ be such that the ith chunk contains a fraction of pi of the input dataset.
    2. Find the frequent itemsets in each chunk using any algorithm (e.g.A-priori), with support threshold = $p_i$ · s in each chunk i . Let $C_i$ be the set of frequent itemsets in the ith chunk (with support threshold $p_i$ · s).
* Pass 2:
    * Compute the support for each itemsets in $C_1$ ∪ $C_2$ ∪ · · · ∪ $C_k$ and return the frequent itemsets (with support threshold s).


Remark: When counting the number of passes over the input dataset we include only the passes on the disk, as data in main memory can be processed quickly. Hence, if each chunks fits into main memory (as it is usually the case) the total number of passes on the disk is two. Otherwise, we need to add the passes on the disk for processing each chunk.

### Input Data

Support threshold s = 4. Suppose we have the following 6 buckets:

* B1 = {ab}
* B2 = {abc}
* B3 = {cd}
* B4 = {abe}
* B5 = {abf}
* B6 = {ef}

### Pass 1
Suppose the first chunk $C_1$ = {B1, B2, B3}, while $C_2$ = {B4, B5, B6}. 

Find the frequent itemsets per chunk with support threshold s · $p_i$ = 4/2 = 2

For the first chunk the frequent itemsets are $C_1$ = {a, b, c, ab}

For the second chunk the frequent itemsets are $C_2$ = {a, b, e, f , ab}

### Pass 2

The frequent itemsets in $C_1$ ∪ $C_2$ with support s = 4 are {a, b, ab}.