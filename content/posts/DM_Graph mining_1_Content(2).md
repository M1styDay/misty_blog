---
title: Graph Mining：Community Detection
author: "Misty"
tags: ["Graph Mining","HKU"]
categories: ["Data Mining"]
date: 2021-05-09
---

# Community Detection

## Community Detection

### Introduction

* Community detection is the problem of finding groups of entities in a network, so as to reflect the structure of the network and other meaningful properties of the underlying system.
* Examples of communities are: computer scientists, users in Facebook sharing similar interests, blogs dealing with the same topic, group of dolphins interacting between each other, etc.
* Community detection finds application in social science, advertising, and it is a cool problem!

#### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515110153.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515110212.png)

### Community Detection as a Graph Problem

* The work of $[14]$ sparked in 2002 a wave of interest, although this area has its roots in graph partitioning dating back to the 1970s (METIS $[15]$).
* It can be formalized as a graph problem, where nodes represent users and edges some kind of links between them (e.g. friendship, interaction etc.).
* Given a graph G = (V,E), we wish to find subsets of nodes C1,...,Ck corresponding to communities. The problem is called non-overlapping or overlapping community detection depending on whether the $C_i$’s are disjoint or not. We might or might not seek to find a partition of V.

## Metrics for Community Detection

We can compile the following list of metrics (as done in $[2]$) so as to devise an effective community detection algorithm:
* separability;
* density; 
* cohesiveness; 
* clustering coefficient.

### Separability

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515134902.png)

### Density

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515135157.png)

### Clustering Coefficient

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515135327.png)

### Modularity

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515135729.png)

* That is the fraction of edges within a same community minus the expected number of edges within a same community in a random graph having the same degree distribution of G (null model).

## Random Graphs with the Same Degree Distribution

* Given a graph G = (V , E ) a random multigraph H maintaining for each node its degree in G is produced as follows: each edge is divided into two halves (stubs) each of them being assigned uniformly at random to any stub in the graph.

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515140210.png)

* Each stub is assigned uniformly at random to any of the 2m stubs available. In H, we might have self loops, multiple edges per pair of nodes, multiple self loops but the same node degrees of G.

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515140242.png)


## Facts about Modularity

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515140428.png)

#### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515140529.png)


### Modularity: Issues

* Merging “well-separated cliques” (that should be identified as two different communities) might result in larger modularity. 
* Resolution limit: “small” communities might be missed.

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515140906.png)

### Optimizing Modularity

* Optimizing most of the metrics we considered is NP-Hard. The NP-hardness of modularity optimization has been proved in $[16]$.
* Some heuristics have been developed to maximize modularity.
* One of the first heuristic is the Louvain Algorithm

## The Louvain Algorithm (one of the variants)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515141140.png)

### Louvain: Running Time

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515141318.png)

### Facts about Louvain

* Positive facts:
    * Successfully applied in a variety of application domains.
    * It produces good results, despite the limitations of modularity. 
    * Simple, efficient in practice, code in C available.
    * Generalization to weighted graphs and hierarchical communities. 
    * Some guarantees on the quality of the solution.
* Limitations:
    * Nodes are partitioned, however, often communities do overlap. 
    * suffers from modularity issues.






## Community Detection from Seed Sets

* We are interested in accessing or studying a group of people in a social network (algorithmists, data scientists, hikers, . . . ) but we know only a few users in the group. We wish to expand this group.
* Problem: Given a graph G, a set S of seed nodes, an integer k > 0, find k additional nodes belonging to the “same community” of S.

#### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515142243.png)

### Algorithms

* Several algorithms based on:
    * local modularity (different than the one we saw): add the node increasing modularity the most.
    * conductance: add the node decreasing conductance the most. 
    * PageRank . . .

### PageRank with Restart

#### Matrix
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515150024.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515142431.png)

#### Algorithm

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515142508.png)


### Experimental Evaluation

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515150058.png)

#### Setting

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515150120.png)

#### Results

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515150145.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515150204.png)

#### Findings

* Findings:
    * PageRank with restart is simple and efficient and performs best. 
    * The PR algorithm needs to be iterated for 2-3 steps.
* Limitations:
    * how large k must be?
    * good also with other choices of β, set of communities, datasets?



### Reference

[Modularity的计算方法——社团检测中模块度计算公式详解](http://www.yalewoo.com/modularity_community_detection.html)
[社区发现算法之——Louvain](https://blog.csdn.net/qq_40438165/article/details/83374304)
[Louvain 社团发现算法学习](https://blog.csdn.net/qq547276542/article/details/70175157)