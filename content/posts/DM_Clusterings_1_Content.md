---
title: Clusterings：Content
author: "Misty"
tags: ["Clusterings","HKU"]
categories: ["Data Mining"]
date: 2021-02-10
---

# Clusterings

## Background

### What is Cluster Analysis

* Finding groups of objects such that the objects in a group will be similar (or related) to one another and different from (or unrelated to) the objects in other groups
    * Intra-cluster distances are minimized
    * Inter-cluster distances are maximized
* Notion of a Cluster can be Ambiguous

### Applications of Cluster Analysis

* Understanding
    * Group related documents for browsing, group genes and proteins that hav similar functionality, or group stocks with similar price fluctuations
* Summarization
    * Reduce size of large data sets

### What is not Cluster Analysis
* Superviesd classification
    * Have class label information
* Simple segmentation
    * Dividing students into different registration groups alpgabetically, by last name
* Results of a query
    * Groupings are a result of an external specification
* Graph partitioning
    * Some mutual relevance and synergy, but areas are not identical

## Types of Clusterings

### Introduction

* **A clustering is a set of clusters**

* Important distinction between hierarchical and
partitional sets of clusters 

* Partitional Clustering
    * A division data objects into non-overlapping subsets (clusters)
    * such that each data object is in exactly one subset

* Hierarchical clustering
    * A set of nested clusters organized as a hierarchical tree

### Partitional Clustering

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309153046.png)

### Hieratchical Clustering

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309153134.png)

### Other Distinctions Between Sets of Clusters

* Exclusive versus non-exclusive clusters
    * In non-exclusive clusterings, points may belong to multiple
    * Can represent multiple classes or ‘border’ points 
* Fuzzy versus non-fuzzy
    * In fuzzy clustering, a point belongs to every cluster with some weight between 0 and 1
    * Weights must sum to 1
    * Probabilistic clustering has similar characteristics
* Partial versus complete
    * In some cases, we only want to cluster some of the data
* Heterogeneous versus homogeneous
    * Cluster of widely different sizes, shapes, and densities

## Types of Clusters

* Well-separated clusters 
* Center-based clusters 
* Contiguous clusters 
* Density-based clusters
* Property or Conceptual
* Described by an Objective Function

#### Well-separated clusters
A cluster is a set of points such that any point in a cluster is closer (or more similar) to every other point in the cluster than to any point not in the cluster.

#### Center-based clusters 
A cluster is a set of objects such that an object in a cluster is closer (more similar) to the “center” of a cluster, than to the center of any other cluster.

The center of a cluster is often a centroid, the average of all the points in the cluster, or a medoid, the most “representative” point of a cluster.

#### Contiguity-Based clusters
A cluster is a set of points such that a point in a cluster is closer (or more similar) to one or more other points in the cluster than to any point not in the cluster.

#### Density-Based clusters
A cluster is a dense region of points, which is separated by low-density regions, from other regions of high density.

Used when the clusters are irregular or intertwined, and when noise and outliers are present.

#### Conceptual clusters
**Shared Property or Conceptual Clusters**

Finds clusters that share some common property or represent a particular concept.

## Clustering Algorithms

### K-means

#### Description

Input: integer k>0, set S of points in the euclidean space 

Output: A (partitional) clustering of S

1. Select k points in S as the initial centroids
2. Repeat until the centroids do not change
    * Form k clusters by assigning points to the closest centroids 
    * For each cluster recompute its centroid

* Initial centroids are often chosen randomly.

* Centroids are often the mean of the points in the cluster.

* “Closeness” is measured by Euclidean distance, cosine similarity, correlation, etc.

#### Importance of Choosing Initial Centroids

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309161318.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309161356.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309161425.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309161454.png)

#### Problems with Initial Centroids (Adv. Topic)

Input: k clusters with the same size n/k, clusters are “sufficiently” spread apart.

Need to select 1 point per cluster!

* prob. the 2nd point is in a new cluster is
(k-1)/k, the 3rd point in a new cluster is (k-2)/k...

* Prob. to select exactly one point per cluster =
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309161823.png)

  * For example, if K = 9, then probability = 9!/$9^9$

#### Evaluating K-means Clusterings
* Most common measure is Sum of Squared Error (SSE)
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309162226.png)

  * where x is a point in cluster $C_i$ and $m_i$ is the centroid of cluster $C_i$

* Given two clusterings, we can choose the one with smallest error

* Decreasing K might decrease SSE. However, good clusterings with small K might have a lower SSE than poor clusterings with higher K.

#### K-Means Always Terminates

* Theorem. K-means with Euclidean distance as distance always terminates.
* Proof follows from the following lemmas:
    * Lemma 1. The point y that minimizes the SSE in a cluster C is the mean of all points in C.
    * Lemma 2. SSE strictly decreases.
    * Lemma 3. The total number of possible clusterings is finite (< n^k).

* Lemma 1
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309162741.png)


* Lemma 2
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309163125.png)

* Theorem. K-means always terminates

The proof follows from Lemma 2 and Lemma 3. We cannot obtain the same clustering more than once, otherwise we get the same SSE value.

Observe that we need both Lemma 2 and 3.

#### Solutions to Initial Centroids Problem

* Multiple runs (helps but low success probability)
* Sample and use hierarchical clustering to determine initial centroids
* Select more than k initial centroids and then select among these initial centroids
* Postprocessing 
* K-Means++

#### Handling Empty Clusters([Exercise]())
* Basic K-means algorithm can yield less than k clusters (so called empty clusters)
* Serveral strategies:
    * Pick the points that contributes most to SSE and move them to empty cluster.
    * Pick the points from the cluster with the highest SSE
    * If there are several empty clusters, the above can be repeated several times.

#### Updating Centers Incrementally
* In the basic K-means algorithm, centroids are updated after all points are assigned to a centroid.
* An alternative is to update the centroids after each assignment (incremental approach).
* More precisely, let $C_1$,$C_2$,...,$C_k$ be the current clusters. Re-assign all points one by one to the best cluster. Let p in $C_i$ be the current point and suppose we re-assign it to $C_j$. Then, after that, recompute the centroid of $C_i$ and $C_j$.
    * Never get an empty cluster
    * Introduces an order dependency
    * More expensive

#### Pre-processing and Post-processing
* Pre-processing
    * Normalize the data
    * Eliminate outliers
* Post-processing
    * Eliminate small clusters that may represent outliers
    * Split "loose" clusters, i.e., clusters with relatively high SSE
    * Merge clusters that are "close" and that have relatively low SSE

#### Limitations of K-means
* K-means has problems when clusters are of differing
    * Sizes
    * Densities
    * Non-globular shapes
* K-means has problems when the data contains outliers

#### Overcoming K-means Limitations

One solution is to use many clusters.

Find parts of clusters, but need to put together.

* Sizes
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309182850.png)

* Densities
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309182929.png)

* Non-globular shapes
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309183054.png)

### Hieratchical clustering

#### Description

* Produces a set of nested clusters organized as a hierarchical tree
* Can be visualized as a dendrogram
    * A tree like diagram that records the sequences of merges or splits

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309183228.png)

#### Strengths of Hierarchical Clustering

* Do not have to assume any particular number of clusters
    * Any desired number of clusters can be obtained by "cutting" the dendogram at the proper level
* They may correspond to meaningful taxonomies
    * Example in biological sciences (e.g., animal kingdom, phylogeny reconstruction, ...)

#### Two main types of hierarchical clustering

* Agglomerative
    * Start with the points as individual clusters
    * At each step, merge the closest pair of clusters until only one cluster (or k clusters) left
* Divisive
    * Start with one, all-inclusive cluster
    * At each step, split a cluster until each cluster contains a point (or there are k clusters)

* Traditional hierarchical algorithms use a similarity or distance matrix
    * Merge or split one cluster at a time

#### Agglomerative Clustering Algorithm

* Most popular hierarchical clustering technique
* Algorithm:
  * Let each data point be a cluster
  * Compute the distance matrix n x n 
  * Repeat
    * Merge the two closest clusters
    * Update distance matrix 
  * Until only a single cluster remains

#### Example of Agglomerative Clustering Algorithm
* Starting Situation

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309184040.png)

* Intermediate Situation

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309184113.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309184153.png)

* After Merging

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309184317.png)

* How to Define Inter-Cluster Similarity

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309184436.png)

#### Hierarchical Clustering: Problems and Limitations

* Once a decision is made to combine two clusters, it cannot be undone
* No objective function is directly minimized
* Different schemes have problems with one or more of the following:
    * Sensitivity to noise and outliers
    * Difficulty handling different sized clusters and convex shapes
    * Breaking large clusters

## Cluster Validity

### Introduction
* For cluster analysis, the analogous question is how to evaluate the “goodness” of the resulting clusters?
* But “clusters are in the eye of the beholder”!
* Then why do we want to evaluate them? 
    * To avoid finding patterns in noise
    * To compare clustering algorithms
    * To compare two sets of clusters
    * To compare two clusters

### Measures of Cluster Validity
* Numerical measures that are applied to judge various aspects of cluster validity, are classified into the following three types.

    * Internal Index: Used to measure the goodness of a clustering structure without respect to external information. 
        * Sum of Squared Error (SSE)
    * External Index: Used to measure the extent to which cluster labels match externally supplied class labels.
        * Entropy
    * Relative Index: To compare two different clusterings or clusters. 
        * An external or internal index is used for this function, e.g., SSE or entropy

* Sometimes these are referred to as criteria instead of indices

### Internal Measures: SSE
* Clusters in more complicated figures aren’t well separated
* Internal Index: Used to measure the goodness of a clustering structure without respect to external information
    * SSE
* SSE is good for comparing two clusterings or two clusters (average SSE).
* Can also be used to estimate the number of clusters

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309185507.png)

### External Measures of Cluster Validity: Entropy

#### Definition

* Given a discrete random variable X with possible value {1,..,n} entropy is defined as

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309185711.png)

* Entropy measure how uncertain is an event, the larger the entropy the more uncertain is the event

#### Intuition

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309185818.png)

#### Example

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309190157.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309190558.png)

### Final Comment on Cluster Validity
“The validation of clustering structures is the most difficult and frustrating part of cluster analysis. Without a strong effort in this direction, cluster analysis will remain a black art accessible only to those true believers who have experience and great courage.”

Algorithms for Clustering Data, Jain and Dubes

## k-means++

### Algorithm

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309191210.png)

### Introduction

* Initialize the centroids as in Algorithm 1
* Run K-menas algorithm to improve the clustering

### Theorem

* Let C_KM++ be the clustering produced by the K-means++ algorithm
* let C_opt be an optimal clustering (with minimum SSE among all possible clusterings)
* Then, SSE(C_KM++) <= 8*(ln k + 2)*SSE(C_opt), on expectation (average).

### [Exercise]()

* give an example where k-means computes an approximation "worse" than k-means++.

### K-means vs. K-means++

* K-means
    * no guarantees on the quality of the solution
    * it always terminates
    * running time could be exponential but it is OK in practice
* K-means++
    * it always terminates
    * O(log k)-approximation on the quality of the solution. 
    * In practice the advantage is noticeable for large k