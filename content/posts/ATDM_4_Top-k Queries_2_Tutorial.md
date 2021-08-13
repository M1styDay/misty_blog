---
title: Top-k Queries：Tutorial
author: "Misty"
tags: ["HKU","COMP 7801","Top-k Queries"]
categories: ["Advanced Topics in Data Management"]
date: 2021-02-19
---


## TA & NRA
### Qustion
A website posts information about apartments. Suppose that there are 10 apartments to be sold, together with their ratings($a_1$) and prices($a_2$), as listed in the table below. The website employs an aggregation function f = 0.6*$a_1$+ 0.4*$a_2$ to rank these apartments.

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210308230026.png)

Q1) Write down two lists of apartments, in descending order of $a_1$ and $a_2$.

Q2) Use the TA algorithm to find the two best apartments in terms of f. Write down your steps.

Q3) Use the NRA algorithm to find the two best apartments in terms of f. Write down your steps.

Q4) Which of the TA and NRA solutions requires fewer iterations?

### Answer

A1）

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210308230110.png)

A2)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210308230215.png)

A3)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210308230241.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210308230319.png)

A4)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210308230345.png)
