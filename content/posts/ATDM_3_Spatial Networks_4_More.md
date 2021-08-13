---
title: Spatial Networks：Supplement
author: "Misty"
tags: ["HKU","COMP 7801","Spatial Networks"]
categories: ["Advanced Topics in Data Management"]
date: 2021-02-07
---


## Shortest Path Search

### Dijkstra's algorithm 

* Dijkstra算法用来寻找图形中节点之间的最短路径。

* 在Dijkstra算法中，需要计算每一个节点距离起点的总移动代价。同时，还需要一个优先队列结构。对于所有待遍历的节点，放入优先队列中会按照代价进行排序。

* 在算法运行的过程中，每次都从优先队列中选出代价最小的作为下一个遍历的节点。直到到达终点为止。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210318155247.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210319000637.png)

### A* algorithm

* A*算法通过下面这个函数来计算每个节点的优先级:
    * f(n)=g(n)+h(n)
        * f(n)是节点n的综合优先级。当我们选择下一个要遍历的节点时，我们总会选取综合优先级最高（值最小）的节点。
        * g(n) 是节点n距离起点的代价。
        * h(n)是节点n距离终点的预计代价，这也就是A*算法的启发函数。
* A*算法在运算过程中，每次从优先队列中选取f(n)值最小（优先级最高）的节点作为下一个待遍历的节点。

* 另外，A*算法使用两个集合来表示待遍历的节点，与已经遍历过的节点，这通常称之为open_set和close_set。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210319001256.png)

* 在极端情况下，当启发函数h(n)始终为0，则将由g(n)决定节点的优先级，此时算法就退化成了Dijkstra算法。
* 如果h(n)始终小于等于节点n到终点的代价，则A*算法保证一定能够找到最短路径。但是当h(n)的值越小，算法将遍历越多的节点，也就导致算法越慢。
* 如果h(n)完全等于节点n到终点的代价，则A*算法将找到最佳路径，并且速度很快。可惜的是，并非所有场景下都能做到这一点。因为在没有达到终点之前，我们很难确切算出距离终点还有多远。
* 如果h(n)的值比节点n到终点的代价要大，则A*算法不能保证找到最短路径，不过此时会很快。
* 在另外一个极端情况下，如果h(n)相较于g(n)大很多，则此时只有h(n)产生效果，这也就变成了最佳优先搜索。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210319002151.png)

### Bi-directional search


![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210319003540.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210319003628.png)


## Spatial queries over spatial networks

* Data:
    * A (static) spatial network (e.g., city map)
    * A (dynamic) set of spatial objects
* Spatial queries based on network distance:
    * Selections. Ex: find gas stations within 10km driving distance from here
    * Nearest neighbor search. Ex: find k nearest restaurants from present position
    * Joins. Ex: find pairs of restaurants and hotels at most 100m from each other
* Methodology:
    * Store (and index) the spatial network
        * Graph component (indexes connectivity information)
        * Spatial component (indexes coordinates of nodes, edges, etc.)
    * Store (and index) the sets of spatial objects
        * Ex., one spatial relation for restaurants, one spatial relation for hotels, one relation for mobile users, etc.
    * Given a spatial location p, use spatial component of network to find the network edge containing p
    * Given a network edge, use network component to traverse neighboring edges
    * Given a neighboring edge, use spatial indexes to find objects on them


### Evaluation of Spatial Selections (1)

* Query: find all objects in spatial relation R, within network distance ε from location q
* Method:
    * Use spatial index of network (R-tree indexing network edges) to find edge n1,n2, which includes q
    * Use adjacency index of network (graph component) and apply Dijkstra’s algorithm to progressively retrieve edges that are within network distance ε from location q
    * For all these edges apply a spatial selection on the R-tree that indexes R to find the results

### Evaluation of Spatial Selections (2)

* Query: find all objects in spatial relation R, within network distance ε from location q
* Alternative method based on Euclidean bounds:
    * Assumption: Euclidean distance is a lower-bound of network distance:
        * dist(v,u) ≤ SPD(v,u), for any v,u
    * Use R-tree on R to find set S of objects such that for each o in S: dist(q,o) ≤ ε
    * For each o in S:
        * find where o is located in the network (use Network R-tree)
        * compute SPD(q,o) (e.g. use A*)
        * If SPD(q,o) ≤ ε then output o
  
### Evaluation of NN search (1)

* Query: find in spatial relation R the nearest object to a given location q
* Method:
    * Use spatial index of network (R-tree indexing network edges) to find edge n1,n2, which includes q
    * Use adjacency index of network (graph component) and apply Dijkstra’s algorithm to progressively retrieve edges in order of their distance to q
    * For each edge apply a spatial selection on the R-tree that indexes R to find any objects
    * Keep track of nearest object found so far; use its shortest path distance to terminate network browsing

### Evaluation of NN search (2)

* Query: find in spatial relation R the nearest object to a given location q
* Alternative method based on Euclidean bounds:
    * Assumption: Euclidean distance lower-bounds network distance:
        * dist(v,u) ≤ SPD(v,u), for any v,u

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210319182152.png)

### Spatial Join Queries

* Query: find pairs (r,s), such that r in relation R, s in relation S, and SPD(r,s)≤ε
* Methods:
    * For each r in R, do an ε-distance selection queries for objects in S (Index Nested Loops)
    * For each pair (r,s), such that Euclidean dist(r,s)≤ε compute SPD(r,s) and verify SPD(r,s)≤ε


## Advanced indexing techniques for spatial networks

### Hierarchical Path Materializatio

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210318212448.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210318212336.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210318212917.png)


### Compressing Materialized Paths
