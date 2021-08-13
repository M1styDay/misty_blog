---
title: Regression：Linear Regression
author: "Misty"
tags: ["Regression","Model"]
categories: ["Data Mining"]
date: 2021-01-02
---

# 线性回归

## 一元线性回归

### 相关分析

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402115124.png)


### 一元线性回归模型

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402115521.png)

* 模型中的x称为自变量，y称为因变量;
* a为模型的截距项，b为模型的斜率项，ε为模型的误差项; 
* 误差项ε的存在主要是为了平衡等号两边的值，通常被称为模型 无法解释的部分;
* 如果拟合线能够精确地捕捉到每一个点(即所有散点全部落在拟合线上)，那么对应的误差项ε应该为0;
* 所以，模型拟合的越好，则误差项ε应该越小。进而可以理解为: **求解参数的问题便是求解误差平方和最小的问题**。

### 参数a和b求解

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402115904.png)

* J(a,b)为目标函数，需求解该函数的最小值；
* 求解方法便是计算目标函数关于参数a和b的两个偏导数，最终令偏倒数为0即可。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402120053.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402120126.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402120149.png)

### 模型的应用

```pyton
# 导入第三方模块
import statsmodels.api as sm
sm.ols(formula, data, subset=None, drop_cols=None)
```
* formula:以字符串的形式指定线性回归模型的公式，如'y~x'就表示简单线性回归模型 
* data:指定建模的数据集 
* subset:通过bool类型的数组对象，获取data的子集用于建模 
* drop_cols:指定需要从data中删除的变量

```python
# 导入第三方模块
import pandas as pd
import statsmodels.api as sm

# 导入数据
income = pd.read_csv('Salary_Data.csv')
# 利用收入数据集，构建回归模型
fit = sm.formula.ols('Salary ~ YearsExperience', data = income).fit() 
# 返回模型的参数值
fit.params
```
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402131831.png)

```python
# 相关系数
income.columns
income.Salary.corr(income.YearsExperience)
```


## 多元线性回归

### 定义

* 对于一元线性回归模型来说，其反映的是单个自变量对因变量的影响，然而实际情况中，影
响因变量的自变量往往不止一个，从而需要将一元线性回归模型扩展到多元线性回归模型。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402121247.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402121316.png)

### 参数求解

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402121356.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402121412.png)

### 模型的应用

* 数据集包含5个变量，分别是产品的研发成本、管理成本、市场营销成本、销售市场和销 售利润。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402121459.png)

```python
# 导入模块
from sklearn import model_selection

# 导入数据
Profit = pd.read_excel(r'Predict to Profit.xlsx')
# 将数据集拆分为训练集和测试集
train, test = model_selection.train_test_split(Profit, test_size = 0.2, random_state=1234)
# 根据train数据集建模
model = sm.formula.ols('Profit ~ RD_Spend+Administration+Marketing_Spend+C(State)', data = train).fit()

print('模型的偏回归系数分别为：\n', model.params)

# 删除test数据集中的Profit变量，用剩下的自变量进行预测
test_X = test.drop(labels = 'Profit', axis = 1)
pred = model.predict(exog = test_X)

print('对比预测值和实际值的差异：\n',pd.DataFrame({'Prediction':pred,'Real':test.Profit}))
```

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402132147.png)


```python
# 生成由State变量衍生的哑变量
dummies = pd.get_dummies(Profit.State)
# 将哑变量与原始数据集水平合并
Profit_New = pd.concat([Profit,dummies], axis = 1)
# 删除State变量和California变量（因为State变量已被分解为哑变量，New York变量需要作为参照组）
Profit_New.drop(labels = ['State','New York'], axis = 1, inplace = True)

# 拆分数据集Profit_New
train, test = model_selection.train_test_split(Profit_New, test_size = 0.2, random_state=1234)

# 建模
model2 = sm.formula.ols('Profit~RD_Spend+Administration+Marketing_Spend+Florida+California', data = train).fit()
print('模型的偏回归系数分别为：\n', model2.params)
```

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402132557.png)

```python
#相关系数
Profit.drop('State',axis=1).corrwith(Profit['Profit'])
Profit.drop('State',axis=1).corr()
```



## 线性回归模型的假设检验

### 模型的F检验

* 提出问题的原假设和备择假设 
* 在原假设的条件下，构造统计量F
* 根据样本信息，计算统计量的值 
* 对比统计量的值和理论F分布的值，当统计量值超过理论值时，拒绝原假设，否则接受原假设

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402121916.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402121956.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402122019.png)

### 参数的t检验

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402122052.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210402122126.png)


## Reference

[统计学常用概念：T检验、F检验、卡方检验、P值、自由度](http://cblog.csdn.net/mydear_11000/article/details/51576564)

[一文详解t检验](https://zhuanlan.zhihu.com/p/138711532)

[t检验](https://www.zhihu.com/question/30753175)
    