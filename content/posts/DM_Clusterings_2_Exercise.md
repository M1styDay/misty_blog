---
title: Clusterings：Exercise
author: "Misty"
tags: ["Clusterings","HKU"]
categories: ["Data Mining"]
date: 2021-02-09
---

# Clusterings

## K-Means Algorithm

### Input Points

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193007.png)

### Centroids

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193112.png)

### Reclustering

#### step 1

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193233.png)

#### Recomputing centroids

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193329.png)

#### step 2

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193439.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193531.png)

#### Recomputing the centroids

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193616.png)

#### step 3

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193653.png)

### Final Clustering

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309193738.png)



## K-Means++: Main Intuition

### Probaility distribution

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309194902.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309194941.png)

### Sampling points

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309195216.png)


### Examples

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309204543.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309204609.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309204634.png)

### K-means-

To understand why K-means++ use some randomness we compare it against the following algorithm which we call it K-means–:

The algorithm selects the first point randomly. Let t be any step of the algorithm, with 2 ≤ t < k. Let C be the set of points chosen at step t. The algorithm chooses a point p which maximizes d(p,C) where d(p,C) := minc∈C d(p,c).

### K-means++ vs. K-means-

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309205125.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309205147.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309205211.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309205234.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309205300.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210309205322.png)

## Supplement

### K-means++

K-Means++算法在聚类中心的初始化过程中的基本原则是使得初始的聚类中心之间的相互距离尽可能远，这样可以避免出现上述的问题。K-Means++算法的初始化过程如下所示：

* 在数据集中随机选择一个样本点作为第一个初始化的聚类中心
* 选择出其余的聚类中心：
    * 计算样本中的每一个样本点与已经初始化的聚类中心之间的距离，并选择其中最短的距离，记为d_i
    * 以概率选择距离最大的样本作为新的聚类中心，重复上述过程，直到k个聚类中心都被确定
* 对k个初始化的聚类中心，利用K-Means算法计算最终的聚类中心。

在上述的K-Means++算法中可知K-Means++算法与K-Means算法最本质的区别是在k个聚类中心的初始化过程。



