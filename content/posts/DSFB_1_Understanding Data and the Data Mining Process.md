---
title: Lecture 1：Understanding Data and the Data Mining Process
author: "Misty"
tags: ["HKU","ICOM 6044","Data science for business"]
categories: ["Data science for business"]
date: 2021-05-23
---

# Lecture 1: Understanding Data and the Data Mining Process

* In this class we discuss the role of data mining for electronic commerce.  The wealth of information and methodologies does not necessarily lead managers to make better decisions unless they are able to transform the data into a useable form.  In this lecture we consider how data mining can help turn data into information that managers.  We also consider examples where data mining has been used successfully in business and electronic commerce.  Finally, we introduce different types of data and how statistics and visual techniques can be used to understand the data.

* Required Readings:
    * Sahay (2018), “Data Mining: Tools and Applications in Predictive Analytics”, Harvard Business Case BEP506.
    * Taddy, Business Data Science, Chapter 1.
    * Venables et al, An Introduction to R, available online at https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf

* Optional Readings:
    * Provost and Fawcett, Data Science for Business, Chapters 1 and 2.
    * Stanton, Introduction to Data Science, Chapters 1 through 9.
    * James et al, An Introduction to Statistical Learning, Chapter 1.

* Session:
    * Course Information
    * What is Data Science? Overview of Data Mining and Limitations
    * Primer on R


## Part 1: Class Overview

* Required Textbook

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608213326.png)

* Optional, Supplemental Book

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608213410.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608213439.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608213532.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608213554.png)


## Part 2: The promise and limiations of data science for business

* Lecture Outline
    * What is Data Science?
    * Promise of Big Data
    * Limitations of Data Science

### What is Data science

#### Extracting knowledge from data to make better decisions in business.
* Data can be structured (transactions) or unstructured (emails, videos, photos, social media, ...).
* Data are facts, while knowledge is generalizable.
* The extraction process uses data mining techniques.
* Data scientists need to have both technical skills for data mining, but domain knowledge to know how to structure an analysis to have an impact.
* Notice that Data Science is an empirical science. It is based upon experimentation or observation (evidence), as opposed to case studies or theoretical research methods.

#### Hacking Skills / Math & Statistics Knowledge / Substantive Expertise  
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608230038.png)

#### Empiricism versus Rationalism
* Empiricists believe that we learn about our world through previous experience. Rationalists believe reason is the basis for understanding anything.   
    * Strength of empiricism: Objectivity, measurability, replicability, ...
    * Weaknesses of empiricism: Inefficient, Potential for bias in data due to (bad) prior research or incorrect collection, Lack of information (e.g., predict future), ...
* Example: Why is our customer loyalty dropping?
    * Empiricists collect data, rationalists argue we know that loyalty is driven by consumer heuristic to “keep doing it if it works”

#### Data science is a proces
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608230536.png)


![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608230605.png)


#### Connection with Other Related Areas
* Machine Learning 
* Artificial Intelligence 
* Optimization
* Operations Research 
* Exploratory Data Analysis 
* Visualization
* Statistical Modeling
* Statistical Computing 
* Hadoop/MapReduce/GraphLab/Parallel Computing
 
#### What are the most important qualities that recruiters want in a data scientist?
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608231205.png)


### The Promise of Big Data

#### What is Big Data

* Four basic components:
    * Massive datasets
    * Unstructured data
    * Collected as a by-product from transactions (not for decision making) 
    * Populations not samples
* Related to Business Analytics, Data Analysis, Data Mining, Data Science, Machine Learning, Statistics


#### Big Data Example

* Billion Prices Project

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608231405.png)

* Google Correlates

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608231452.png)

* Tweeting about Unemployment

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608231539.png)

* Predicting TV Ratings

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608233940.png)

* Understanding Market Structure

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608234021.png)

* Making Better Priceing Decisions

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210608234111.png)

#### Advantages of Big Data

* Can detect patterns by leveraging these qualities: ◦ Massive
    * Immediate and timely
    * Predictive
    * Free (or inexpensive)

### Limitations of Data Science

#### Why companies fail to leverage Big Data

* Some illustrations
    * Assessing Model Uncertainty in Financial Risk Management
    * Retail Price Optimization using Business Rules
    * Predicting Flu Trends
    * Problems with Big Data
    * Mangers and culture

* Summary
    * Big Data has a huge potential to shape our lives through changes in business, government, and science, or society in general
        * It is a by-product of our electronic lives and generally the reason it is collected has nothing to do with analysis or learning
        * The goal of data science is to tap into this potential of data (big or small) to make decisions
    * But remember analytical approaches fail because
        * Bad/poor/biased data
        * Bad/poor/biased models
        * Bad/poor/biased managers who interface with the models
 
#### Limitations of Big Data and Data Science

* The promise of Big Data is that we can solve problems faster, cheaper and better.
* The problem is that Big Data is still just data, and we need to know its biases
    * Historical data may not be representative of future data
    * Participants in social media data may not be representative of society 
    * The collection and use of “Big Data” changes through time
* Knowledge (managerial or theoretical) is still useful
    * The data we observe is influenced by our past decisions, which is a function of our “models”, need to consider this feedback relationship
 
#### Disadvantages of Data Based Approaches

* It may not be representative
     * Who writes reviews? Really excited customers and really disappointed ones
* Data quality may be poor
    * Consumers generate Big Data for themselves not for data miners
* Privacy and confidentiality issues 
    * How can we protect consumers?
* Difficult to assess accuracy and uncertainty
* The past may not be representative of the future


## Part 3: Primer on R

* 详情见课件