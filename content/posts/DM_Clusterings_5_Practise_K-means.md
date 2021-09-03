---
title: Clusterings：Practise(K-means)
author: "Misty"
tags: ["Clusterings","Model"]
categories: ["Data Mining"]
date: 2021-02-06
---

# Clusterings

## K-means聚类的思想和原理

### 模型介绍

对于监督的数据挖掘算法而言，数据集中需要包含标签变量（即因变量y的值）。但在有些场景下，并没有给定的y值，对于这类数据的建模，一般称为无监督的数据挖掘算法，最典型的当属聚类算法。

K-means聚类算法利用距离远近的思想将目标数据为制定的k个簇，进而使样本呈现簇内差异小，簇间差异大的特征。

### 聚类步骤

1. 从数据中随机挑选k个样本点作为原始的簇中心 
2. 计算剩余样本与簇中心的距离，并把各样本标记为离k个簇中心最近的类别
3. 重新计算各簇中样本点的均值，并以均值作为新的k个簇中心 
4. 不断重复第二步和第三步，直到簇中心的变化趋于稳定，形成最终的k个簇
 
### 原理介绍

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210311172801.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210311172836.png)


## 最佳K值的选择

### 拐点法

簇内离差平方和拐点法的思想很简单，就是在不同的k值下计算簇内利差平方和，然后通过可视化的方法找到“拐点”所对应的k值。当折线图中的斜率由大突然变小时，并且之后的斜率变化缓慢，则认为突然变化的点就是寻找的目标点，因为继续随着簇数k的增加，聚类效果不再有大的变化。

```python
def k_SSE(X,cluster):
    # 选择连续的K种不同的值
    K = range(1,clusters+1)
    # 构建空列表用于存储总的簇内离差平方和
    TSSE = []
    for k in K:
        # 用于存储各个簇内离差平方和
        SSE = []
        kmeans = KMeans(n_clusters = k)
        Kmeans.fit(X)
        # 返回簇标签
        labels = Kmeans.labels_
        # 返回簇中心
        centers = Kmeans.cluster_centers_
        # 计算各簇样本的离差平方和，并保存到列表中
        for label in set(labels):
            SEE.append(np.sum((X.loc[labels == label,]-centers[label,:])**2))
        # 计算总的簇内离差平方和
        TSSE.append(np.sum(SSE))
```

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210311180151.png)

### 轮廓系数法

该方法综合考虑了簇的密集性和分散性两个信息，如果数据集被分割为理想的k各簇，那么对应的簇内样本会很密集，而簇间样本会很分散，轮廓系数的计算公式可以表示为：

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210311174618.png)

其中，a(i)体现了簇内的密集性，代表样本i与同簇内其他样本点距离的平均值；b(i)反映了簇间的分散性，它的计算过程是，样本i与其他非同簇样本点距离的平均值，然后从平均值中挑选出最小值。

当S(i)接近于-1时，说明样本i分配的不合理，需要将分配到其他簇中；当S(i)近似为0时，说明样本i落在了模糊地带，即簇的边界处；当S(i)近似为1时，说明样本i的分配是合理的。

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210311175629.png)

```python
# 构造自定义函数
def k_silhouette(X,clusters):
    K = range(2,clusters+1)
    # 构建空列表，用于存储不同簇数下的轮廓系数
    S = []
    for k in K:
        kmeans = KMeans(n_clusters = k)
        Kmenas.fit(X)
        labels = Kmeans.labels
        # 调用子模块metrics中的silhouette_score函数，计算轮廓系数
        S.append(metrics.silhouette_score(X, labels, metric = 'euclidean'))
```

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210311180217.png)

## Kmeans聚类的实操

### 函数介绍

```python
KMeans(n_clusters=8, init='k-means++', n_init=10, max_iter=300, tol=0.0001)
```

* n_clusters:用于指定聚类的簇数 
* init:用于指定初始的簇中心设置方法，如果为'k-means++'，则表示设置的初始簇中心之间相距较远;如果为'random'，则表示从数据集中随机挑选k个样本作为初始簇中心;如果为数组，则表示用户指定具体的簇中心
* n_init:用于指定Kmeans算法运行的次数，每次运行时都会选择不同的初始簇中心，目的是防止算法收敛于局部最优，默认为10
* max_iter:用于指定单次运行的迭代次数，默认为300 
* tol:用于指定算法收敛的阈值，默认为0.0001

### 最佳K值的选择

数据构建

```python
# 导入第三方包
import pandas as pd
import numpy as np  
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn import metrics

# 随机生成三组二元正态分布随机数 
np.random.seed(1234)
mean1 = [0.5, 0.5]
cov1 = [[0.3, 0], [0, 0.3]]
x1, y1 = np.random.multivariate_normal(mean1, cov1, 1000).T

mean2 = [0, 8]
cov2 = [[1.5, 0], [0, 1]]
x2, y2 = np.random.multivariate_normal(mean2, cov2, 1000).T

mean3 = [8, 4]
cov3 = [[1.5, 0], [0, 1]]
x3, y3 = np.random.multivariate_normal(mean3, cov3, 1000).T

# 绘制三组数据的散点图
plt.scatter(x1,y1)
plt.scatter(x2,y2)
plt.scatter(x3,y3)
# 显示图形
plt.show()
```

拐点法

```python
# 构造自定义函数，用于绘制不同k值和对应总的簇内离差平方和的折线图
def k_SSE(X, clusters):
    # 选择连续的K种不同的值
    K = range(1,clusters+1)
    # 构建空列表用于存储总的簇内离差平方和
    TSSE = []
    for k in K:
        # 用于存储各个簇内离差平方和
        SSE = []
        kmeans = KMeans(n_clusters=k)
        kmeans.fit(X)
        # 返回簇标签
        labels = kmeans.labels_
        # 返回簇中心
        centers = kmeans.cluster_centers_
        # 计算各簇样本的离差平方和，并保存到列表中
        for label in set(labels):
            SSE.append(np.sum((X.loc[labels == label,]-centers[label,:])**2))
        # 计算总的簇内离差平方和 
        TSSE.append(np.sum(SSE))

    # 中文和负号的正常显示
    plt.rcParams['font.sans-serif'] = ['Microsoft YaHei']
    plt.rcParams['axes.unicode_minus'] = False
    # 设置绘图风格
    plt.style.use('ggplot')
    # 绘制K的个数与GSSE的关系
    plt.plot(K, TSSE, 'b*-')
    plt.xlabel('簇的个数')
    plt.ylabel('簇内离差平方和之和')
    # 显示图形
    plt.show()

# 将三组数据集汇总到数据框中
X = pd.DataFrame(np.concatenate([np.array([x1,y1]),np.array([x2,y2]),np.array([x3,y3])], axis = 1).T)
# 自定义函数的调用
k_SSE(X, 15)
```
轮廓系数法
```python
# 构造自定义函数，用于绘制不同k值和对应轮廓系数的折线图
def k_silhouette(X, clusters):
    K = range(2,clusters+1)
    # 构建空列表，用于存储个中簇数下的轮廓系数
    S = []
    for k in K:
        kmeans = KMeans(n_clusters=k)
        kmeans.fit(X)
        labels = kmeans.labels_
        # 调用字模块metrics中的silhouette_score函数，计算轮廓系数
        S.append(metrics.silhouette_score(X, labels, metric='euclidean'))

    # 中文和负号的正常显示
    plt.rcParams['font.sans-serif'] = ['Microsoft YaHei']
    plt.rcParams['axes.unicode_minus'] = False
    # 设置绘图风格
    plt.style.use('ggplot')    
    # 绘制K的个数与轮廓系数的关系
    plt.plot(K, S, 'b*-')
    plt.xlabel('簇的个数')
    plt.ylabel('轮廓系数')
    # 显示图形
    plt.show()
    
# 自定义函数的调用
k_silhouette(X, 15)
```

### iris聚类--已知k值的情况

```python
# 导入第三方包
import pandas as pd
import numpy as np  
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn import metrics

# 读取iris数据集
iris = pd.read_csv(r'iris.csv')
# 查看数据集的前几行
iris.head()

# 提取出用于建模的数据集X
X = iris.drop(labels = 'Species', axis = 1)
# 构建Kmeans模型
kmeans = KMeans(n_clusters = 3)
kmeans.fit(X)
# 聚类结果标签
X['cluster'] = kmeans.labels_
# 各类频数统计
X.cluster.value_counts()

# 导入第三方模块
import seaborn as sns

# 三个簇的簇中心
centers = kmeans.cluster_centers_
# 绘制聚类效果的散点图
sns.lmplot(x = 'Petal_Length', y = 'Petal_Width', hue = 'cluster', markers = ['^','s','o'], 
           data = X, fit_reg = False, scatter_kws = {'alpha':0.8}, legend_out = False)
plt.scatter(centers[:,2], centers[:,3], marker = '*', color = 'black', s = 130)
plt.xlabel('花瓣长度')
plt.ylabel('花瓣宽度')
# 图形显示
plt.show()

# 增加一个辅助列，将不同的花种映射到0,1,2三种值，目的方便后面图形的对比
iris['Species_map'] = iris.Species.map({'virginica':0,'setosa':1,'versicolor':2})
# 绘制原始数据三个类别的散点图
sns.lmplot(x = 'Petal_Length', y = 'Petal_Width', hue = 'Species_map', data = iris, markers = ['^','s','o'],
           fit_reg = False, scatter_kws = {'alpha':0.8}, legend_out = False)
plt.xlabel('花瓣长度')
plt.ylabel('花瓣宽度')
# 图形显示
plt.show()
```

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210311180930.png)

### NBA球员聚类--未知k值的情况

```python
# 导入第三方包
import pandas as pd
import numpy as np  
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn import metrics
import seaborn as sns

# 读取球员数据
players = pd.read_csv(r'players.csv')
players.head()

# 绘制得分与命中率的散点图
sns.lmplot(x = '得分', y = '命中率', data = players, 
           fit_reg = False, scatter_kws = {'alpha':0.8, 'color': 'steelblue'})
plt.show()
```

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210311181102.png)


```python
from sklearn import preprocessing
# 数据标准化处理
X = preprocessing.minmax_scale(players[['得分','罚球命中率','命中率','三分命中率']])
# 将数组转换为数据框
X = pd.DataFrame(X, columns=['得分','罚球命中率','命中率','三分命中率'])
```

```python
# 构造自定义函数，用于绘制不同k值和对应总的簇内离差平方和的折线图
def k_SSE(X, clusters):
    # 选择连续的K种不同的值
    K = range(1,clusters+1)
    # 构建空列表用于存储总的簇内离差平方和
    TSSE = []
    for k in K:
        # 用于存储各个簇内离差平方和
        SSE = []
        kmeans = KMeans(n_clusters=k)
        kmeans.fit(X)
        # 返回簇标签
        labels = kmeans.labels_
        # 返回簇中心
        centers = kmeans.cluster_centers_
        # 计算各簇样本的离差平方和，并保存到列表中
        for label in set(labels):
            SSE.append(np.sum((X.loc[labels == label,]-centers[label,:])**2))
        # 计算总的簇内离差平方和 
        TSSE.append(np.sum(SSE))

    # 中文和负号的正常显示
    plt.rcParams['font.sans-serif'] = ['Microsoft YaHei']
    plt.rcParams['axes.unicode_minus'] = False
    # 设置绘图风格
    plt.style.use('ggplot')
    # 绘制K的个数与GSSE的关系
    plt.plot(K, TSSE, 'b*-')
    plt.xlabel('簇的个数')
    plt.ylabel('簇内离差平方和之和')
    # 显示图形
    plt.show()
```

```python
# 使用拐点法选择最佳的K值
k_SSE(X, 15)
```

```python
# 构造自定义函数，用于绘制不同k值和对应轮廓系数的折线图
def k_silhouette(X, clusters):
    K = range(2,clusters+1)
    # 构建空列表，用于存储个中簇数下的轮廓系数
    S = []
    for k in K:
        kmeans = KMeans(n_clusters=k)
        kmeans.fit(X)
        labels = kmeans.labels_
        # 调用字模块metrics中的silhouette_score函数，计算轮廓系数
        S.append(metrics.silhouette_score(X, labels, metric='euclidean'))

    # 中文和负号的正常显示
    plt.rcParams['font.sans-serif'] = ['Microsoft YaHei']
    plt.rcParams['axes.unicode_minus'] = False
    # 设置绘图风格
    plt.style.use('ggplot')    
    # 绘制K的个数与轮廓系数的关系
    plt.plot(K, S, 'b*-')
    plt.xlabel('簇的个数')
    plt.ylabel('轮廓系数')
    # 显示图形
    plt.show()
```

```python
# 使用轮廓系数选择最佳的K值
k_silhouette(X, 10)
```

```python
# 将球员数据集聚为3类
kmeans = KMeans(n_clusters = 3)
kmeans.fit(X)
# 将聚类结果标签插入到数据集players中
players['cluster'] = kmeans.labels_
# 构建空列表，用于存储三个簇的簇中心
centers = []
for i in players.cluster.unique():
    centers.append(players.loc[players.cluster == i,['得分','罚球命中率','命中率','三分命中率']].mean())
# 将列表转换为数组，便于后面的索引取数
centers = np.array(centers)

# 绘制散点图
sns.lmplot(x = '得分', y = '命中率', hue = 'cluster', data = players, markers = ['^','s','o'],
           fit_reg = False, scatter_kws = {'alpha':0.8}, legend = False)
# 添加簇中心
plt.scatter(centers[:,0], centers[:,2], c='k', marker = '*', s = 180)
plt.xlabel('得分')
plt.ylabel('命中率')
# 图形显示
plt.show()
```

### K-means参数

[参考网站](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html#)