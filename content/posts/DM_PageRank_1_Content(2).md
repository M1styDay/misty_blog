---
title: PageRank：Content(2)【Not finish】
author: "Misty"
tags: ["PageRank","HKU"]
categories: ["Data Mining"]
date: 2021-03-10
---

# The Theory behind PageRank

## Computing Importance

* Web graph: a directed graph G = (V , E ) where nodes represent web pages, while there is a directed edge between u and v if there is a hyperlink between the corresponding web pages.
* Importance of v is proportional to the importance of nodes linking to v. 
* It can be modeled by a system of linear equations...

## System of Linear Equations for PageRank

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210323163538.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210323163631.png)

## PageRank

* The importance of a web page can be computed by solving the corresponding system of linear equations.
* However there are two main issues: 
    * The solution might not be unique!
    * It is expensive to solve large system of linear equations. Gaussian elimination requires Ω($n^3$) operations.

### Eigenvector Computation

* The vector x is an eigenvector of the matrix A with eigenvalue λ if Ax = λx.
* Therefore, one could compute the importance of web pages by computing an eigenvector with eigenvalue 1 of $M_G$ , which is also very expensive!