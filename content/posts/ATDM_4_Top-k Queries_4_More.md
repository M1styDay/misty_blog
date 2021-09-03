---
title: Top-k Queries：Supplement
author: "Misty"
tags: ["HKU","COMP 7801","Top-k Queries"]
categories: ["Advanced Topics in Data Management"]
date: 2021-02-17
---


## Threshold Algorithm (TA) 

* Original version, often used as synonym for entire family of top-k algorithms.
* But: eager random access to candidate objects required.
* Worst-case memory consumption is strictly bounded → O(k)


![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210317143350.png)

## No-Random-Access Algorithm (NRA) 

* No random access required at all, but may have to scan large parts of the index lists.
* Worst-case memory consumption bounded by index size → O(m*n + k)


![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210317153713.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210317210135.png)