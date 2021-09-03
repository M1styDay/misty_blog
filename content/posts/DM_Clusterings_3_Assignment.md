---
title: Clusterings：Assignment
author: "Misty"
tags: ["Clusterings","HKU"]
categories: ["Data Mining"]
date: 2021-02-08
---

# Clusterings

## Theoretical exercises on K-means
### Qustion 1

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309213215.png)

### Answer 1

#### Input Points and Set Centroids

Input P1=(0,0), P2=(0,1/2), P3=(1,1/2), P4=(1,1), P5=(4,0), P6=(4,1), P7=(5,1)

Set P1=(0,0) and P4=(1,1) as centroids

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309224023.png)

#### Reclustering

* STEP 1

For each point P2, P3, P5, P6, P7, determine the closest centroid

d(a,P1)|distance|d(a,P4)|distance
:---:|:---:|:---:|:---:|
d(P2,P1)|$\sqrt{  0^2 + (\frac{1}{2})^2  }$|d(p2,p4)|$\sqrt{  (\frac{1}{2})^2 + 1^2  }$
d(P3,P1)|$\sqrt{  (\frac{1}{2})^2 + 1^2  }$|d(P3,P4)|$\sqrt{  0^2 + (\frac{1}{2})^2  }$
d(P5,P1)|$\sqrt{  0^2 + 4^2  }$|d(P5,P4)|$\sqrt{  1^2 + 3^2  }$
d(P6,P1)|$\sqrt{  1^2 + 4^2  }$|d(P6,P4)|$\sqrt{  0^2 + 3^2  }$
d(P7,P1)|$\sqrt{  1^2 + 5^2  }$|d(P7,P4)|$\sqrt{  0^2 + 4^2  }$

P2 is assigned to the red cluster

P3,P5,P6,P7 are assigned to the green cluster

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309224132.png)

* Recomputing centroids

$\overline{C1}$ = (P1+P2)/2 = (0,0.25)

$\overline{C2}$ = (P3+P4+P5+P6+P7)/5 = (3,0.7)

* STEP 2

For each point P1, P2, P3, P4, P5, P6, P7, determine the closest centroid

d(a,$\overline{C1}$)|distance|d(a,$\overline{C2}$)|distance
:---:|:---:|:---:|:---:|
d(P1,$\overline{C1}$)|$\sqrt{  0^2 + (\frac{1}{4})^2  }$|d(p1,$\overline{C2}$)|$\sqrt{  3^2 + 0.7^2  }$
d(P2,$\overline{C1}$)|$\sqrt{  0^2 + (\frac{1}{4})^2  }$|d(p2,$\overline{C2}$)|$\sqrt{  3^2 + 0.2^2  }$
d(P3,$\overline{C1}$)|$\sqrt{  1^2 + (\frac{1}{4})^2  }$|d(P3,$\overline{C2}$)|$\sqrt{  2^2 + 0.2^2  }$
d(P4,$\overline{C1}$)|$\sqrt{  1^2 + (\frac{3}{4})^2  }$|d(P4,$\overline{C2}$)|$\sqrt{  2^2 + 0.3^2  }$
d(P5,$\overline{C1}$)|$\sqrt{  4^2 + (\frac{1}{4})^2  }$|d(P5,$\overline{C2}$)|$\sqrt{  1^2 + 0.7^2  }$
d(P6,$\overline{C1}$)|$\sqrt{  4^2 + (\frac{3}{4})^2  }$|d(P6,$\overline{C2}$)|$\sqrt{  1^2 + 0.3^2  }$
d(P7,$\overline{C1}$)|$\sqrt{  5^2 + (\frac{3}{4})^2  }$|d(P7,$\overline{C2}$)|$\sqrt{  2^2 + 0.3^2  }$

P1,P2,P3,P4 is assigned to the red cluster

P5,P6,P7 are assigned to the green cluster

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309230000.png)

* Recomputing centroids

$\overline{C1}$ = (P1+P2+P3+P4)/4 = (0.5,0.5)

$\overline{C2}$ = (PP5+P6+P7)/3 = ($\frac{13}{3}$,$\frac{2}{3}$)

* STEP 3

For each point P1, P2, P3, P4, P5, P6, P7, determine the closest centroid

d(a,$\overline{C1}$)|distance|d(a,$\overline{C2}$)|distance
:---:|:---:|:---:|:---:|
d(P1,$\overline{C1}$)|$\sqrt{  0.5^2 + 0.5^2  }$|d(p1,$\overline{C2}$)|$\sqrt{  (\frac{13}{3})^2 + (\frac{2}{3})^2  }$
d(P2,$\overline{C1}$)|$\sqrt{  0.5^2 + 0^2  }$|d(p2,$\overline{C2}$)|$\sqrt{  (\frac{13}{3})^2 + (\frac{2}{3}-0.5)^2  }$
d(P3,$\overline{C1}$)|$\sqrt{  0.5^2 + 0^2  }$|d(P3,$\overline{C2}$)|$\sqrt{  (\frac{13}{3}-1)^2 + (\frac{2}{3}-0.5)^2  }$
d(P4,$\overline{C1}$)|$\sqrt{  0.5^2 + 0.5^2  }$|d(P4,$\overline{C2}$)|$\sqrt{  (\frac{13}{3}-1)^2 + (1-\frac{2}{3})^2  }$
d(P5,$\overline{C1}$)|$\sqrt{  3.5^2 + 0.5^2  }$|d(P5,$\overline{C2}$)|$\sqrt{  (\frac{13}{3}-4)^2 + (\frac{2}{3})^2  }$
d(P6,$\overline{C1}$)|$\sqrt{  3.5^2 + 0.5^2  }$|d(P6,$\overline{C2}$)|$\sqrt{  (\frac{13}{3}-4)^2 + (1-\frac{2}{3})^2  }$
d(P7,$\overline{C1}$)|$\sqrt{  4.5^2 + 0.5^2  }$|d(P7,$\overline{C2}$)|$\sqrt{  (5-\frac{13}{3})^2 + (1-\frac{2}{3})^2  }$

P1,P2,P3,P4 stay the red cluster

P5,P6,P7 stay the green cluster

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309230000.png)

* Final Clustering

As the clustering did not change , the algorithm terminates with the following final clustering:

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309230000.png)


### Qustion 2

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210309213258.png)

### Answer 2

https://blog.csdn.net/shwan_ma/article/details/80096408

如果所有的点在指派步骤都未分配到某个簇，就会得到空簇。如果这种情况发生，则需要某种策略来选择一个替补质心，否则的话，平方误差将会偏大。一种方法是选择一个距离当前任何质心最远的点。这将消除当前对总平方误差影响最大的点。另一种方法是从具有最大SEE的簇中选择一个替补的质心。这将分裂簇并降低聚类的总SEE。如果有多个空簇，则该过程重复多次。另外编程实现时，要注意空簇可能导致的程序bug。


## Practical Exercise on Clustering

### Qustion 3

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210312000759.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210312000841.png)

### Answer 3

```python
import pandas as pd
import numpy as np  
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.cluster import KMeans
from sklearn import metrics
from sklearn import preprocessing
from sklearn.preprocessing import Normalizer
from __future__ import print_function

# raw data
stock = pd.read_csv(r'data.csv')

# cluster
X = stock.drop(labels = 'StockName', axis = 1)


#kmeans = KMeans(init='random',n_clusters=8)
kmeans = KMeans(init='k-means++',n_clusters=8)
kmeans.fit(X)

labels = kmeans.labels_
centers = kmeans.cluster_centers_

stock['cluster'] = kmeans.labels_

stock.cluster.value_counts()

for i in range(0,9):
    res = stock[kmeans.labels_ == i]
    stockname = res.loc[:,'StockName']
    print(stockname)

SSE = []
SSE_labels = []

for label in set(labels):
    SSE_labels.append(np.sum((X.loc[labels == label,]-centers[label,:])**2))


SSE.append(np.sum(SSE_labels))
print(SSE)
```

```python
import pandas as pd
import numpy as np  
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.cluster import KMeans
from sklearn import metrics
from sklearn import preprocessing
from sklearn.preprocessing import Normalizer
from __future__ import print_function


# Normalize the data

stock = pd.read_csv(r'data.csv')
X_first = stock['StockName']

X = stock.drop(labels = 'StockName', axis = 1)

norm_X_l1 = Normalizer(norm="l1").fit_transform(X)

stock_l1 = pd.DataFrame(norm_X_l1)

new_stock_l1 = pd.concat([X_first, stock_l1], axis=1)

# cluster
X_l1 = new_stock_l1.drop(labels = 'StockName', axis = 1)


#kmeans = KMeans(init='random',n_clusters=8)
kmeans = KMeans(init='k-means++',n_clusters=8)
kmeans.fit(X_l1)


labels = kmeans.labels_
centers = kmeans.cluster_centers_

new_stock_l1['cluster'] = kmeans.labels_

new_stock_l1.cluster.value_counts()

for i in range(0,9):
    res = new_stock_l1[kmeans.labels_ == i]
    stockname = res.loc[:,'StockName']
    print(stockname)

SSE_l1 = []
SSE_labels_l1 = []

for label in set(labels):
    SSE_labels_l1.append(np.sum((X_l1.loc[labels == label,]-centers[label,:])**2))


SSE_l1.append(np.sum(SSE_labels_l1))
print(SSE_l1)
```



