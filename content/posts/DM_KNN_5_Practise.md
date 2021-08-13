---
title: KNN：Practise
author: "Misty"
tags: ["KNN","Model"]
categories: ["Data Mining"]
date: 2021-04-21
---

# K近邻模型

## 模型思想

### 模型介绍

模型的本质就是寻找k个最近样本,然后基于最近样本做“预测”。对于离散型的因变量来说,从k个最近的已知类别样本中挑选出频率最高的类别用于未知样本的判断;对于连续型的因变量来说,则是将k个最近的已知样本均 值用作未知样本的预测。

### 执行步骤

* 确定未知样本近邻的个数k值。
* 根据某种度量样本间相似度的指标(如欧氏距离)将每一个末知类别样本的最近k个已知样本搜寻出来,形成一个个簇。
* 对搜寻出来的已知样本进行投票,将各簇下类别最多的分类用作未知样本点的预测。

## K值的选择

### 不同的K值带来的影响

* 根据经验发现，不同的k值对模型的预测准确性会有比较大的影响，如果k值过于偏小，可能会导致模型的过拟合；反之，又可能会使模型进入欠拟合状态。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210422171643.png)

### 设置投票权重/多重交叉检验

* k值的选择，一种是设置k近邻样本的投票权重，使用KNN算法进行分类或预测时设置的k值比较大，担心模型发生欠拟合的现象，一个简单有效的处理办法就是设置近邻样本的投票权重，如果已知样本距离未知样本比较远，则对应的权重就设置得低一些，否则权重就高一些，通常可以将权重设置为距离的倒数。
* 另一种是采用多重交叉验证法，该方法是目前比较流行的方案，其核心就是将k取不同的值，然后在每种值下执行m重的交叉验证，最后选出平均误差最小的k值。
* 也可以将两种方法结合，选出理想的k值。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210422172152.png)

## 距离度量

### 欧氏距离

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210422172330.png)

### 曼哈顿距离

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210422172346.png)

### 余弦相似度

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210422172404.png)

## 代码

### 函数说明

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210422172437.png)

### 代码演示

#### Example 1

```python
# 导入第三方包
import pandas as pd
# 导入数据
Knowledge = pd.read_excel(r'Knowledge.xlsx')
# 返回前5行数据
Knowledge.head()
```


```python
# 构造训练集和测试集
# 导入第三方模块
from sklearn import model_selection
# 将数据集拆分为训练集和测试集
predictors = Knowledge.columns[:-1]
X_train, X_test, y_train, y_test = model_selection.train_test_split(Knowledge[predictors], Knowledge.UNS, test_size = 0.25, random_state = 1234)
```


```python
# 导入第三方模块
import numpy as np
from sklearn import neighbors
import matplotlib.pyplot as plt

# 设置待测试的不同k值
K = np.arange(1,np.ceil(np.log2(Knowledge.shape[0]))).astype(int)
# 构建空的列表，用于存储平均准确率
accuracy = []
for k in K:
    # 使用10重交叉验证的方法，比对每一个k值下KNN模型的预测准确率
    cv_result = model_selection.cross_val_score(neighbors.KNeighborsClassifier(n_neighbors = k, weights = 'distance'), 
                                                X_train, y_train, cv = 10, scoring='accuracy')
    accuracy.append(cv_result.mean())

# 从k个平均准确率中挑选出最大值所对应的下标    
arg_max = np.array(accuracy).argmax()
# 中文和负号的正常显示
plt.rcParams['font.sans-serif'] = ['Microsoft YaHei']
plt.rcParams['axes.unicode_minus'] = False
# 绘制不同K值与平均预测准确率之间的折线图
plt.plot(K, accuracy)
# 添加点图
plt.scatter(K, accuracy)
# 添加文字说明
plt.text(K[arg_max], accuracy[arg_max], '最佳k值为%s' %int(K[arg_max]))
# 显示图形
plt.show()
```


```python
# 导入第三方模块
from sklearn import metrics

# 重新构建模型，并将最佳的近邻个数设置为6
knn_class = neighbors.KNeighborsClassifier(n_neighbors = 6, weights = 'distance')
# 模型拟合
knn_class.fit(X_train, y_train)
# 模型在测试数据集上的预测
predict = knn_class.predict(X_test)
# 构建混淆矩阵
cm = pd.crosstab(predict,y_test)
cm

```


```python
# 导入第三方模块
import seaborn as sns

# 将混淆矩阵构造成数据框，并加上字段名和行名称，用于行或列的含义说明
cm = pd.DataFrame(cm)
# 绘制热力图
sns.heatmap(cm, annot = True,cmap = 'GnBu')
# 添加x轴和y轴的标签
plt.xlabel(' Real Lable')
plt.ylabel(' Predict Lable')
# 图形显示
plt.show()

```


```python
# 模型整体的预测准确率
metrics.accuracy_score(y_test, predict)
```


```python
# 分类模型的评估报告
print(metrics.classification_report(y_test, predict))
```

#### Example 2


```python
# 读入数据
ccpp = pd.read_excel(r'CCPP.xlsx')
ccpp.head()
```


```python
# 返回数据集的行数与列数
ccpp.shape

```


```python
# 导入第三方包
from sklearn.preprocessing import minmax_scale
# 对所有自变量数据作标准化处理
predictors = ccpp.columns[:-1]
X = minmax_scale(ccpp[predictors])

```


```python
# 将数据集拆分为训练集和测试集
X_train, X_test, y_train, y_test = model_selection.train_test_split(X, ccpp.PE, 
                                                                    test_size = 0.25, random_state = 1234)

```


```python
# 设置待测试的不同k值
K = np.arange(1,np.ceil(np.log2(ccpp.shape[0]))).astype(int)
# 构建空的列表，用于存储平均MSE
mse = []
for k in K:
    # 使用10重交叉验证的方法，比对每一个k值下KNN模型的计算MSE
    cv_result = model_selection.cross_val_score(neighbors.KNeighborsRegressor(n_neighbors = k, weights = 'distance'), 
                                                X_train, y_train, cv = 10, scoring='neg_mean_squared_error')
    mse.append((-1*cv_result).mean())

# 从k个平均MSE中挑选出最小值所对应的下标  
arg_min = np.array(mse).argmin()
# 绘制不同K值与平均MSE之间的折线图
plt.plot(K, mse)
# 添加点图
plt.scatter(K, mse)
# 添加文字说明
plt.text(K[arg_min], mse[arg_min] + 0.5, '最佳k值为%s' %int(K[arg_min]))
# 显示图形
plt.show()

```


```python
# 重新构建模型，并将最佳的近邻个数设置为7
knn_reg = neighbors.KNeighborsRegressor(n_neighbors = 7, weights = 'distance')
# 模型拟合
knn_reg.fit(X_train, y_train)
# 模型在测试集上的预测
predict = knn_reg.predict(X_test)
# 计算MSE值
metrics.mean_squared_error(y_test, predict)

```


```python
# 对比真实值和实际值
pd.DataFrame({'Real':y_test,'Predict':predict}, columns=['Real','Predict']).head(10)
```


```python
# 导入第三方模块
from sklearn import tree

# 预设各参数的不同选项值
max_depth = [19,21,23,25,27]
min_samples_split = [2,4,6,8]
min_samples_leaf = [2,4,8,10,12]
parameters = {'max_depth':max_depth, 'min_samples_split':min_samples_split, 'min_samples_leaf':min_samples_leaf}
# 网格搜索法，测试不同的参数值
grid_dtreg = model_selection.GridSearchCV(estimator = tree.DecisionTreeRegressor(), param_grid = parameters, cv=10)
# 模型拟合
grid_dtreg.fit(X_train, y_train)
# 返回最佳组合的参数值
grid_dtreg.best_params_
```

```python
# 构建用于回归的决策树
CART_Reg = tree.DecisionTreeRegressor(max_depth = 25, min_samples_leaf = 10, min_samples_split = 4)
# 回归树拟合
CART_Reg.fit(X_train, y_train)
# 模型在测试集上的预测
pred = CART_Reg.predict(X_test)
# 计算衡量模型好坏的MSE值
metrics.mean_squared_error(y_test, pred)
```

