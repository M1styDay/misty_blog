---
title: Resume Framework (1)
author: "Misty"
tags: ["Study map","Job"]
categories: ["Study Map"]
date: 2021-06-19
---



# 技术知识


## 统计学
### 描述性统计
TBC
### 假设检验
TBC
### 概率论
TBC
### AB Test
TBC






## 分析工具

### Sql

#### sql基础知识

[sql基础知识](https://www.m1sty.com/2020/database_sql_notes/)

#### sql笔试题

[SQL面试必会50题](https://www.m1sty.com/2020/database_sql_50/)

```sql
# 查询每门功成绩最好的前两名
SELECT c_id, 
max(case when rank1 = 1 then s_score else null end ) as '第一',
max(case when rank1 = 2 then s_score else null end ) as '第二'
FROM (SELECT score.s_id, student.s_name, score.c_id, score.s_score, row_number() over(partition by c_id order by s_score DESC) rank1
FROM score 
INNER JOIN student
ON score.s_id = student.s_id) a
WHERE rank1 in (1,2)
Group by c_id;
```

```sql
# 查询选修“张三”老师所授课程的学生中成绩最高的学生姓名及其成绩
select score.s_id, s_name, s_score
from score
inner join student
on score.s_id = student.s_id
inner join course
on score.c_id = course.c_id
inner join teacher
on teacher.t_id = course.t_id
where t_name = '张三'
order by s_score desc
limit 1 offset 1
```

### Hadoop
TBC


### Python

* numpy
* pandas
* sklearn
* statsmodel
* matplotilb
* seaborn


### R Language
TBC






## 机器学习

### 线性回归模型

[线性回归模型](https://www.m1sty.com/2021/dm_regression_5_practise_linear-regression/)


### Ridge回归模型和Lasso回归模型

[Ridge回归模型和Lasso回归模型](https://www.m1sty.com/2021/dm_regression_5_practise_ridge-regression-and-lasso-regression/)

* 线性回归模型的短板
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408191356.png)

* Ridge回归模型：为解决多元线性回归模型中可能存在的不可逆问题，统计学家提出了岭回归模型。该模型解决问题的思路就是在线性回归模型的目标函数之上增加l2正则项（也称为惩罚项）。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408192153.png)

* 岭回归模型解决线性回归模型中矩阵X’X不可逆的办法是添加l2正则的惩罚项,但缺陷在于始终保留建模时的所有变量,无法降低模型的复杂度。对于此, Lasso回归采用了l1正则的惩罚项。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408194118.png)

* Lasso回归和岭回归的同和异：
    * 相同： 都可以用来解决标准线性回归的过拟合问题。 
    * 不同： lasso 可以用来做 feature selection，而 ridge 不行。或者说，lasso 更容易使得权重变为 0，而 ridge 更容易使得权重接近 0。 从贝叶斯角度看，lasso（L1 正则）等价于参数 w 的先验概率分布满足拉普拉斯分布，而 ridge（L2 正则）等价于参数 w 的先验概率分布满足高斯分布
    * L1惩罚项的目的是使权重绝对值最小化
    * L2惩罚项的目的是使权重的平方最小化

* 代码思路
    * 构建Lambda->交叉验证->模型拟合->最佳Lambda->基于最佳的Lambda值建模->返回岭回归系数->预测->验证

    * 交叉验证
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408192933.png)


### 逻辑回归

[逻辑回归](https://www.m1sty.com/2021/dm_regression_5_practise_logistic-refression/)

[逻辑回归_ICOM6044](https://www.m1sty.com/2021/dsfb_0_overview/#53-predictive-modeling-using-logistic-regression---596)



### 随机森林模型

[随机森林模型](https://www.m1sty.com/2021/dm_decistion-trees_5_practise/#%E9%9A%8F%E6%9C%BA%E6%A3%AE%E6%9E%97%E7%9A%84%E6%80%9D%E6%83%B3)

* 决策树节点字段的选择和阈值的选择（生成算法）
    * 信息增益（ID3）
    * 信息增益率（C4.5）
    * 基尼指数（CART）
* 分类树和回归树
    * 分类树使用信息增益或增益比率来划分节点；每个节点样本的类别情况投票决定测试样本的类别。
    * 回归树使用最大均方差划分节点；每个节点样本的均值作为测试样本的回归预测值。
* 随机森林模型介绍
    * 利用Bootstrp抽样法，从原始数据集合中生成k个数据集，并且每个数据集都含有N个观测和P个自变量；
    * 针对每一个数据集，构造一棵CART决策树，在构建子树的过程中，并没有将所有自变量用作节点字段的选择，而是随机选择p个字段；
    * 让每一棵决策树尽可能地充分生长，使得树中的每个节点尽可能“纯净”，即随机森林中的每一棵子树都不需要剪枝；
    * 针对k棵CART树的随机森林，对分类问题利用投票法，将最高得分的类别用于最终的判断结果；对回归问题利用均值法，将其用作预测样本的最终结果。


### 聚类分析

[聚类分析](https://www.m1sty.com/2021/dm_clusterings_5_practise_k-means/)

* k-means
    * K-means聚类算法利用距离远近的思想将目标数据为制定的k个簇，进而使样本呈现簇内差异小，簇间差异大的特征。（簇内样本的离差平方和之和达到最小）
    * 最佳k选择：拐点法。在不同的k值下计算簇内利差平方和，然后通过可视化的方法找到“拐点”所对应的k值。当折线图中的斜率由大突然变小时，并且之后的斜率变化缓慢，则认为突然变化的点就是寻找的目标点，因为继续随着簇数k的增加，聚类效果不再有大的变化。
* DBSCAN
    * Kmeans聚类存在两个致命缺点，一是聚类效果容易受到异常样本点的影响;二是该算法无法准确地将非球形样本进行合理的聚类。
    * 基于密度的聚类则可以解决非球形簇的问题，“密度”可以理解为样本点的紧密程度，如果在指定的半径领域内，实际样本量超过给定的最小样本量阈值，则认为是密度高的对象，就可以聚成一个簇。
* 层次聚类
    * 层次聚类更适合小样本；K-Means更适合大样本。
* K-means++


### 朴素贝叶斯

[朴素贝叶斯模型](https://www.m1sty.com/2021/dm_naive-bayes-class_5_practise/)

### K近邻模型

[K近邻模型](https://www.m1sty.com/2021/dm_knn_5_practise/)

### SVM模型

[SVM模型](https://www.m1sty.com/2021/dm_svm_4_practise/)


### 常见分类算法

* 朴素贝叶斯分类器（Naive Bayes）
* 支持向量机（SVM）
* K-最邻近（K-Nearest Neighbor）
* 逻辑斯谛回归（Logistic regression）
* 决策树（Decision trees）
* 神经网络（Neural networks）
* 主题模型（LDA）



### 常见回归算法的原理和优劣对比
* [几种常见回归算法的原理和优劣对比](https://www.zhoulujun.cn/html/theory/algorithm/RegressionAlgorithm/8272.html)



### 对比建模结果的方式（ROC/混淆矩阵/均方误差/拟合优度）

* ROC 
    * ROC的全称是Receiver Operating Characteristic Curve，中文名字叫“受试者工作特征曲线”，顾名思义，其主要的分析方法就是画这条特征曲线。
    * 该曲线的横坐标为假阳性率（False Positive Rate, FPR），N是真实负样本的个数，FP是N个负样本中被分类器预测为正样本的个数。
    * 纵坐标为真阳性率（True Positive Rate, TPR），P是真实正样本的个数，TP是P个正样本中被分类器预测为正样本的个数。
    * AUC（Area under roc Curve）面积，就是指ROC曲线下的面积大小，而计算AUC值只需要沿着ROC横轴做积分就可以了。真实场景中ROC曲线一般都会在y=x这条直线的上方，所以AUC的取值一般在0.5~1之间。AUC的值越大，说明该模型的性能越好。

* [混淆矩阵](https://www.m1sty.com/2021/dm_regression_5_practise_logistic-refression/#%E5%B8%B8%E8%A7%81%E7%9A%84%E6%A8%A1%E5%9E%8B%E8%AF%84%E4%BC%B0%E6%96%B9%E6%B3%95)

* 均方误差
    * 均方误差：是预测值与真实值之差的平方和的平均值（衡量预测结果）
    * 均方差/标准差：是方差的算术平方根。而方差是样本实际值与实际值的总体平均值之差的平方和的平均值。（衡量数据集的离散程度）

* 拟合优度
    * 回归分析中用来检验样本数据点聚集在回归线周围的密集程度，用于评价回归方程对样本观测值的拟合程度。
    * 过拟合定义：模型在训练集上的表现很好，但在测试集和新数据上的表现很差。
    * 产生过拟合的原因：
        * 模型复杂度过高，参数过多
        * 训练数据比较小
        * 训练集和测试集分布不一致（样本里面的噪声数据干扰过大，导致模型过分记住了噪声特征，反而忽略了真实的输入输出特征/训练集和测试集特征分布不一样，如果训练集和测试集使用了不同类型的数据集会出现这种情况）
    * 过拟合的解决办法：
        * 降低模型复杂度
        * 增加更多数据
        * 数据增强（使用数据增强可以生成多幅相似图像。这可以帮助我们增加数据集规模从而减少过拟合。因为随着数据量的增加，模型无法过拟合所有样本，因此不得不进行泛化。计算机视觉领域通常的做法有：翻转、平移、旋转、缩放、改变亮度、添加噪声等等，音频数据增强方法有：增加噪音、增加混响、时移、改变音调和时间拉伸）
        * 正则化
            * L1惩罚项的目的是使权重绝对值最小化
            * L2惩罚项的目的是使权重的平方最小化
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210409123032.png)


### 分类、回归分析、时间序列分析、主成分分析等分析方法，应用场景和方法
* 分类
    * 分类明确，数目和特征都明确
    * 业务场景：是否会购买某样东西
    * 常见算法：逻辑回归、SVM、决策树
* 回归
    * 我和你有没有关系？有关系的话是什么关系？关系有多深？
    * 业务场景：优惠券的优惠力度对促活跃的效果/运营推广中，是不是花的钱越多，买的流量越大，品类越丰富，用户活跃越高，用户留存越高/那么，多到什么程度、大到什么程度、丰富到什么程度，用户的活跃最高，留存最高
    * 常见算法：线性回归（什么是线性？导数为常数）
* 时间序列
    * 核心逻辑：江山易改本性难移
    * 对不同周期的数据进行加权，离现在越近的数据权重越高，越远权重越低。
    * 周期性、季节性
    * 回归预测和时间序列预测的区别：回归是是自变量对因变量的预测，自变量可以是任何数据（包括时间），但无法做季节性预测；时间序列只考量时间对的因变量的影响，有季节性。
* 主成分分析
    * 主成分分析的主要目的是用较少的变量去解释原来数据中的大部分信息，将许多相关性较高的变量转化为彼此相互独立和不相干的变量。除了调用PCA(n_components=k).fit_transform(data)一股脑的将数据进行压缩降维，主成分分析还能用于很多地方。
    * 对指标进行建模时的客观赋权
    * 构造新特征
    * 进行特征选项 / 对特征重要性进行排序
    * 异常数据检测
    * 用户生命周期价值


## 多重共线性
* [多重共线性的解决方法](https://zhuanlan.zhihu.com/p/72722146)
