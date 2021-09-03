---
title: Lecture 2：Exploring and Visualizing Data
author: "Misty"
tags: ["HKU","ICOM 6044","Data science for business"]
categories: ["Data science for business"]
date: 2021-06-10
---

# Lecture 2：Exploring and Visualizing Data

* This lecture focuses on how we can use descriptive statistics and exploratory analysis to understand datasets. A primary goal of data visualization is to help identify patterns in data and be able to communicate these patterns succinctly to an analyst.  Often our goal is to find patterns in large datasets, to help reduce the size of the dataset we introduce cluster analysis as a data mining technique for grouping objects into similar subsets or clusters.  It is one of the most common data mining techniques and used in many fields, such as machine learning, pattern recognition, image analysis and bioinformatics.

* Required Readings: 
    * Taddy, Business Data Science, Chapter 7.
    * “Cluster Analysis for Marketing Segmentation”, UVA-M-0748.
  
* Optional Readings: 
    * Provost and Fawcett, Data Science for Business, Chapter 6.
    * James et al, An Introduction to Statistical Learning, Chapter 10.3.

* Session:
    * Introduction to Cluster Analysis
    * Example of k-Means Clustering using Iris Data 
    * Introduce Ford Ka Case


## Part 1: Cluster Analysis

* Review from Lecture 1 and Questions
* Cluster Introduction
* k-Means Algorithm
* Example of k-Means clustering using Lending Club
* Video: Example of k-Means clustering using Iris Data

### Review from Lecture 1 and Questions

* Data Science for Business
* Course Objectives
* Zoom Etiquette
* Questions
* Announcements

### Motivation and Types of Cluster Analysis

#### Clustering 

* “Clustering is the most frequent data mining task.” Kdnuggets News, 11 June 2001
* An unsupervised learning method that organizes and simplifies the structure for large, complex data sets
* Example: Find a “natural” grouping of data given unlabeled data with two variables (dimensions)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615233649.png)

#### Types of Clustering Methods

* Partitioning
    * Distinct, non-overlapping groups
    * Works using iterative assignment (and re-assignment) of objects
* Hierarchical
    * Tree of objects; Dendrogram
    * Works using agglomerative or divisive approaches
* Other clustering techniques
    * Fuzzy or soft clustering; Overlapping
    * Probablistic or mixtures, as with topic models like Latent Dirichlet Allocation (LDA) or Gaussian Mixture Models

#### Using Cluster Analysis to Understand

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615233901.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615233934.png)


#### Using Cluster Analysis to Summarize Psychographic Sementation for Weight-Loss

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615234240.png)

#### Example: PersonicX.com Lifestyle Segmentaion

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615234356.png)


### Distance Based Approaches

#### Use of "Closest" data points

* Amazon.com: “People like you also liked ...”
* House appraisals: “The three most similar houses to your are ...”
* Lots of informal arguments: “I was in a similar situation three years ago and I ...”

#### Clustering works by measuring distance between records

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615234718.png)

#### Distance metrics implicitly reflect judgment about importance

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615235430.png)

#### Distances

* Range (or continuous): easy enough, can just take (absolute value of) differences
* Ordinal: a little harder, but not unreasonable to take number of categories different
* Nominal: 1 if different, 0 if the same
    * Previous example: |704-619| + 2+1+1 = 89
    * Not best distance metric: lots of weight on GMAT

#### Fixing Weight issue

* Normalize data, or
* Assign weights to each field: say (1/100,1,2,3) to give value
    * Previous example: |704-619|/100 + 2+2*1+3*1 = 7.85
* How to get weights? No obvious way, but distance function is critical to these approaches


### Combinatorial Problem of Finding Clustering Solutions

#### Illustrating our true grouping

* Suppose we have a dataset with 2 variables and 15 observations
* We know that it is made up of 3 groups each with 5 observations
* Our true grouping of the data shows three distinct groups
 
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615235922.png)

#### The goal of cluster analysis is to reconstruct the true grouping but without knowing the group

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210615235959.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616000301.png)


#### How do we decide which is the best "solution"

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616000610.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616000705.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616000741.png)


#### K-Means decomposes variation into between (explained) and within (unexplained)

* Find k groupings (or clusters) of n observations that maximize the distances between the groups (or minimize distances within groups)
    * Motivation “similar within, different between
    * SStotal = SSwithin + SSbetween
* Define centroid of a group of observations to be the mean or average of each of the field values for those points (convert discrete and ranks to numeric values)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616000924.png)

#### K-Means attempts to find the best solution by iterating upon an initial solution

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616001108.png)



### K-Means Algorithm

* We cannot evaluate every potential solution, so we use an algorithm that avoids computing every permutation and iterates to find a “good” one.

#### K-means Clustering Algorithm

* Partitional clustering approach
* Each cluster is associated with a centroid (center point)
* Each point is assigned to the cluster with the closest centroid 
* Number of clusters, K, must be specified
* The basic algorithm is very simple

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616001355.png)

#### K-Means Example (Geometric Perspective)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616001550.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616001603.png)


#### K-means Clustering - Detail

* Initial centroids are often chosen randomly.
    * Clusters produced vary from one run to another.
* The centroid is the mean of the points in the cluster
* ‘Closeness’ is measured by Euclidean distance (others are cosine similarity, correlation, etc.)
* K-means will converge for common similarity measures mentioned above.
* Most of the convergence happens in the first few iterations.
    * Often the stopping condition is changed to ‘Until relatively few points change clusters’
* Complexity is O( n * K * I * d )
    * n = number of points
    * K = number of clusters
    * I = number of iterations
    * d = number of attributes


#### Cluster Profiling: What do my clusters mean?

* Clustering optimizes a statistical criterion, but your goal is to use the clusters to make better sense of your data. To interpret the meaning of the clusters try the following:
    *  Examine the cluster centroids (averages) and compare them to one another (e.g., Heavy vs. Light users) with tables and plots
    *  Select individual(s) close to the cluster centroid to give a prototypical example, to understand what observations belong (e.g., high income customer might suggest “affluent” cluster)
    *  Identify names or labels for each cluster can relate to behaviors or observables (e.g., wealthy retired become “Sitting Pretty”, rural customers “Country Ways”, single consumers renting in the city “Urban Tenants”)
    *  Compare with known taxonomies or groupings to validate the meaning of your clusters
 

 ### Cluster Validity

 #### Cluster Validity

 * For supervised classification we have a variety of measures to evaluate how good our model is
     * Accuracy, precision, recall
 * For cluster analysis, the analogous question is how to evaluate the “goodness” of the resulting clusters?
 * But "clusters are in the eye of the beholder"!
 * Then why do we want to evaluate them?
    * To avoid finding patterns in noise
    * To compare clustering algorithms
    * To compare two sets of clusters
    * To compare two clusters


#### Internal Measures: Cohesion and Separation

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616002753.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616003154.png)


#### Evaluating K-means Clusters

* Most common measure is Sum of Squared Error (SSE) or Within Sum of Squares (WSS)
    * For each point, the error is the distance to the nearest cluster
    * To get SSE, we square these errors and sum them.
    * ![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616004443.png)
    * x is a data point in cluster Ci and mi is the representative point for cluster Ci 
        * can show that mi corresponds to the center (mean) of the cluster
    * Given two clusters, we can choose the one with the smallest error
    * One easy way to reduce SSE is to increase K, the number of clusters
        * A good clustering with smaller K can have a lower SSE than a poor clustering with higher K
 

#### Using Scree Plots to determine k

* Clusters in more complicated figures aren’t well separated
* Internal Index: Used to measure the goodness of a clustering structure without respect to external information like SSE
* SSE is good for comparing two clusterings or two clusters (average SSE). 
* Can also be used to estimate the number of clusters

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616005108.png)


#### Framework for Cluster Validity

* Our goal is to find a cluster solution that is “Similar within, different between” 
* Need a framework to interpret any measure.
    * For example, if our measure of evaluation has the value, 10, is that good, fair, or poor? 
* Statistics provide a framework for cluster validity
    * The more “atypical” a clustering result is, the more likely it represents valid structure in the data
    * Can compare the values of an index that result from random data or clusterings to those of a clustering result.
        * If the value of the index is unlikely, then the cluster results are valid
    * These approaches are more complicated and harder to understand.
* For comparing the results of two different sets of cluster analyses, a framework is less necessary. 
    * However, there is the question of whether the difference between two index values is significant


### Lending Club In-Class Exercise

Customer Segmentation using k-Means

#### Introduction to Lending Club

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616005556.png)

#### Two-sided Market

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616005837.png)

#### Lending Club Dataset

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616005924.png)

#### In-Class Exercise Cluster Analysis of Lending Club

* Review the list of variables and identify what potential relationships you expect to find with loan default
* Download the files: lendingclub_kmeans.R and loans-kpi.csv
* Run the “@setup” and “@input”. Step through the “@exploratory analysis” section of the script and carefully consider the output.
* What did you learn from descriptive analysis?
* Run the “@kmeans” and “@scree” and “@cluster” to complete the cluster analysis. Make sure you choose the best k.
* What is the meaning of the cluster analysis?

#### Understanding Boxplots

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616012202.png)

#### Parallel Lines Visualization

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616012226.png)

#### Scatterplot Matrix

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616012250.png)

#### K-Means Cluster for Lending Club Data

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616012318.png)

#### Understanding k-means output

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616012342.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616012410.png)

#### Choosing the Number of Clusters Using a Scree Plot

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616012437.png)

#### How do we interpret our clusters

* Focus on the Cluster Centroids or Centers since this is our summary of the cluster or gives us a “prototype” of the cluster
    * Look at the table
    * Also try a parallels lines plot of the Cluster Centroids
* Often we label our clusters so that we do not refer to them as “cluster A”, “cluster B”, ... but instead something more meaningful like “big spenders”, ...


#### Interpreting our Clusters (Use the Parallel Lines Plot to Compare Centroids Graphically)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210616012510.png)


### Conclusions 

#### Summary on Clustering 

* Undirected data mining approach: no output field.
* Wish to group together “similar” records (as given by distance function)
* Used as end in itself (determining market segments) or as part of datamining process (apply different neural network or decision tree to each cluster)
* Advantages
    * Easy to apply, depends only on distance function
    * Leads to interesting insights
* Disadvantages
    * Relies on distance function: bad function, bad results
    * Difficult to find good clusters: lots of algorithms, no clear winner
    * Difficult to interpret the results



## Part 2: k-Means Clustering with Iris Data

* Iris Dataset
* R script to complete k-Means Analysis 
    * Setup
    * Syntax help
    * Visualization
    * k-Means
    * Scree Plots


### Processing

* 详情见课件


### Summary of Cluster Analysis with R

* Goal
    * Take a large datasets (many rows) and organize into groups (or assign each row into a cluster) ◦ Helpful in reducing the dimension of a dataset and finding patterns
* Input
    * Matrix of numeric values (rows are observations, columns are variables)
* Output
    * Vector of assignments (each element corresponds to the cluster of a row) ◦ Matrix of cluster centroids (averages of the variables within a cluster)
* Interpretation
    * Comparing the differences in the means of the clusters using cluster centroids
    * Visualize differences in the clusters by looking at tables/plots of cluster centroids ◦ Use the clusters as a way of reducing the dimension of the data for other analyses



## Part 3: Introduction to Ford Ka Case

* 详情见课件