---
title: Curriculum Overview
author: "Misty"
tags: ["HKU","ICOM 6044","Data science for business"]
categories: ["Data science for business"]
date: 2021-05-22
---



## Lecture 1: Understanding Data and the Data Mining Process

### 1.1 Course Overview - 1

### 1.2 The promise and limitations of data science for business - 25

#### What is Data Science? 

* What is Data Science?
* Empiricism versus Rationalism
* Data science is a process
* Relationship of Data Mining to  Data Science/ Decision Making/ Big Data/ Business Analytics
* Connection with Other Related Areas
* What are the most important qualities that recruiters want in a data scientist?

#### Promise of Big Data 
* What is Big Data?
* Some Examples
* Advantages of Big Data

#### Limitations of Data Science
* Why companies fail to leverage Big Data
    * Assessing Model Uncertainty in Financial Risk Management
    * Retail Price Optimization using Business Rules
    * Predicting Flu Trends
    * Problems with Big Data
    * Mangers and culture
    * Summary
* Limitations of Big Data and Data Science
* Disadvantages of Data Based Approaches


### 1.3 Primer on R - 77



## Lecture 2: Exploring and Visualizing Data

### 2.1 Introduction to Cluster Analysis - 158

#### Cluster Introduction
* Clustering
* Types of Clustering Methods
* Distance Based Approaches
* Combinatorial Problem of Finding Clustering Solutions

#### k-Means Algorithm
* K-means Clustering Algorithm
* Cluster Profiling

#### Cluster Validity
* Cluster Validity
* Internal Measures: Cohesion and Separation
* Evaluating K-means Clusters[计算]
* Using Scree Plots to determine k
* Framework for Cluster Validity

#### Example of k-Means clustering using Lending Club 

#### Summary on Clustering
* Avantages and Disadvantages

### 2.2 k-Means Clustering with Iris Data - 125

### 2.3 An Example of k-Means using Iris Data - 241

### 2.4 Introduce Ford Ka Case -233

* The steps
    * Input Data
    * Describe and manipulate the data
    * Plot Data
    * Perform k-Means
    * Interpret and evaluate Clusters



## Lecture 3: Market Segmentation of Consumers

### 3.1 Discussion of Ford Ka Case and Clustering - 260
* Ford’s Objectives
* Segmentation based upon psychographics versus demographics
* How do we use our cluster analysis to drive a segmentation/targeting/positioning strategy?

#### Review and Setup for Ford Ka Case

* Clustering using k-Means Analysis (Goal/input/output/interpretation)


#### Ford Ka Case
* Questions
* What data do we have
* The Data Mining Process
    * State the problem
    * Collect the data
    * Preprocess the data
    * Estimate the model(mine the data)
    * Interpret the model and draw conclusions
* Steps for Preparing Data
    * Create data table
    * Characterize variables 
    * Clean data
    * Remove variables
    * Transform variables 
    * Segment table
  
#### Potential Segmentation Solutions
* k-Means Psychographic Solutions
* K-Means Demographic Solution

#### Discussion
* Compare our Cluster Solutions with Market Research Segments
* Relationship between Clusters and Choosers: Who should we target?
* Incremental Value of Demographic and Psychographic Data
* Tradeoffs between Attitudinal and Demographic Segments
* Using Ford’s Cluster Solution for Targeting


#### Alternative Solution
* How can we reduce the number of variables?
* Motivation for Alternative Method
* k-Means clusters on Questions
* Reflecting upon our solution





### 3.2 Limitations of k-Means - 366 
* Influence of Scaling Data on Clustering 
* Influence of Initial Starting Points 
* Limitations of k-Means in Detecting Patterns

#### Influence of Scaling Data on Clustering 
* Structuring the data for k-Means
* Compare the Scaled and Unscaled Ford Ka Demographic Data
* Summary

#### Influence of Initial Starting Points for k-Means
* Robustness of k-Means
* Compare k-Means with two different starting points
* Problem with Random Selection of Initial Centroids
* Illustration of k-Means using Packed Circles Moral: Bad initializations can yield bad solutions
* Solutions to Initialization Problem

#### Limitations of k-Means in Detecting Patterns
* Limitations of k-Means
    * k-Means has problems when clusters are of differing (Sizes/Densities/Non-globular shapes)
    * k-Means has problems when the data contains outliers
* Illustration of k-Means using a Smiley Face Moral: Overcome limitations by increasing k

#### Conclusions
* Discussion: Strengths & Weaknesses
* What Cluster Analysis is Not Supervised classification/ Simple segmentation/ Results of a query/ Graph partitioning
* Notion of a Cluster can be Ambiguous
* Illustration of k-Means using Uniform Data Moral: k-Means finds a structure even if your data lacks one
* Clustering
* Final Comment on Cluster Validity








## Lecture 4: Working with Unstructured Datasets
### 4.1 Analyzing Unstructured Data - 409
* Going beyond k-Means: Clustering Techniques
* Mining unstructured data like text
* Movie Scheduling Problem (not assigned, class example) 
* Probabilistic Clustering with Topic Modeling

#### Mining Unstructured Data
* Unstructured Datasets
* How do we represent text?
* “Bag of Words” example
* Some Important Statistical Properties of Text
* Why does “bag of words” work?
* Overview of Common Preparations for Text Mining

#### Representing Data as Matrices
* Transaction Data as Matrices (or Data Frames in R terminology)
* Matrices
* Vectors and Matrices
* Social Networks as Matrices
* Unstructured Data

#### Alternative Clustering Schemes
* Hierarchical Cluster
* Soft Clustering
* Topic Model (Probabilistic Clustering with LDAvis) of Yelp Reviews

#### Soft Clustering
* Contrasting Partition Clustering (k-Means) and Soft Clustering
* What if there is an underlying tendency?
* Probabilistic Clustering using Latent Dirichlet Allocation (Goal/ Input/ Output/ Interpretation)
 
#### Clustering Movies using the Text from Movie Reviews
* How do we analyze user reviews?
* What problems can we address with our review data?(Movie recommendation system/ Planning first-run release schedule/ Dimensionality reduction)

#### Clustering Movies with Topic Models
* Probabilistic Clustering illustrates a newer type of clustering
* Latent Dirichlet Allocation detects “topics” which provide latent dimensions to describe observation
* Example[重要]


#### Topic Modeling applied to the Movie Data with a Small Scale Dataset



#### Movie Scheduling Problem 
* Latent Dirichlet Allocation detects “topics” which provide latent dimensions to describe observations
* How are the tags in a movie generated?

#### Clustering Movies with Topic Models
* Summary

### 4.2 Topic Modeling Example - 477
* Probabilistic Clustering with Topic Models
* An example of Topics Models using the Iris Dataset

#### Probabilistic Clustering with Topic Models
* Probabilistic Clustering
* Latent Dirichlet Allocation
* Model Example
* Clustering using LDA
* Model Features
    * Latent topics drive probability of choosing a word
    * Probability of using a word given a topic is common across all users (e.g., “money” is the same for every document)
    * Each document’s topics are unique (but if there are not too many words in the document then the topics will look similar across documents)
    * Estimation using variational EM algorithm or Monte-Carlo Markov Chain (simulation approach)


#### Topic Modeling applied to the Iris Data
* Summary
    * Some types of clusters are well represented by k-Means
    * Probabilistic clustering is an alternative scheme
    * Topic Modeling is a specific type of probabilistic clustering that has been found to work well for modeling text data


### 4.3 Topic Modeling for Movie Reviews Problem - 504
### 4.4 Movie Scheduling Solution - 529







## Lecture 5: Predictive Modeling
### 5.1 Predictive Models - 545

#### What is a Predictive model？
* What is a model?
* Which model is best?
* What is a predictive model


#### Modeling Terminology
* Supervised Data Mining: Terminology
    * Feature Types (Numeric/Categorical)
    * Dimensionality of the data
    * Attributes/Target
    * Training/ A learner (Unduces a model from examples)
    * Refression modeling (Rather than classification modeling)

#### Conclusions
* Predictive Modeling 
* The steps in the modeling process


### 5.2 Evaluating Models - 562
* Lift Charts
* ROC Curves and AUC
* COnfusion Matrices and Cost

#### Computing Lift Charts

* Direct Marketing Evaluation
* Direct Marketing Paradigm
* Lift Charts
    * Model-Sorted List
    * CPH (Cumulative Pct Hits)
    * CPH: Random List vs Model-ranked list
    * Lift: Lift(P,M) = CPH(P,M)/P
    * Lift Properties
    * Lift Chart
    * Cumulative Lift Chart
* Gains Chart

#### Receiver Operating Characteristic (ROC) Curve

* ROC curves
* Area Under Curve

##### Evaluating our Model from a Buiness Viewpoint

* Measuring predictive ability
* Evaluating Classifiers
    * Accuracy
    * Error
    * Precision
    * Recall
    * FP rate
* Counting the Costs
* Confusion Matrices
    * Evaluating Confusion Matrices
    * Associating Costs (Or Benefits) with our confusion Matrix
    * Confusion cost matrix
    * Calculating Value by taking the expected cost (or gain)
    * Value of Perfect Information





### 5.3 Predictive Modeling using Logistic Regression - 596
* Logistic Regression Models
* Stepwise Variable Selection
* Example of Logistic Regression using Lending Club

#### Overview of Logistic Regression

* Different Types of Prediction Models
    * Linear Regression
    * Logistic Regression
    * Poisson Regression
* Overview of Logistic Regression
    * Predictive model is a weighted combination of the inputs like a regression model.
    * Results expressed in log-odds ratio
    * Specification
* Why use logistic regression?
* Logistic Regression Graphical Intuition
* Logistic Regression Mathematical Representation
* Logistic Regression Alternative Mathematical Representation
* Understanding Odds Ratios
* Understanding Log Transformation
* Logistic Regression Example
* Classification with Logistic Regression
* Evaluating Logistic Regression Predictions using Confusion Matrices


#### Logistic Regression Traning

* Understanding the Output
    * Estimate
    * Standard Error
    * Z-Value
    * P-Value
* How do we know which variables are important?[重要]
    * Look at the coefficients
    * Compare p-values (or Z-values)
    * Ask the model to compute a counterfactual
    * P675, Estimate/Est*SD/Importance
* Understanding Calculations of Importance: Why exp and stddev?

#### Stepwise Variable Selection

* Specifying your Logistic Regression Model
* Selection Techniques
    * Forward Selection
    * Backward Elimination
    * Stepwise Regression

#### Redoing Ford Ka with Stepwise Logistic Regression



#### Logistic Regression
* Training or Learning often requires the solution of an optimization problem (gradient descent)
* Takeaways for Logistic Regression
    * Closely related to Linear Regression
    * Scoring Model
    * Coefficient Interpretation
    * Variable Importance
* Summary of Logistic Regression

### 5.4 Logistic Regression Example for Lending Club - 684

* Findings: Predictive models are not just about making predictions, but about understanding relationships










## Lecture 6: Decision Trees, Overfitting and Evaluating Models
### 6.1 Freemium Case Introduction - 705

#### Freemium

* What do we know?
    * Free accounts generate advertising revenue.
    * Premium subscribers are more profitable than free users.
    * Premium subscribers are rare.
* Understanding our Data
    * Demographic characteristics
    * Social network characteristics
    * Engagement level data
* Generic strategy for data understanding
    * Look at your data
    * Exploratory analyses
    * Model your data
    * Make recommendations


### 6.2 Classification and Regression Trees - 719

#### Overview of Decision Trees

* Popular non-parametric model for classification and regression
    * Prediction model is a set of decision rules that are organized in a tree
    * Intuitive
    * Overfitting
* What can decision trees represent
    * Rules
    * Partitions
    * PERSPECTIVE PLOT
* Trees are good at detecting interactions
* Underlying Method
* How would we build this tree?
    * Measures of Uncertainty (Entropy/Gini/Min)
    * 计算P733[重要]
    * Choosing Splitting Variable (highest Gain)
* When to stop growing our tree?
* Alternative representation of Decision Tree is to define “Rules” that correspond with each leaf
* Errors or Randomness in Leaves (Relevance/Accuracy)
* Continuous attributes
* Missing Values
* Prediction/Regression Problem or Classification Problem


#### Avoiding Overfitting of Trees

* Overfitting data
* Overfitting and Decision Trees
* Summarizing Methods to Avoid Overfitting
    * Limits on number of data points in nodes before forcing it to be a leaf
    * Limits on depth
    * Statistical tests on significance of differences
    * Use of validation data: allow overfitting, then prune away based on new data (data not used to create tree)


#### Validating and Selecting Trees

* Evaluating
* The answer: Run an experiment
* Estimation with Training Data
* Estimation with Independent Test Data
* Hold-out Method (when direct experiment not available)
* Holdout validation
* Summary
    * Use part of your data for training (“training sample”)
    * Another part for validation (“validation”, “holdout”, “test set”)
    * Third sample for predicting the accuracy of your classifier (“prediction sample”)
    * Generally, the larger the training data the better the classifier (but returns diminish).

#### Conclusions

* Takeaways for Decision Trees
    * Interpretable
    * Overfitting
    * Avoid overfitting
    * Validation
    * Metrics

### 6.3 Decision Tree Examples - 762

* Which cutoff
* Which model
* Business sense
    * How can use use your model to improve the recommendation of which customers receive loans?
    * What KPIs or metrics should we use to judge the model?
    * If we follow your model recommendation then how much can we make?
* Summary
    * Confusion Matrix encapsulates the probability of correct (profitable) and incorrect (unprofitable) decisions
    * The decision of threshold determines whether we want to be aggressive in making loans (positive classification) or not making loans (negative classification)
* Findings
    * Predictive models are not just about making predictions, but about understanding relationships
    * You can use predictive models iteratively, to better understand the data, and then (perhaps collect better data and) build better models
    * Models can be judged on many metrics, but the most important one for a business context is how will it help you improve your decision (and increase profits)

### 6.4 Storytelling - 804









## Lecture 7: Data Mining Techniques for Prediction
### 7.1 Freemium Case Discussion - 858 

#### Frreemium Exercise (Decision Trees)

#### Frreemium Exercise (Logistic Regression)

* Training and Test Data
    * One way to approach this problem is to fit the model on one dataset (say half the data) and assess the fit on another
    * This is two-fold cross validation
* Selecting Models using an Information Criterion
* Freemium Logistic Regression Understanding our Score

### 7.2 Followup on Freemium Case - 947

#### Followup on Freemium
* Findings
* Potential Stories
* Social Engagement: From free to fee?
* Data and Commensurate Strategies (Marketing Strategies)


#### Why do we need to experiment
* Experimentation is needed:
    * When there is insufficient variation
    * The environment has changed
    * The variation we observe is due to natural variation in which we are uncertain about its causes
    * We need to demonstrate causality


#### Lack of correlation does not imply independence

* Statistical Definitions
    * Correlation
    * Independence

#### Correlation versus Causation

* Possible relationships between two events A and B:
    * A causes B (direct causation);
    * B causes A (reverse causation);
    * A and B are both caused by C
    * A causes B and B causes A (bidirectional or cyclic causation);
    * There is no connection between A and B; the correlation is a coincidence

#### Omitted Variables

* Recoding missing values
    * The coefficient on the missing value detects an omitted effect (e.g., perhaps the variable is not missing at random)
 

#### Experimentation to address Freemium’s problem

* Flip the Question: Causation versus Correlation
* “Ideal” Experiment
* Alternative is a “Difference in Difference”
* Implementation of Difference-in-Difference
    * Simple two-period, two-group comparison which is very useful in combination with randomization and matching
* Similar to a difference-in-difference model what if we look at changes in the variable over time?
    * levels
    * changes
* The Virtuous Cycle Exists


### 7.3 Understanding our Logistic Regression for the Freemium Exercise - 1000


#### Learning about Freemium adopters from Logistic (重复)

* How do we know which variables are important?[重要]
* Understanding Calculations of Importance
* Why exp and stddev?[重要]

#### Regression Telling a story from Logistic Regression
#### How to cluster our logistic regression output



### 7.4 Evaluating Profits for Freemium - 1029

#### Decision Tree Analysis
* How to compare models?
    * Training sample
    * Validation sample
    * Prediction sample

#### Revisit Freemium Exercise
* Which is the right cut-off
* Model Accuracy (Validation Sample) using different cut-offs
* Offer/Profits
* Conclusions
* Key Takeways
    * Evaluate models based upon their impact on the outcome
    * Choose the model that gives us the best result not the most accurate prediction
    * Often our data gives us the result if we do nothing, but we are interested in assessing what happens if we do something new






## Lecture 8: Pro-Active Churn Management
### 8.1 Random Forests and Neural Networks - 1062
* Ensemble Learners
    * Random Forests
    * Gradient Boosted Trees
* Neural Networks

#### Ensemble Learners: Random Forests and Gradient Boosted Trees

* “The Wisdom of Crowds”
* Bootstrap Sampling (or Resampling) or Bootstrap Aggregating (Bagging)
* Random Forests
* Bootstrapping helps us avoid overfitting by choosing many weak learners and averaging them
* Understanding Random Forests
    * Recall how CART is used in practice
    * Random Forests avoid the need for CV
* Model Averaging
* Summarizing Random Forests
* Summarizing Gradient Boosted Trees
* Summarizing Ensemble Methods
* Contrasting Forests and Boosted Trees
* Summary
    * Random Forests and Gradient Boosted Trees take advantage of advanced statistical methods to improve a single tree by constructing an ensemble of trees
    * Ensemble of trees work by taking ”weak” learners or models to create a new meta-model.
    * Advantages:
        * Improved predictions
    * Disadvantages:
        * More time consuming to compute   
        * More difficult to explain than a single learner or model 
        * Sensitive to hyper-parameters like the number of trees

#### Neural Networks (and Deep Learning)

* Neural Networks: Analogy to Brain
* Simplified Neuron
* Linear Aggregation
* Transfer Functions
* Networks of perceptrons
* Hopfield Networks
* Neural Network
* Deep Learning Models have many layers
* Summary
    * Advantages
    * Disadvantages
* Why Deep Learning

#### Conclusions

* Supervised Learning


### 8.2 Cell2Cell Assignment Introduction - 1118




## Lecture 9: Data Based Decision Making
### 9.1 Pro-active Churn Prevention - 1164

* Model Building Process
* Model (Decision Tree)
* Model (Logistic Regression)[重要]
* Choose
* Oversampling

### 9.2 Pro-active Churn Prevention, Preparing for Cell2Cell Part 2 - 1328








## Lecture 10: Business Strategy for Employing Data Science

### 10.1 Review of Data Science for Business - 1361
* Building an Analytics Checklist 
* Course Review
* Modeling Review
* Final Thoughts

#### Building an Analytics Checklist
* What are pitfalls for each analysis?
    * Prescriptive Analytics
    * Predictive Analytics
    * Descriptive Analytics
* Checklist: Prescriptive Models
    * Metrics
    * Calibration
    * Integer Varibales
    * Alternate Solutions
    * Bingding Constraints
    * Simulation Distributions
* Checklist: Predictive Models
    * Sampling
    * Data Spending
    * Decision Tree Relationships
    * Logistic Regression Variable Importance
    * Regression Variable Selection
    * Model Complexity
    * Sanity Check
    * Correlation Versus Causation
* Checklist: Descriptive Models
    * Variable scales
    * Clustering Variable Selection
    * Significance of Patterns
    * Visualizations that enable interpretation
    * Stationarity
    * Sampling biases
* Riseks
    * Privacy
    * Security
    * Legality
    * Ethicality
* Key Takeaways: Pitfalss on the way to impact

#### Course Review

* Course Objectives
    * Understand the data mining process 
    * Introduce and apply a set of data mining tools
    * Apply these techniques to specific case studies to solve business and e- commerce problems
* WHat is Data Science
* What is "Data"? (What are its strengths and weaknesses of an empirical science?)
* What is "Science" Part? (Finding Patterns using Data Mining Process)
* Predictive Models
    * Optimal Pricing (Log-linear regression)
    * Customer Churn (Logistic regression)
    * Production Recommendation (k-nearest neighbor)
* Ten popular data mining algorithms
* What type of software

##### Modeling Review

* Logistic Regression Example
    * Mathematical Representation
    * Graphical Intuition
    * Prediction and Understanding
    * Solution
    * Understanding Odds Ratios
    * Training Models: How do we find the parameters (β) ?
    * Evaluating Models: Which model is best?
    * Training Errors (Fit) versus Model Complexity (Prediction)
    * Communicating the Results
    * Understanding Variable Influence
    * Create "Stories" from your models
* Review: What are the main lessons we have learned?
    * Ford Ka
    * Movie Scheduling
    * Lending Club
    * Freemium
    * Cell2Cell


#### Final Thoughts
* Some General Comments
    * Data science not an automatic process
    * Data science should not be taken as a “black box”
    * Data science makes you care more about accurate data, not less 
    * There are many ethical and legal traps to think about
    * It works: data mining does help you use data better!
* Where to learn more about data science
* Quick list of useful R packages
* Quick list of useful R packages
* Curated list of Awesome R packages and tools
* COnclusion



### 10.2 Cell2Cell Case Discussion - 1401


#### Cell2Cell Potential Solution【需要再研究】

* Potential Offers to Make to Customers
* Expected Results if Promotional Offer given to All Customers
* Expected Results of Pro-Active Retention Campaign
* Returns from Pro-Active Retention Campaign
* Returns from Pro-Active Retention Campaign using Test Data

#### Managing Customer Churn【需要再研究】

* Overview
* Customer churn in a telco
* Game Plan: Determining How Much and What to Offer, and Value at Stake
    * 1) Lifetime Value Calculation
        * Customer value depends on Retention and Profits
        * Lifetime Value as a Function of Retention
        * Profitability of Proactive Retention Plan (Profit & LV)
    * 2) How Much and What to Offer?
        * What is the maximum possible incentive cost?
        * Maximum Incentive Cost
    * 3) Which predictive model is better? (Simple, Complex, Random Forest or Gradient Boosted Models)
        * Definite tradeoffs
            * Complexity of models
            * Interpretation and explainability of models
            * Insights into relationships
            * Effort to draw those insights
    * Understand which factors drive Churn using Logistic Regression Model
    * Focus on factors that drive churn
        * Translating a Logistic Regression into Action
        * Specifying the Incentives: What variables are actionable?
        * Develop the Incentive Plan
    * Values at Stake
        * Profitablility of Proactive Churn Program
        * Profitability as a Function of Lift
    * How to evaluate the program?
* Summary
    * Reactive churn management vs. Proactive churn management
    * Predictive modeling approach/ Can afford stronger incentives to the extent/ No guarantee the program will work – need to experiment

#### Duke’s Teradata Center Churn Modeling Tournament

* Tournament Structure
* Participants
* Tournament Data
* Prediction Criteria
    * Top Decile Lift
    * Gini Coefficient
* Estimation Methods/ Submission Methods/ Number of Variables in Model/ Time Allocation/ Divided Calibration Sample
* Overall Performance
* Summary
* Best Methodologies
* Summary about Tree

#### Review and Conclusions