---
title: Decision Trees：Project
author: "Misty"
tags: ["Decistion Trees","Model"]
categories: ["Data Mining"]
date: 2021-04-05
---

# 随机森林模型项目代码


## 建模版

### 导入数据

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as nps  
from scipy import stats
from sklearn import metrics

# 导入Excel文档
data=pd.read_excel('D:\\Britney\\项目1\\K数据.xlsx')
```

### 数据预处理

```python
# 去除为0的行
a=data[data['大货唛架 YY']==0].index
data1=data.drop(a,axis=0)
data1[data1['大货唛架 YY'].isin([0])]

y1=data1['大货唛架利用率%']
y2=data1['大货唛架 YY']

#如果缺失率达到40%就可以去除该因子
d1=data1.isnull().sum()/data1.shape[0]
#a=d1>0.5
a1=pd.DataFrame(d1)
print(a1[a1[0]>0.4])

#去掉缺失率过大的因子
data2=data1.drop(['后整方式','循环尺寸标准_经向(Inch)','循环尺寸标准_纬向(Inch)'],axis=1)

# 类型变量集合
quality=[attr for attr in data2.columns if data2.dtypes[attr] == 'object']  
 
# 类型变量缺失值补全
for c in quality:  
    data2[c] = data2[c].astype('category')
    if data2[c].isnull().any():                                            
        data2[c] = data2[c].cat.add_categories(['MISSING'])
        data2[c] = data2[c].fillna('MISSING')

 
#将数值型变量的缺失值用平均值代替
quantity=['缩水率标准_L%','缩水率标准_W%']
for x in quantity:               #mean() 求平均值
    mean_value = data2[x].mean()
    data2[x] = data2[x].replace(np.NaN, mean_value)

#将类型变量编码
from category_encoders import *
YY_test = data2['大货唛架利用率%']
XX_test = data2['大货唛架 YY']
X=data2.drop(['大货唛架利用率%','大货唛架 YY'],axis=1)
enc = OrdinalEncoder(cols=(['Factory', 'GMT Color Code','Customer Code ', 'Gender', 'Prod Category', 'Finishing & Wash','Quality Code', 'Season Code', 'Style No', '款式', '袖形描述-以长/短为主', '袋形描述-以单/双为主', '介英描述', '领形描述-MI', 'Fab Pattern', '裁向', '对条/格要求_筒', '对条/格要求_钮子', '对条/格要求_纳膊','对条/格要求_口袋', '对条/格要求_前幅', '对条/格要求_后幅', '对条/格要求_侧骨', '对条/格要求_袖','对条/格要求_上级领', '对条/格要求_介英', '对条/格要求_袖侧', '对条/格要求_担干', '成衣花型', 'COMBO', '布种', '成分', 'N纱类', 'N布的花型', 'N纱支','工艺布封', '成衣尺码类别','纸样尺寸单位', '尺码类别', '尺码范围1', '后中衫长', '胸围', '夹圈', '袖长', '臂围', '坐围', '裤长','尺码范围2', '订单数比率'])).fit(X, y2)
ht=enc.transform(X)
ht.head()

#将变量转为数值型变量
ht['缩水率标准_L%']=ht['缩水率标准_L%'].astype('int')
ht['缩水率标准_W%']=ht['缩水率标准_W%'].astype('int')
```

### 构建随机森林模型

```python
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score
from sklearn.ensemble import RandomForestRegressor

#设置训练集
X2=ht.drop([],axis=1)
X_train, X_test, Y_train, Y_test = train_test_split(X2, y1, test_size=0.3,random_state=42)

#使用随机森林建模
model =RandomForestRegressor()
model.fit(X_train,Y_train)
predicted = model.predict(X2)
```


### 画图/拟合优度/均方误差

```python
#这是画图，画预测值和原值两者 
plt.scatter(range(X2.shape[0]), YY_test, marker='x')
plt.plot(range(X2.shape[0]), predicted, c='r')
plt.show()

#拟合优度检验
print(r2_score(YY_test,predicted))

#均方误差
rmse = np.sqrt(metrics.mean_squared_error(YY_test, predicted))
print(rmse)
```

### 输出结果

```python
#输出预测结果
test=pd.DataFrame(YY_test)
test.to_excel('D:\\Britney\\项目1\\预测大货唛架利用率te.xlsx')
predicted3=pd.DataFrame(predicted)
predicted3.to_excel('D:\\Britney\\项目1\\预测大货唛架利用率yc.xlsx')
```


## 预测版


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as nps  
from scipy import stats
from sklearn import metrics

# 导入Excel文档
data=pd.read_excel('D:\\Britney\\项目2\\K数据.xlsx')
# 去除为0的行
a=data[data['大货唛架 YY']==0].index
data1=data.drop(a,axis=0)
data1[data1['大货唛架 YY'].isin([0])]

y1=data1['大货唛架利用率%']
y2=data1['大货唛架 YY']

#如果缺失率达到40%就可以去除该因子
d1=data1.isnull().sum()/data1.shape[0]
#a=d1>0.5
a1=pd.DataFrame(d1)
print(a1[a1[0]>0.4])

#去掉缺失率过大的因子
data2=data1.drop(['后整方式','循环尺寸标准_经向(Inch)','循环尺寸标准_纬向(Inch)'],axis=1)

# 类型变量集合
quality=[attr for attr in data2.columns if data2.dtypes[attr] == 'object']  
 
# 类型变量缺失值补全
for c in quality:  
    data2[c] = data2[c].astype('category')
    if data2[c].isnull().any():                                            
        data2[c] = data2[c].cat.add_categories(['MISSING'])
        data2[c] = data2[c].fillna('MISSING')

#将数值型变量的缺失值用平均值代替
quantity=['缩水率标准_L%','缩水率标准_W%']
for x in quantity:               #mean() 求平均值
    mean_value = data2[x].mean()
    data2[x] = data2[x].replace(np.NaN, mean_value)

 
#将类型变量编码
from category_encoders import *
X=data2.drop(['大货唛架利用率%','大货唛架 YY'],axis=1)
enc = OrdinalEncoder(cols=(['Factory', 'GMT Color Code','Customer Code ', 'Gender', 'Prod Category', 'Finishing & Wash','Quality Code', 'Season Code', 'Style No', '款式', '袖形描述-以长/短为主', '袋形描述-以单/双为主', '介英描述', '领形描述-MI', 'Fab Pattern', '裁向', '对条/格要求_筒', '对条/格要求_钮子', '对条/格要求_纳膊','对条/格要求_口袋', '对条/格要求_前幅', '对条/格要求_后幅', '对条/格要求_侧骨', '对条/格要求_袖','对条/格要求_上级领', '对条/格要求_介英', '对条/格要求_袖侧', '对条/格要求_担干', '成衣花型', 'COMBO', '布种', '成分', 'N纱类', 'N布的花型', 'N纱支','工艺布封', '成衣尺码类别','纸样尺寸单位', '尺码类别', '尺码范围1', '后中衫长', '胸围', '夹圈', '袖长', '臂围', '坐围', '裤长','尺码范围2', '订单数比率'])).fit(X, y2)
ht=enc.transform(X)
ht.head()

#将变量转为数值型变量
ht['缩水率标准_L%']=ht['缩水率标准_L%'].astype('int')
ht['缩水率标准_W%']=ht['缩水率标准_W%'].astype('int')

 
#预测大货唛架MU
#设置训练集
from sklearn.model_selection import train_test_split
X2=ht.drop(['布种', '成分', 'N纱类', 'N布的花型', 'N纱支','缩水率标准_L%','缩水率标准_W%'],axis=1)

#导入需要预测的数据
test_data=pd.read_excel('D:\\Britney\\项目2\\K数据new.xlsx')
test_data=test_data.drop(['后整方式','循环尺寸标准_经向(Inch)','循环尺寸标准_纬向(Inch)'],axis=1)
test_data=test_data.drop(['大货唛架利用率%','大货唛架 YY'],axis=1)
test_data=enc.transform(test_data)
test_data.head()  
test_data=test_data.drop(['布种', '成分', 'N纱类', 'N布的花型', 'N纱支','缩水率标准_L%','缩水率标准_W%'],axis=1)

#训练，y1和y2看需要修改
X_train, X_test, Y_train, Y_test = train_test_split(X2, y1, test_size=0.3,random_state=42)
from sklearn.metrics import r2_score
from sklearn.ensemble import RandomForestRegressor

#使用随机森林建模
model =RandomForestRegressor()
model.fit(X_train,Y_train)

predicted = model.predict(X_test)
answer1 = model.predict(test_data)

#这是画图，画预测值和原值两者 
#plt.scatter(range(X_test.shape[0]), Y_test, marker='x')
plt.scatter(range(X_test.shape[0]), Y_test, marker='x')
#plt.plot(range(X_test.shape[0]), predicted, c='r')
plt.plot(range(X_test.shape[0]), predicted, c='r')
plt.show()

#拟合优度检验
print(r2_score(Y_test,predicted))

#均方误差
rmse = np.sqrt(metrics.mean_squared_error(Y_test, predicted))
print(rmse)

#输出预测结果
test=pd.DataFrame(Y_test)
test.to_excel('D:\\Britney\\项目2\\针织大货唛架MUte.xlsx')
predicted1=pd.DataFrame(predicted)
predicted1.to_excel('D:\\Britney\\项目2\\针织大货唛架MUyc.xlsx')
output1=pd.DataFrame(answer1)
output1.to_excel('D:\\Britney\\项目2\\针织大货唛架MUan.xlsx')
```


