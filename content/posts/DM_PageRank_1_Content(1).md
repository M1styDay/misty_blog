---
title: PageRank：Content(1)
author: "Misty"
tags: ["PageRank","HKU"]
categories: ["Data Mining"]
date: 2021-03-10
---

# Data and Algorithms of the Web

## Link Analysis Algorithms & Page Rank

#### Link Analysis Algorithms

* Page Rank
* Hubs and Authorities
* Topic-Specific Page Rank
* Spam Detection Algorithms
* Other interesting topics we won't cover
    * Detecting duplicates and mirrors
    * Mining for communities

#### Ranking Web Pages

* Web pages are not equally “important”
* www.bernard.com and www.stanford.edu both contain both the term “stanford” but:
    * www.stanford.edu has 23,400 webpages linking to it
    * www.bernard.com has 10 webpages linking to it
* Are all webpages linking to www.stanford.edu equally important?
    * The webpage of MIT is more “important” than the webpage of a friend of bernard
* Recursive definition of importance

## Simple recursive formulation

### Introduction

* The importance of a page P is proportional to the importance of pages Q where Q -> P (predecessors).
* Each page Q votes for its successors. If page Q with importance x has n successors, each succ. P gets x/n votes
* Page P's own importance is the sum of the votes of its predecessors Q.

### Simple "flow" model

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323112627.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323124308.png)

### Solving the flow equations

* 3 equatins, 3 unknows, no constants
    * No unique solution
    * All solutions equivalent modulo scale factor
* Additional constraint forces uniqueness
    * y + a + m =1
    * y = 2/5, a= 2/5, m =1/5
* Gaussian elimination method works for small examples, but we need a better method for large graphs

## Matrix formulation

### Introduction

* Matrix M has one row and one column for each web page (n x n, where n is the num of pages)
* Suppose page j has k successors
    * If j -> i, then M(ij) = 1/k
    * Else M(ij) = 0
* M is a column stochastic matrix
    * columns sum to 1
* Let r be the rank vector where:
    * $r_i$ is the improtance score of page i
    * |r| = 1

### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323130355.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323130423.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323172410.png)

## Eigenbector formulation

### Introduction

* The system of linear eq. can be written
    * r = Mr
* So the rank vector is an eigenvector of the stochastic web matrix
    * In fact, its first or principal eigenvector, with corresponding eigenvalue...
* Definition. The vector x is an eigenvector of the matrix A with eigenvalue λ (lambda) if the following equation holds: Ax = λx.

### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323131329.png)



## Power Iteration method

### Introduction

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323132025.png)


### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323134508.png)


## Random Walk Interpretation & The stationary distribution

### Random Walk Interpretation

* Imagine a random web surfer
    * At any time t, surfer is on some page P
    * At time t+1, the surfer follows an outlink from P uniformly at random
    * Ends up on some Page Q linked from P
    * Process repeats indefinitely
* Let P(t) be a vector whose ith component is the probability that the surfer is at page i at time t
    * P(t) is a probability distribution on pages


### The stationary distribution

* Where is the surfer at time t+1?
    * follows a link uniformly at random
    * P(t+1) = Mp(t)
* Suppose the random walk reaches a state such that p(t+1) = Mp(t) = p(t)
    * Then p(t) is called a stationary distribution for the random walk
* Our rank vector r satisfies r = Mr
    * So it is a stationary distribution for the random surfer

### Existence and Uniqueness

* A central result from the theory of random walks (aka Markov processes):
    *  For graphs that satisfy certain conditions, the stationary distribution is unique and eventually will be reached no matter what the initial probability distribution at time t = 0.

* 随机游走random walks实际上叫做马尔科夫过程Markov processes或者first order Mark, order Markov processes。

* 平稳分布的条件：非周期，状态连通

### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323140154.png)







## Problem & Solution

### Problem: Spider traps

#### Description

* A group of pages is a spider trap if there are no links from within the group to outside the group
    * Random surfer gets trapped
* Spider traps violate the conditions needed for the random walk theorem

#### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323140827.png)


### Solution: Random teleports

#### Description

* The Google solution for spider traps
* At each time step, the random surfer has two options:
    * With probability β, follow a link at random
    * With probability 1-β, jump to some page uniformly at random
    * Common values for β are in the range 0.8 to 0.9
* Surfer will teleport out of spider trap within a few time steps

#### Example(β = 0.8)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323143618.png)


### Problem: Dead Ends

#### Description
* The description of the PageRank algorithm is essentially complete. Minor problem with “dead ends”.
* Pages with no outlinks are “dead ends” for the random surfer -> Nowhere to go in the next step.
* Our algorithm so far is not well-defined when the number of successors k=0 (we would have 1/0!).

#### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323144817.png)

### Solution: Dealing with dead-ends

* Teleport
    * Follow random teleport links with probability 1.0 from dead-ends
    * Adjust matrix accordingly
* More efficient: prune and propagate
    * Preprocess the graph to eliminate dead-ends
    * Might require multiple passes
    * Compute page rank on reduced graph
    * Approximate values for deadends by propagating values from reduced graph






## Rage Rank

### Introduction

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323144450.png)


### Efficiency Issues

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323145112.png)

### Rearranging the equation

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323145156.png)

### Spares matrix

#### Sparse matrix formulation

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323145349.png)

#### Spares matrix coding

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323145417.png)



## Summary

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323145450.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210323231327.png)



