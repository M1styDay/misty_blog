---
title: Regression：Ridge Regression and Lasson Regression
author: "Misty"
tags: ["Regression","Model"]
categories: ["Data Mining"]
date: 2021-01-03
---

## 线性回归模型的短板

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408191356.png)

### 当列数比行数多

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408191539.png)

### 当列之间存在多重共线性

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408191615.png)

## 岭回归模型

为解决多元线性回归模型中可能存在的不可逆问题，统计学家提出了岭回归模型。该模型解决问题的思路就是在线性回归模型的目标函数之上增加l2正则项（也称为惩罚项）。

### 表达式

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408192153.png)

### 系数求解

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408192221.png)

### 凸优化的等价命题

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408192739.png)

### 系数求解的几何意义

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408192828.png)

### 交叉验证法

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408192933.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408192957.png)


## Lasso模型

岭回归模型解决线性回归模型中矩阵X'X不可逆的办法是添加l2正则的惩罚项,但缺陷在于始终保留建模时的所有变量,无法降低模型的复杂度。对于 此, Lasso回归采用了l1正则的惩罚项。

### 表达式

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408194118.png)

### 凸优化的等价命题

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408194150.png)

### 系数求解的几何意义

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408194237.png)


### 交叉验证法

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408194304.png)


## 实操

```python
# 导入第三方模块
import pandas as pd
import numpy as np
from sklearn import model_selection
from sklearn.linear_model import Ridge,RidgeCV
import matplotlib.pyplot as plt

# 读取糖尿病数据集
diabetes = pd.read_excel(r'diabetes.xlsx')
# 构造自变量（剔除患者性别、年龄和因变量）
predictors = diabetes.columns[2:-1]
# 将数据集拆分为训练集和测试集
X_train, X_test, y_train, y_test = model_selection.train_test_split(diabetes[predictors], diabetes['Y'], test_size = 0.2, random_state = 1234 )
```

### 多元线性回归

```python
# 导入第三方模块
from statsmodels import api as sms
# 为自变量X添加常数列1，用于拟合截距项
X_train2 = sms.add_constant(X_train)
X_test2 = sms.add_constant(X_test)

# 构建多元线性回归模型
linear = sms.OLS(y_train, X_train2).fit()
# 返回线性回归模型的系数
linear.params

# 模型的预测
linear_predict = linear.predict(X_test2)
# 预测效果验证
RMSE = np.sqrt(mean_squared_error(y_test,linear_predict))
RMSE
```



### 岭回归

```python
# 构造不同的Lambda值
Lambdas = np.logspace(-5, 2, 200)
# 岭回归模型的交叉验证
# 设置交叉验证的参数，对于每一个Lambda值，都执行10重交叉验证
ridge_cv = RidgeCV(alphas = Lambdas, normalize=True, scoring='neg_mean_squared_error', cv = 10)
# 模型拟合
ridge_cv.fit(X_train, y_train)
# 返回最佳的lambda值
ridge_best_Lambda = ridge_cv.alpha_
ridge_best_Lambda
```

```python
# 导入第三方包中的函数
from sklearn.metrics import mean_squared_error
# 基于最佳的Lambda值建模
ridge = Ridge(alpha = ridge_best_Lambda, normalize=True)
ridge.fit(X_train, y_train)
# 返回岭回归系数
pd.Series(index = ['Intercept'] + X_train.columns.tolist(),data = [ridge.intercept_] + ridge.coef_.tolist())
# 预测
ridge_predict = ridge.predict(X_test)
# 预测效果验证
RMSE = np.sqrt(mean_squared_error(y_test,ridge_predict))
RMSE
```

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408202121.png)


### Lasso回归

```python
# 构造不同的Lambda值
Lambdas = np.logspace(-5, 2, 200)

# 导入第三方模块中的函数
from sklearn.linear_model import Lasso,LassoCV
# LASSO回归模型的交叉验证
lasso_cv = LassoCV(alphas = Lambdas, normalize=True, cv = 10, max_iter=10000)
lasso_cv.fit(X_train, y_train)
# 输出最佳的lambda值
lasso_best_alpha = lasso_cv.alpha_
lasso_best_alpha
```

```python
# 基于最佳的lambda值建模
lasso = Lasso(alpha = lasso_best_alpha, normalize=True, max_iter=10000)
lasso.fit(X_train, y_train)
# 返回LASSO回归的系数
pd.Series(index = ['Intercept'] + X_train.columns.tolist(),data = [lasso.intercept_] + lasso.coef_.tolist())

# 预测
lasso_predict = lasso.predict(X_test)
# 预测效果验证
RMSE = np.sqrt(mean_squared_error(y_test,lasso_predict))
RMSE
```

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210408202201.png)