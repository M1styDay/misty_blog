---
title: Decision Trees：Content
author: "Misty"
tags: ["Decistion Trees","HKU"]
categories: ["Data Mining"]
date: 2021-04-10
---

# Decisision Trees

## Classification

### Definition

* Given a collection of records (training set)
    * Each record contains a set of attributes, one of the attributes is the Class.
* Find a model for Class attribute as a function of the values of other attributes
* Goal: previously unseen records should be assigned a Class as accurately as possible
    * A test set is used to determine the accuracy of the model. Usually, the given data set is divided into training and test sets, with training set used to build the model and test set used to validate it.
* Example
    * Predicting tumor cells as benign or malignant
    * Classifying credit card transactions as legitimate or fraudulent
    * Classifying secondary structures of protein as alpha-helix, beta-sheet, or random coil
    * Categorizing news stories as finance, weather, entertainment, sports, etc

#### Illustrating Classification Task    

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415145322.png)

### Facts about Classification

* Attributes might be discrete or continuous, however, the class must be discrete.
* If the class is continuous then regression. 
* Both descriptive and predictive.
* Most suited for binaries or nominal attributes, less effective for ordinal because ignores orders.

### Classification Techniques
* Decision Tree based Methods 
* Rule-based Methods
* Memory based reasoning Neural Networks
* Naïve Bayes and Bayesian Belief Networks 
* Support Vector Machines

## Decision Tree

### Example of a Decision Tree

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415150052.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415150113.png)

#### Decision Tree Classification Task

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415150149.png)

#### Apply Model to Test Data

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415150233.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415150524.png)

### Induction

* Many Algorithms
    * Hunt’s Algorithm (one of the earliest) 
    * CART
    * ID3, C4.5
    * SLIQ,SPRINT

### Hunt's Algorithm

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415152329.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415152306.png)

### General structure of tree induction

* Based on a greedy strategy:
    * Split the records based on an attribute test that optimizes certain criterion.
* We need to determine:
    * How to split the records:
        * How to split the attribute test condition?
        * How to determine the best split?
    * When to stop splitting

### - How to Specify Test Condition?

* Depends on attribute types:
    * Nominal(or categorical), have 2 or more categories, no order.(USA, Spain)
    * Ordinal, 2 or more categories but can ordered or ranked.(S,M,L,XL,XXL)
    * Continuous Ordinal.(temperature, salary)

* Depends on numver of ways to split
    * 2-way split
    * Multi-way split
  
#### Splitting Based on Nominal Attributes

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415154003.png)

#### Splitting Based on Ordinal Attributes

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415153819.png)

#### Splitting Based on Continuous Attributes

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415153928.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415153945.png)

### - How to determine the Best Split?

* Greedy approach:
    * Nodes with homogeneous Class distribution are preferred
* Need a measure of node impurity

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415154903.png)

*  Measures of Node Impurity
   * Gini Index
   * Entropy
   * MisClassification error

#### Gini Index

##### Measure of Impurity: Gini

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415155133.png)

##### Examples for computing Gini

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415155206.png)

##### Splitting Based on Gini

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415155241.png)

##### Binary Attributes: Computing Gini

* Splits into two partitions
* Effect of Weighing partitions:
    * Larger and Purer Partitions are sought for.

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415155727.png)

##### Find best Gini

* Categorical Attributes
    * For each distinct value, gather counts for each Class in the dataset
    * Use the count matrix to make decisions
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415160332.png)

* Continuous Attributes
    * Input: N records, attribute A 
    * Output: value v with min Gini for A
    * Naive:
        * let v1...vN be the values of A in the N records 
        * compute Gini for each of them, return the min 
        * requires O(N^2) operations, too expensive!
    * Better strategy
        * Sort the records non-decreasingly: v1<=v2,...,<=vN 
        * compute Gini index for each of them incrementally 
        * return the candidate with minimum Gini
        * Running time: O (N log N)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415160632.png)

#### Entropy

##### Alternative Splitting Criteria based on INFO

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415161051.png)

##### Examples for computing Entropy

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415161210.png)

##### Splitting Based on Information Theory

* Information Gain

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415161312.png)

* Gain Ratio

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415161343.png)

#### MisClassification error

##### Splitting Criteria based on Classification Error

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415161652.png)

##### Examples for Computing Error

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415161727.png)


#### Comparison among Splitting Criteria

* Binary Classification (2 Classes)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415162128.png)

* More about splitting criteria
    * Studies have shown that the choice of impurity measure has little effect on the final result
    * The strategy used to prune the tree (decrease its size and complexity) has a much bigger impact. More on this later...

### - When to Stop Splitting

* Stopping Criteria for Tree Induction
    * Stop expanding a node when all the records belong to the same Class
    * Stop expanding a node when all the records have similar attribute values (e.g. similar salaries)
    * Early termination (to be discussed later)

### Advantages of Decision Tree Based Classification

* Inexpensive to construct
* Extremely fast at Classifying unknown records
* Easy to interpret for small-sized trees
* Accuracy is comparable to other Classification techniques for many tasks

### Decision Tree Algorithm: C4.5
* #1 in the top 10 DM algorithm according to Springer LNCS (2008)*
* Simple depth-first construction. 
* Uses Information Gain
* Needs entire data to fit in memory. 
* Unsuitable for Large Datasets.

#### Example: Web-Robot detection

* Problem: Given a Web log, detect which accesses are made by humans and which ones by robots (e.g. crawlers)
* Input: a list of accesses to a Web site with the info:
    * IP address
    * average breadth of page visits
    * average depth of page visits
    * repeated access: how many times a same web page is accessed on average
    * number of images retrieved

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415165415.png)

* Results
    * Web robots tend to access as many pages as possible => visits are broad but shallow.
    * Web robots rarely download pictures.
    * Web robots are more likely to make repeated requests to a same Web page (Web pages retrieved by humans are often cached).




## Practical Issues of Classification

* Underfitting and Overfitting
* Missing Values
* Costs of Classification

### Underfitting and Overfitting 

#### Description

* Our main goal is to find a model that predicts the Class values on unseen records. We might have:
    * underfitting: the model did not learn the structure of the data and performs poorly on both the training set and the test set.
    * overfitting: the model becomes too specialized, describes well the training data but not unseen records. Good in training set but poor in the test set.
* Might have overfitting when decision tree is too large e.g. one record per leaf, which means tree size > dataset size.

#### Example of underfitting and overfitting

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415165818.png)


#### Results

* Results after building a decision tree on the previous dataset.
* Note that more sophisticated decision trees (larger # nodes) deliver good results in the training set but poor in the test set.

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415165946.png)


#### Overfitting 

* Overfitting due to Noise

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415170225.png)

* Overfitting due to insufficient examples
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415170235.png)

* notes on overfitting
    * Overfitting results in decision trees that are more complex than necessary
    * Training error no longer provides a good estimate of how well the tree will perform on previously unseen records
    * Need new ways for estimating errors

### Generalization and training errors

* Our main goal: the decision tree should generalize well to previously unseen data
* Two main errors
    * Training(aka resubstitution) errors: on training set
    * Generalization errors: errors on testing set

#### Occam's Razor(ORP)

* ORP: Given two models with similar generalization errors, one should prefer the simpler model over the more complex model
* For complex models, there is a greater chance that it was fitted accidentally by errors in data
* Therefore, one should include model complexity when evaluating a model

#### Estimating Generalization Errors

* Optimistic approach: ideal training test, generalization errors=training errors.
* Penalty for model complexity (not ideal training set, in line with ORP)
    * Pessimistic estimate:
        * Gener. error = training error + 0.5 x #of leaves.
        * E.g. Tree with 30 leaves,10 errors on training (1000 instances):
            * Gener. error = 10 + 30×0.5 = 25
            * Normalized gener. error = (10 + 30×0.5)/1000 = 2.5%
    * Minimum Description Length (MDL)

#### Minimum Description Length (MDL)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415171242.png)

### How to Address Overfitting

* pre-pruning (Early Stopping Rule)
    * Stop the algorithm before it becomes a fully-grown tree
    * Typical stopping conditions for a node:
        * Stop if all instances belong to the same Class
        * Stop if all the attribute values are the same
    * More restrictive conditions:
        * Stop if number of instances per node is less than some threshold
        * Stop if Class distribution of instances are independent of the available features (e.g., using χ 2 test to test variables indep.)
        * Stop if expanding the current node does not improve impurity measures (e.g., Gini or information gain).

* post-pruning(after building the tree)
    * Grow decision tree to its entirety
    * Trim the nodes of the decision tree in a bottom-up fashion
    * If generalization error improves after trimming, replace sub-tree by a leaf node.
    * Class label of leaf node is determined from majority Class of instances in the sub-tree
    * Better than pre-pruning but more operations.

#### Example of Post-Pruning

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415171536.png)


#### Example: Web-Robot detection

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415171637.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415171649.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415171705.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415171715.png)


## Decision Trees: Issues

### Data Fragmentation 

* Number of instances gets smaller as you traverse down the tree
* Number of instances at the leaf nodes could be too small to make any statistically significant decision

### Search Strategy 

* Finding an optimal decision tree is NP-hard
* The algorithm presented so far uses a greedy, top-down, recursive partitioning strategy to induce a reasonable solution
* Other strategies?
    * Bottom-up
    * Bi-directional

### Expressiveness 

* Decision tree works often well for discrete functions:
    * Not always:
        * Example: parity function:
            * Class = 1 if even number of Boolean attributes with truth value = True
            * Class = 0 otherwise
        * For accurate modeling, must have a complete tree (2^d nodes, where d is the number of boolean attributes)

* Not expressive enough for modeling continuous variables
    * Particularly when test condition involves only a single attribute at-a-time

* Decision Boundary
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415172541.png)

* Oblique Decision Trees
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415172620.png)

### Tree Replication

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210415172640.png)

## pseudocode

### Simple Decision Tree

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416111954.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416112019.png)

### Postpruning

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416112047.png)

## Random Forest

### The Random Forest Classifier

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416112150.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416112204.png)

### Main Idea

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416112228.png)