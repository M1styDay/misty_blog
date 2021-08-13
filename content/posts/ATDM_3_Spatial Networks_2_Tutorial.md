---
title: Spatial Networks：Tutorial
author: "Misty"
tags: ["HKU","COMP 7801","Spatial Networks"]
categories: ["Advanced Topics in Data Management"]
date: 2021-02-09
---

## Dijkstra's algorithm review

## A* search algorithm review

## Nearest neighbor search exercise 

### Question
Consider a spatial network database, which includes a road network graph G and a set of points of interest P. The points in P can only be located on the vertices or edges of G. Each point of interest is with some labels (at least one), e.g., 'school', 'hotel', 'restaurant'. The points P are indexed by an R-tree $R_P$ based on location and by an inverted file (see the demo below) IP based on the labels. There is also an R-tree $R_E$ that spatially indexes the edges of G. Finally, there is a graph index for G, which enables us to quickly find all edges adjacent to any vertex in G. Consider a mobile user u on the spatial network who issues the query **find the nearest point of interest in P, in terms of shortest path distance, which contains the label 'vegetarian' and 'restaurant'**. Describe an efficient way to evaluate the query, using the given indexes, taking into consideration the following information:
1. Every edge of G includes at least one point in P which has the label 'restaurant'. However, only five points in P have the label 'vegetarian'.
2. The Euclidean distance between any two vertices of G is a lower bound of their shortest path distance.

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210318215341.png)

### Answer

* Find the nearest point of interest in P, in terms of shortest path distance, which contains the label 'vegetarian' and 'restaurant’.

* First perform a range query on $R_E$ to find the edge which includes u. Since 'vegetarian' is very rare, use the inverted file to find all points that include words 'vegetarian' and 'restaurant’. 

* Use R-tree $R_E$ again to find the locations of these candidate points on the spatial network.

* Perform an A* search from u to each candidate point and get the one with the lowest network distance to u. 
