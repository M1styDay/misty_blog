---
title: Decision Trees：Practise
author: "Misty"
tags: ["Decistion Trees","Model"]
categories: ["Data Mining"]
date: 2021-04-06
---

# 决策树与随机森林

## 决策树节点字段的选择和阈值的选择 

### 决策树模型介绍

* 图中的决策树呈现自顶向下的生长过程，深色的椭圆表示树的根节点;浅色的椭圆表示树的中间节点;方框则表示树的叶节点。
* 对于所有的非叶节点来说，都是用来表示条件判断，而叶节点则存储最终的分类结果，例如中年分支下的叶节点(4,0)表示4位客户购买，0位客户不购买。

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401152754.png)


### 信息熵与条件熵

* 熵原本是物理学中的一个定义，后来香农将其引申到了信息论领域，用来表示信息量的大小。
* 信息量越大(分类越不“纯净”)，对应的熵值就越大，反之亦然。信息熵的计算公式如下:

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401152933.png)

* 在实际应用中，会将概率$P_k$的值用经验概率替换，所以经验信息熵可以表示为：

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401153045.png)

* 举例:以产品是否被购买为例，假设数据集一共包含14个样本，其中购买的用户有9个，没有购买 的用户有5个，所以对于是否购买这个事件来说，它的经验信息熵为:

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401153309.png)

* 条件熵

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401153436.png)

### 信息增益

* 信息增益：对于已知的事件A来说，事件D的信息增益就是D的信息熵与A事件下D的条件熵之差，事件A对于事件D的影响越大，条件熵H（D｜A）就会越小（在事件A的影响下，事件D就划分得越“纯净”），体现在信息增益熵就是差值越大，进而说明事件D的信息熵下降得越多。

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401153924.png)

* 所以，在根节点或中间节点的变量选择过程中，就是挑选出各自变量下因变量的信息增益最大的。

### 信息增益率

* 决策树中的ID3算法使用信息增益指标实现根节点或中间节点的字段选择，但是该指标存在一个非常明显的缺点，即信息增益会偏向于取值较多的字段。
* 为了克服信息增益指标的缺点，提出了信息增益率的概念，它的思想很简单，就是在信息增益的基础上进行相应的惩罚。信息增益率的公式可以表示为:

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401154419.png)

* 其中$H_A$为事件A的信息熵。事件A的取值越多$Gain_A$(D)可能越大，但同时$H_A$也会越大，这样以商的形式就实现了$Gain_A$(D)的惩罚。

### 基尼指数与条件基尼指数

* 决策树中的C4.5算法使用信息增益率指标实现根节点或中间节点的字段选择，但该算法与ID3算法一致，都只能针对离散型因变量进行分类，对于连续型的因变量就显得束手无策了。
* 为了能够让决策树预测连续型的因变量，Breiman等人在1984年提出了CART算法，该算法也称为分类回归树，它所使用的字段选择指标是基尼指数。

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401160202.png)

* 条件基尼指数

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401160257.png)

### 基尼指数增益

* 与信息增益类似，还需要考虑自变量对因变量的影响程度，即因变量的基尼指数下降速度的快慢，下降得越快，自变量对因变量的影响就越强。下降速度的快慢可用下方式子衡量:

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401160454.png)

### 生成算法与划分标准

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210401163004.png)



## 随机森林的思想

### 分类树与回归树

#### 分类树 
* 以C4.5分类树为例，C4.5分类树在每次分枝时，是穷举每一个feature的每一个阈值，找到使得按照feature<=阈值，和feature>阈值分成的两个分枝的熵最大的阈值(熵最大的概念可理解成尽可能每个分枝的男女比例都远离1:1)，按照该标准分枝得到两个新节点，用同样方法继续分枝直到所有人都被分入性别唯一的叶子节点，或达到预设的终止条件，若最终叶子节点中的性别不唯一，则以多数人的性别作为该叶子节点的性别。
* 总结：分类树使用信息增益或增益比率来划分节点；每个节点样本的类别情况投票决定测试样本的类别。

#### 回归树 
* 回归树总体流程也是类似，区别在于，回归树的每个节点（不一定是叶子节点）都会得一个预测值，以年龄为例，该预测值等于属于这个节点的所有人年龄的平均值。分枝时穷举每一个feature的每个阈值找最好的分割点，但衡量最好的标准不再是最大熵，而是最小化均方差即(每个人的年龄-预测年龄)^2 的总和 / N。也就是被预测出错的人数越多，错的越离谱，均方差就越大，通过最小化均方差能够找到最可靠的分枝依据。分枝直到每个叶子节点上人的年龄都唯一或者达到预设的终止条件(如叶子个数上限)，若最终叶子节点上人的年龄不唯一，则以该节点上所有人的平均年龄做为该叶子节点的预测年龄。
* 总结：回归树使用最大均方差划分节点；每个节点样本的均值作为测试样本的回归预测值


### 决策树模型函数说明

```python
DecisionTreeClassifier(criterion='gini', splitter='best', max_depth=None, min_samples_split=2, min_samples_leaf=1, max_leaf_nodes=None, class_weight=None)
```

* criterion:用于指定选择节点字段的评价指标，对于分类决策树，默认为'gini'，表示采用基尼指数选择节点的最佳分割字段;对于回归决策树，默认为'mse'，表示使用均方误差选择节点的最佳分割字段 
* splitter:用于指定节点中的分割点选择方法，默认为'best'，表示从所有的分割点中选择最佳分割点; 如果指定为'random'，则表示随机选择分割点 
* max_depth:用于指定决策树的最大深度，默认为None，表示树的生长过程中对深度不做任何限制 
* min_samples_split:用于指定根节点或中间节点能够继续分割的最小样本量，默认为2 
* min_samples_leaf:用于指定叶节点的最小样本量，默认为1
* max_leaf_nodes:用于指定最大的叶节点个数，默认为None，表示对叶节点个数不做任何限制 
* class_weight:用于指定因变量中类别之间的权重，默认为None，表示每个类别的权重都相等;如果为balanced，则表示类别权重与原始样本中类别的比例成反比;还可以通过字典传递类别之间的权重差异，其形式为{class_label:weight}


### 随机森林模型介绍
* 利用Bootstrp抽样法，从原始数据集合中生成k个数据集，并且每个数据集都含有N个观测和P个自变量；
* 针对每一个数据集，构造一棵CART决策树，在构建子树的过程中，并没有将所有自变量用作节点字段的选择，而是随机选择p个字段；
* 让每一棵决策树尽可能地充分生长，使得树中的每个节点尽可能“纯净”，即随机森林中的每一棵子树都不需要剪枝；
* 针对k棵CART树的随机森林，对分类问题利用投票法，将最高得分的类别用于最终的判断结果；对回归问题利用均值法，将其用作预测样本的最终结果。

### 随机森林模型函数说明

```python
RandomForestClassifier(n_estimators=10, criterion='gini', max_depth=None, min_samples_split=2, min_samples_leaf=1, max_leaf_nodes=None, bootstrap=True, class_weight=None)
```
* n_estimators:用于指定随机森林所包含的决策树个数 
* criterion:用于指定每棵决策树节点的分割字段所使用的度量标准，用于分类的随机森林，默认的 criterion值为'gini'; 用于回归的随机森林，默认的criterion值为'mse' 
* max_depth:用于指定每棵决策树的最大深度，默认不限制树的生长深度 
* min_samples_split:用于指定每棵决策树根节点或中间节点能够继续分割的最小样本量，默认为2
* min_samples_leaf:用于指定每棵决策树叶节点的最小样本量，默认为1 
* max_leaf_nodes:用于指定每棵决策树最大的叶节点个数，默认为None，表示对叶节点个数不做任 何限制 
* bootstrap:bool类型参数，是否对原始数据集进行bootstrap抽样，用于子树的构建，默认为True 
* class_weight:用于指定因变量中类别之间的权重，默认为None，表示每个类别的权重都相等

## 代码实操

### 导入数据

```python
# 导入第三方模块
import pandas as pd
# 读入数据
Titanic = pd.read_csv(r'Titanic.csv')
Titanic.head()
```

### 数据预处理

```python
# 删除无意义的变量，并检查剩余自字是否含有缺失值
Titanic.drop(['PassengerId','Name','Ticket','Cabin'], axis = 1, inplace = True)
Titanic.isnull().sum(axis = 0)

# 对Sex分组，用各组乘客的平均年龄填充各组中的缺失年龄
fillna_Titanic = []
for i in Titanic.Sex.unique():
    update = Titanic.loc[Titanic.Sex == i,].fillna(value = {'Age': Titanic.Age[Titanic.Sex == i].mean()})
    fillna_Titanic.append(update)
Titanic = pd.concat(fillna_Titanic)

# 使用Embarked变量的众数填充缺失值
Titanic.fillna(value = {'Embarked':Titanic.Embarked.mode()[0]}, inplace=True)
Titanic.head()

# 将数值型的Pclass转换为类别型，否则无法对其哑变量处理
Titanic.Pclass = Titanic.Pclass.astype('category')
# 哑变量处理
dummy = pd.get_dummies(Titanic[['Sex','Embarked','Pclass']])
# 水平合并Titanic数据集和哑变量的数据集
Titanic = pd.concat([Titanic,dummy], axis = 1)
# 删除原始的Sex、Embarked和Pclass变量
Titanic.drop(['Sex','Embarked','Pclass'], inplace=True, axis = 1)
Titanic.head()
```

### 设置训练集和测试集

```python
# 导入第三方包
from sklearn import model_selection
# 取出所有自变量名称
predictors = Titanic.columns[1:]
# 将数据集拆分为训练集和测试集，且测试集的比例为25%
X_train, X_test, y_train, y_test = model_selection.train_test_split(Titanic[predictors], Titanic.Survived, test_size = 0.25, random_state = 1234)
```

### 构建决策树

```python
# 预设各参数的不同选项值
max_depth = [2,3,4,5,6]
min_samples_split = [2,4,6,8]
min_samples_leaf = [2,4,8,10,12]
# 将各参数值以字典形式组织起来
parameters = {'max_depth':max_depth, 'min_samples_split':min_samples_split, 'min_samples_leaf':min_samples_leaf} 
# 网格搜索法，测试不同的参数值
grid_dtcateg = GridSearchCV(estimator = tree.DecisionTreeClassifier(), param_grid = parameters, cv=10) # 模型拟合
grid_dtcateg.fit(X_train, y_train)
# 返回最佳组合的参数值
grid_dtcateg.best_params
```

out:

{'max_depth': 3, 'min_samples_leaf': 4, 'min_samples_split': 2}


```python
# 构建分类决策树
CART_Class = tree.DecisionTreeClassifier(max_depth=3, min_samples_leaf=4, min_samples_split=2) # 模型拟合
decision_tree = CART_Class.fit(X_train, y_train)
# 模型在测试集上的预测
pred = CART_Class.predict(X_test)
# 模型的准确率
print('模型在测试集的预测准确率:\n',metrics.accuracy_score(y_test, pred)) print('模型在训练集的预测准确率:\n',
metrics.accuracy_score(y_train, CART_Class.predict(X_train)))
```

### 构建随机森林模型

```python
# 导入第三方包
from sklearn import metrics
from sklearn import ensemble
# 构建随机森林
RF_class = ensemble.RandomForestClassifier(n_estimators=200, random_state=1234)
# 随机森林的拟合
RF_class.fit(X_train, y_train)
# 模型在测试集上的预测
RFclass_pred = RF_class.predict(X_test)
# 模型的准确率
print('模型在测试集的预测准确率：\n',metrics.accuracy_score(y_test, RFclass_pred))
```

### 绘制ROC

```python
import matplotlib.pyplot as plt
# 计算绘图数据
y_score = RF_class.predict_proba(X_test)[:,1]
fpr,tpr,threshold = metrics.roc_curve(y_test, y_score)
roc_auc = metrics.auc(fpr,tpr)
# 绘图
plt.stackplot(fpr, tpr, color='steelblue', alpha = 0.5, edgecolor = 'black')
plt.plot(fpr, tpr, color='black', lw = 1)
plt.plot([0,1],[0,1], color = 'red', linestyle = '--')
plt.text(0.5,0.3,'ROC curve (area = %0.2f)' % roc_auc)
plt.xlabel('1-Specificity')
plt.ylabel('Sensitivity')
plt.show()
```

### 变量重要程度

```python
# 变量的重要性程度值
importance = RF_class.feature_importances_
# 构建含序列用于绘图
Impt_Series = pd.Series(importance, index = X_train.columns)
# 对序列排序绘图
Impt_Series.sort_values(ascending = True).plot('barh')
plt.show()
```

## Refernce

[决策树（分类树/回归树）](https://blog.csdn.net/weixin_36586536/article/details/80468426)