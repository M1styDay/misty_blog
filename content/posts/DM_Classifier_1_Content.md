---
title: Classifier：Content(ClassifierEvaluation)
author: "Misty"
tags: ["Classifier","HKU"]
categories: ["Data Mining"]
date: 2021-04-30
---

## Model Evaluation

* Metrics for Performance Evaluation
    * How to evaluate the performance of a model?
* Methods for Performance Evaluation
    * How to obtain reliable estimates?
* Methods for Model Comparison
    * How to compare the relative performance among competing models?

## Metrics for Performance Evaluation

### Confusion Matrix

* Focus on the predictive capability of a model 
    * Rather than running time, scalability, etc.
* Confusion Matrix:

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210430225315.png)

* Most widely-used metric:

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210430225353.png)

### Limitation of Accuracy
* Consider a 2-Class problem
    * Number of Class 1 examples = 10
    * Number of Class 0 examples = 9990
* If model predicts everything to be Class 0, accuracy is 9990/10000 = 99.9 %
    * Misleading: model does not detect any Class 1 example
    * Detecting the rare class is usually more interesting (frauds, intrusions, etc.)

### Alternative Measures: Precision, Recall, F-1


* Easy to get only high precision: ‘Yes’ only for instances we are “sure” about (e.g. easy to classify “robot” if 1000 pages/sec. collected) => low recall
* Trivial to get only high recall: classify all instances as ‘Yes’ => low precision
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210501003035.png)


* F-measure is the harmonic mean of p and r, which penalizes very small recall or very small precision
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210501235010.png)
* E.g. : Harmonic Mean (1,2,4) = 1/ (1/3 (1+1/2+/1/4)) = 12/7 (reciprocal of the arithmetic mean of the reciprocals)
* It can be shown min (x1,...,xn) <= H(x1,...,xn) <= n * min (x1,...,xn) 
    * min is very small then harmonic mean is very small.


## Methods for Performance Evaluation

* How to obtain a reliable estimate of performance?
* Performance of a model may depend on other factors besides the learning algorithm:
    * Class distribution
    * Cost of misclassification
    * Size of training and test sets

### Methods of Estimation

* Holdout
    * Reserve random 2/3 for training and 1/3 for testing
* Random subsampling
    * Repeated holdout (compute the average)
* Cross validation
    * Partition data into k disjoint subsets of the same size
    * k-fold: train on k-1 sets, test on the remaining one. Repeat k times, each subset being used exactly once for testing. Compute the average of the results.
    * Leave-one-out: k=n, (n-1 records training test, 1 test set)
* Bootstrap
    * Sampling with replacement

### Cross Validation to Estimate Parameter

* Goal
    * is classifier C1 better than C2?
    * which parameter for C1 or C2? max height? k in k-nn?
* Solution
    * perform k-fold cross validation for C1 and C2.Compute average accuracy, use best one.
    * perform k-fold cross validation for different parameter values and use best one.


## Methods for Model Comparison

### Test of Significance

* Use statistic tools to estimate the value of a parameter in a population (e.g. Wilson score interval, Jeffrey intervals, Clopper-Pearson, etc. )

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210502000107.png)

### Approximating Normal Distribution
* Normal distribution
    * does not work well if N<30, or p is close to 0 or 1
    * rule of thumb: Np>5 and N(1-p)>5
* More sophisticated techniques: Wilson score interval, Jeffrey intervals, Clopper-Pearson interval

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210502000303.png)
