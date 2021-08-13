---
title: Lecture 3：Market Segmentation of Consumers
author: "Misty"
tags: ["HKU","ICOM 6044","Data science for business"]
categories: ["Data science for business"]
date: 2021-06-17
---


# Lecture 3: Market Segmentation of Consumers

* Marketing research focuses on understanding a customer’s needs--ideally at an individual level.  However, it is often difficult to react to each customer individually.  An alternative is to identify groups of customers that are similar to one another.  In this class we consider how cluster analysis can be used to segment customers based upon their demographic characteristics and purchase behavior.  The goal of our segmentation scheme is to better target customers.  Specifically, we consider a case study for Ford in which they conduct a cluster analysis to segment their market.

* Required Readings:
    * “Ford Ka: The Marketing Research Problem (A)”, INSEAD Case #503-082-1BW.
    * “Ford Ka: The Market Research Problem (B)”, INSEAD Case #503-082-1BW.

* Session:
    * Discussion of Ford Ka Case
    * Limitations of k-Means

## Part 1: Discussion of Ford Ka Case

* Ford’s Objectives
* Segmentation based upon psychographics versus demographics
* How do we use our cluster analysis to drive a segmentation/targeting/positioning strategy?

### Ford Ka Case

#### Questions


1. How did Ford (and car manufacturers in general) segment the overall car market? What was the typical small car marketing strategy in the past?
2. Why did Ford develop the Ford Ka? Is the existing segmentation approach still applicable?
3. Implement a segmentation scheme using K-Means Clustering. Briefly explain your clustering solution.
4. Which cluster from question #3 would you recommend be the target for the Ford Ka? What potential implementation problems do you expect from your recommendations? How can you overcome them?



#### What data do we have?

* Demographic Data
    * Gender,Age,MaritalStatus,NumberofChildren,Firsttimepurchase,AgeCategory,ChildrenCategory,IncomeCategory
* Psychographic Data
    * 62attitudinalquestions(1=‘stronglydisagree’to7=‘stronglyagree’)
    * Q1:“I want a car that is trendy”
    * Q2:“I am fashion conscious”
    * Q3:“I do not have time to worry about car maintenance” 
    * Q4:“Basic transportation is all I need”
* Perceptual Data (we do not use)
    * On a scale of 1=‘very similar’ to 9=‘very different’ compared each pair of cars
    * Analyzed using another technique known as Multidimensional Scaling(MDS)

##### Materials

* Segments are constructed on the basis of customers’ (a) demographic characteristics, (b) psychographics, (c) desired benefits from products/services, and (d) past-purchase and product-use behaviors. These days most firms possess rich information about customers’ actual purchase behavior, geo-demographic, and psychographic characteristics. In cases where firms do not have access to detailed information about each customer, information from surveys of a representative sample of the customers can be used as the basis for segmentation.


#### The Data Mining Process

1. Statetheproblem
2. Collectthedata
3. Preprocessthedata
4. Estimatethemodel(minethedata)
5. Interpretthemodelanddrawconclusions


#### Steps for Preparing Data

1. Create data table
2. Characterize variables 
3. Clean data
4. Remove variables
5. Transform variables 
6. Segment table


### Potential Segmentation Solutions







## Part 2: Limitations of k-Means 

* Scaling data
* Initial starting points
* Limitations with cluster “shapes”