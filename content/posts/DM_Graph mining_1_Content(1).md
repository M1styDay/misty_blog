---
title: Graph Mining：k-cores and Densest Subgraphs
author: "Misty"
tags: ["Graph Mining","HKU"]
categories: ["Data Mining"]
date: 2021-05-10
---

# k-cores and Densest Subgraphs

## Graph

* Graph Mining: finding dense regions ina graph (for community detectionm spam detection, event detection...)

### Definitions

* Undirected Graph: A graph G is a pair ($V_G$,$E_G$), where $V_G$ is a set of nodes, while $E_G$ is a set of edges (u,v) with u,v ∈ $V_G$.

* Other important definitions:
    * A graph H = ($V_H$,$E_H$) is a (induced) subgraph of G = ($V_G$,$E_G$) if the following two conditions hold: $V_H$ ⊆ $V_G$, moreover, (u,v) ∈ $E_H$ if and only if u,v ∈ H and (u,v) ∈ $E_G$.
    * $δ_G$(v) denotes the number of edges incident to v in G, while $δ_H$(v) denotes the number of edges incident to v in H.

## K-cores

### Definitions

* Given a graph G and k ≥ 0, a subgraph H of G is a k-core, if 
    * for every node v ∈ $V_H$, $δ_H$(v) ≥ k;
    * |$V_H$| is maximum;

* A k-core can be computed in linear time in |$E_G$| as follows.
    * While (at least one node has degree < k)

### k-core decomposition

* Note: a k-core might not be connected and is unique (possibly empty). 
* Note: If v belongs to a k−core then it belongs to a k'-core, k'< k.

* k-core decomposition(definition): A k−core decomposition specifies for each node v in G an integer $k_v$ such that v is in the $k_v$−core and $k_v$ is maximum.

* Note: A k−core decomposition can be computed in linear time: a k'-core is obtained by iteratively removing all nodes with degree < k', k'=1, ... n.

## Density of a graph

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210514020345.png)

#### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210514020703.png)

### Simple lemma

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515102929.png)

### Our main problem

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515103051.png)

* Facts: A global optimum can be computed in polynomial time. There is a linear-time algorithm that computes an approximation to the problem..

### Densest Subgraph Algorithm

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515103156.png)

#### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515103646.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515103702.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515103719.png)

### Approximation Guarantee

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515103805.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104039.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104054.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104108.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104359.png)

#### Proof

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104457.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104519.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104531.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104548.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104602.png)

### Running Time

The algo. can be implemented in linear time in the size of the input graph (i.e. the total number of edges and nodes in the graph).
* for each value δ in $[1, n]$ maintain a list of nodes with degree δ in the current graph.
* As nodes are removed from the graph, update the lists so that each node is placed in the correct list (depending on its current degree).

#### Exercise

which data structures to have a linear-time algorithm?

### Computing the Densest Subgraph

Three main techniques:
* maximum flow
* based on linear programming(LP)
* one recent technique based on convex programming

### Densest subgraph: variants

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210515104921.png)


### What about clique density?

* Finding a “large” subgraph with maximum edge density is very difficult!.
* However, in practice the following heuristic works very well. Modify the greedy algorithm as follows:
    * at each step remove the node with minimum degree until the graph becomes empty (similarly to greedy). Return a subgraph H (among all subgraphs obtained by greedy) maximizing the clique density and with size at least k.

 