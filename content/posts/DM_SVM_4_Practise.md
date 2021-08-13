---
title: SVM：Practise
author: "Misty"
tags: ["SVM","Model"]
categories: ["Data Mining"]
date: 2021-05-04
---

# SVM模型

## SVM模型的思想和理论 

### 模型介绍

超平面的理解:在一维空间中，如需将数据切分为两段，只需要一个点即可;在二维空间中，对于线性可分的样本点，将其切分为两类，只需一条直线即
可;在三维空间中，将样本点切分开来，就需要一个平面。

#### 距离计算

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504204350.png)

### 思想介绍

* 图中绘制了两条分割直线,利用这两条直线,可以方便地将样本点所属的类别判断出来。虽然从直观上来看这两条分割线都没有问题,但是哪一条直线的分类效果更佳呢(训练样本点的分类效果一致,并不代表测试样本点的分类效果也一样)?甚至于在直线l1和l2之间还存在无数多个分割直线,那么在这么多的分割线中是否存在一条最优的“超平面”呢?

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504205133.png)

* 假设直线是l1和l2之间的某条直线(分割面),为了能够寻找到最优的分割面l2,需要做三件事,首先计算两个类别中的样本点到直线li的距离;然后从两组距离中各挑选出一个最短的(如图中所示的距离d1和d2),继续比较d1和d2,再选出最短的距离(如图中的d1),并以该距离构造“分割带”(如图中经平移后的两条虚线);最后利用无穷多个分割直线li,构造无穷多个“分割带”,并从这些“分割 带”中挑选出带宽最大的li。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504213934.png)

### 分隔带

* “分割带”代表了模型划分样本点的能力或可信度，“分割带”越宽，说明模型能够将样本点划分得越清晰，进而保证模型泛化能力越强，分类的可信度越高;反之，“分割带”越窄，说明模型的准确率越容易受到异常点的影响，进而理解为模型的预测能力越弱，分类的可信度越低。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504214002.png)

### 目标函数

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504214040.png)

#### 函数间隔

* 将图中五角星所代表的正例样本用1表示,将实心圆所代表的负例样本用-1表示;实体加粗直线表示某条分割面;两条虚线分别表示因变量y取值为+1和-1时的情况,它们与分割面平行。
* 不管是五角星代表的样本点,还是实心圆代表的样本点,这些点均落在两条虚线以及虚线之外,则说明这些点带入到方程w'x+b所得的绝对值一定大于等于1
* 进而可以说明如果点对应的取值越小于-1,该样本为负例的可能性越高;点对应的取值越大于+1,样本为正例的可能性越髙。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504214439.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504214459.png)

* 其中,yi表示样本点所属的类别,用+1和-1表示当w'xi+b计算的值小于等于-1时,根据分割面可以将样本点xi对应的yi预测为-1;当w'xi+b计算的值大于等于+1时,分割面会将样本点xi对应的yi预测为+1。故利用如上的乘积公式可以得到线性可分的SVM所对应的函数间隔满足yi≥1的条件。

#### 几何间隔

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504214737.png)

* 当分割面中的参数w和b同比例增加时,所对应的γ值也会同比例增加,但这样的增加对分割面W'x+b=0来说却丝毫没有影响。
* 所以,为了避免这样的问题,需要对函数间隔做约束,常见的约束为单位化处理。


## 线性可分的SVM

### 目标函数

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504220058.png)

#### 目标函数的等价转换

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504220125.png)


### 基于拉格朗日乘子法的目标函数

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504220224.png)

#### 拉格朗日乘子法

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504220153.png)

### 目标函数求解

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504220305.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504220332.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504220350.png)

### 函数介绍

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504220426.png)



## 非线性可分的SVM

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504221321.png)

### 目标函数

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504221341.png)

#### 目标函数的求解

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504221405.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504221417.png)


### 核函数

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504221503.png)

### 函数介绍

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504221647.png)


## 实操

### 案例1

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504224438.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504224456.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504224516.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210504224529.png)

### 案例2

```python
# 导入第三方模块
from sklearn import svm
import pandas as pd
from sklearn import model_selection
from sklearn import metrics


# 读取外部数据
letters = pd.read_csv(r'letterdata.csv')
# 数据前5行
letters.head()


# 将数据拆分为训练集和测试集
predictors = letters.columns[1:]
X_train,X_test,y_train,y_test = model_selection.train_test_split(letters[predictors], letters.letter，test_size = 0.25, random_state = 1234)


# 选择线性可分SVM模型
linear_svc = svm.LinearSVC()
# 模型在训练数据集上的拟合
linear_svc.fit(X_train,y_train)


# 模型在测试集上的预测
pred_linear_svc = linear_svc.predict(X_test)
# 模型的预测准确率
metrics.accuracy_score(y_test, pred_linear_svc)


# 选择非线性SVM模型
nolinear_svc = svm.SVC(kernel='rbf')
# 模型在训练数据集上的拟合
nolinear_svc.fit(X_train,y_train)


# 模型在测试集上的预测
pred_svc = nolinear_svc.predict(X_test)
# 模型的预测准确率
metrics.accuracy_score(y_test,pred_svc)

```

```python  
# 读取外部数据
forestfires = pd.read_csv(r'forestfires.csv')
# 数据前5行
forestfires.head()


# 删除day变量
forestfires.drop('day',axis = 1, inplace = True)
# 将月份作数值化处理
forestfires.month = pd.factorize(forestfires.month)[0]
# 预览数据前5行
forestfires.head()


# 导入第三方模块
import seaborn as sns
import matplotlib.pyplot as plt
from scipy.stats import norm
# 绘制森林烧毁面积的直方图
sns.distplot(forestfires.area, bins = 50, kde = True, fit = norm, hist_kws = {'color':'steelblue'}, 
             kde_kws = {'color':'red', 'label':'Kernel Density'}, 
             fit_kws = {'color':'black','label':'Nomal', 'linestyle':'--'})
# 显示图例
plt.legend()
# 显示图形
plt.show()


# 导入第三方模块
from sklearn import preprocessing
import numpy as np
from sklearn import neighbors
# 对area变量作对数变换
y = np.log1p(forestfires.area)
# 将X变量作标准化处理
predictors = forestfires.columns[:-1]
X = preprocessing.scale(forestfires[predictors])



# 将数据拆分为训练集和测试集
X_train,X_test,y_train,y_test = model_selection.train_test_split(X, y, test_size = 0.25, random_state = 1234)


# 构建默认参数的SVM回归模型
svr = svm.SVR()
# 模型在训练数据集上的拟合
svr.fit(X_train,y_train)
# 模型在测试上的预测
pred_svr = svr.predict(X_test)
# 计算模型的MSE
metrics.mean_squared_error(y_test,pred_svr)



# 使用网格搜索法，选择SVM回归中的最佳C值、epsilon值和gamma值
epsilon = np.arange(0.1,1.5,0.2)
C= np.arange(100,1000,200)
gamma = np.arange(0.001,0.01,0.002)
parameters = {'epsilon':epsilon,'C':C,'gamma':gamma}
grid_svr = model_selection.GridSearchCV(estimator = svm.SVR(max_iter=10000),param_grid =parameters,
                                        scoring='neg_mean_squared_error',cv=5,verbose =1, n_jobs=2)
# 模型在训练数据集上的拟合
grid_svr.fit(X_train,y_train)
# 返回交叉验证后的最佳参数值
print(grid_svr.best_params_, grid_svr.best_score_)


# 模型在测试集上的预测
pred_grid_svr = grid_svr.predict(X_test)
# 计算模型在测试集上的MSE值
metrics.mean_squared_error(y_test,pred_grid_svr)


```

## 面试常用题

* [机器学习——SVM算法面试总结](https://blog.csdn.net/u013793732/article/details/80117521)

* [SVM常见面试点](https://blog.csdn.net/qy724728631/article/details/82622535)

* [数据挖掘（机器学习）面试--SVM面试常考问题](https://blog.csdn.net/szlcw1/article/details/52259668)

