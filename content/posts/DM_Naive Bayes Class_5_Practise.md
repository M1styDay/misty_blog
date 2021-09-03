---
title: Naive Bayes Class：Practise
author: "Misty"
tags: ["Naive Bayes Class","Model"]
categories: ["Data Mining"]
date: 2021-04-16
---

# 朴素贝叶斯模型

## 贝叶斯模型的思想和理论

### 模型思想

该分类器的实现思想非常简单，即通过已知类别的训练数据集，计算样本的先验概率，然后利用贝叶斯概率公式测算未知类别样本属于某个类别的后验概率，最终以最大后验概率所对应的类别作为样本的预测值。

### 模型理论

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416141024.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416142634.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416142734.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416142651.png)

## 常用的贝叶斯分类器

### 高斯贝叶斯分类器

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416142934.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416142952.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416143002.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416143011.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416143022.png)

### 多项式贝叶斯分类器

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416144214.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416144225.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416144234.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416144248.png)

### 伯努利贝叶斯分类器

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416144903.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416144926.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416144937.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416144946.png)


## 应用实战

### 高斯贝叶斯——皮肤识别

```python
# 导入第三方包
import pandas as pd
# 读入数据
skin = pd.read_excel(r'Skin_Segment.xlsx')
# 设置正例和负例
skin.y = skin.y.map({2:0,1:1})
skin.y.value_counts()
```

```python
# 导入第三方模块
from sklearn import model_selection
# 样本拆分
X_train,X_test,y_train,y_test = model_selection.train_test_split(skin.iloc[:,:3], skin.y, test_size = 0.25, random_state=1234)
```

```python
# 导入第三方模块
from sklearn import naive_bayes
# 调用高斯朴素贝叶斯分类器的“类”
gnb = naive_bayes.GaussianNB()
# 模型拟合
gnb.fit(X_train, y_train)
# 模型在测试数据集上的预测
gnb_pred = gnb.predict(X_test)
# 各类别的预测数量
pd.Series(gnb_pred).value_counts()
```

```python
# 导入第三方包
from sklearn import metrics
import matplotlib.pyplot as plt
import seaborn as sns
# 构建混淆矩阵
cm = pd.crosstab(gnb_pred,y_test)
# 绘制混淆矩阵图
sns.heatmap(cm, annot = True, cmap = 'GnBu', fmt = 'd')
# 去除x轴和y轴标签
plt.xlabel('Real')
plt.ylabel('Predict')
# 显示图形
plt.show()

print('模型的准确率为：\n',metrics.accuracy_score(y_test, gnb_pred))
print('模型的评估报告：\n',metrics.classification_report(y_test, gnb_pred))
```

```python
# 计算正例的预测概率，用于生成ROC曲线的数据
y_score = gnb.predict_proba(X_test)[:,1]
fpr,tpr,threshold = metrics.roc_curve(y_test, y_score)
# 计算AUC的值
roc_auc = metrics.auc(fpr,tpr)

# 绘制面积图
plt.stackplot(fpr, tpr, color='steelblue', alpha = 0.5, edgecolor = 'black')
# 添加边际线
plt.plot(fpr, tpr, color='black', lw = 1)
# 添加对角线
plt.plot([0,1],[0,1], color = 'red', linestyle = '--')
# 添加文本信息
plt.text(0.5,0.3,'ROC curve (area = %0.2f)' % roc_auc)
# 添加x轴与y轴标签
plt.xlabel('1-Specificity')
plt.ylabel('Sensitivity')
# 显示图形
plt.show()
```


### 多项式贝叶斯——毒蘑菇识别
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416145417.png)

```python
# 导入第三方包
import pandas as pd
# 读取数据
mushrooms = pd.read_csv(r'mushrooms.csv')
# 数据的前5行
mushrooms.head()
```

```python
# 将字符型数据作因子化处理，将其转换为整数型数据
columns = mushrooms.columns[1:]
for column in columns:
    mushrooms[column] = pd.factorize(mushrooms[column])[0]
mushrooms.head()
```

```python
from sklearn import model_selection
# 将数据集拆分为训练集合测试集
Predictors = mushrooms.columns[1:]
X_train,X_test,y_train,y_test = model_selection.train_test_split(mushrooms[Predictors], mushrooms['type'], test_size = 0.25, random_state = 10)
```

```python
from sklearn import naive_bayes
from sklearn import metrics
import seaborn as sns
import matplotlib.pyplot as plt
# 构建多项式贝叶斯分类器的“类”
mnb = naive_bayes.MultinomialNB()
# 基于训练数据集的拟合
mnb.fit(X_train, y_train)
# 基于测试数据集的预测
mnb_pred = mnb.predict(X_test)
# 构建混淆矩阵
cm = pd.crosstab(mnb_pred,y_test)
# 绘制混淆矩阵图
sns.heatmap(cm, annot = True, cmap = 'GnBu', fmt = 'd')
# 去除x轴和y轴标签
plt.xlabel('Real')
plt.ylabel('Predict')
# 显示图形
plt.show()

# 模型的预测准确率
print('模型的准确率为：\n',metrics.accuracy_score(y_test, mnb_pred))
print('模型的评估报告：\n',metrics.classification_report(y_test, mnb_pred))
```

```python
from sklearn import metrics
# 计算正例的预测概率，用于生成ROC曲线的数据
y_score = mnb.predict_proba(X_test)[:,1]
fpr,tpr,threshold = metrics.roc_curve(y_test.map({'edible':0,'poisonous':1}), y_score)
# 计算AUC的值
roc_auc = metrics.auc(fpr,tpr)

# 绘制面积图
plt.stackplot(fpr, tpr, color='steelblue', alpha = 0.5, edgecolor = 'black')
# 添加边际线
plt.plot(fpr, tpr, color='black', lw = 1)
# 添加对角线
plt.plot([0,1],[0,1], color = 'red', linestyle = '--')
# 添加文本信息
plt.text(0.5,0.3,'ROC curve (area = %0.2f)' % roc_auc)
# 添加x轴与y轴标签
plt.xlabel('1-Specificity')
plt.ylabel('Sensitivity')
# 显示图形
plt.show()
```


### 伯努利贝叶斯——情感分析

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210416145338.png)


```python
import pandas as pd
# 读入评论数据
evaluation = pd.read_excel(r'Contents.xlsx',sheet_name=0)
# 查看数据前10行
evaluation.head(10)
```


```python
# 运用正则表达式，将评论中的数字和英文去除
evaluation.Content = evaluation.Content.str.replace('[0-9a-zA-Z]','')
evaluation.head()
```


```python
# 导入第三方包
import jieba

# 加载自定义词库
jieba.load_userdict(r'all_words.txt')

# 读入停止词
with open(r'mystopwords.txt', encoding='UTF-8') as words:
    stop_words = [i.strip() for i in words.readlines()]

# 构造切词的自定义函数，并在切词过程中删除停止词
def cut_word(sentence):
    words = [i for i in jieba.lcut(sentence) if i not in stop_words]
    # 切完的词用空格隔开
    result = ' '.join(words)
    return(result)
# 对评论内容进行批量切词
words = evaluation.Content.apply(cut_word)
# 前5行内容的切词效果
words[:5]
```


```python
# 导入第三方包
from sklearn.feature_extraction.text import CountVectorizer
# 计算每个词在各评论内容中的次数，并将稀疏度为99%以上的词删除
counts = CountVectorizer(min_df = 0.01)
# 文档词条矩阵
dtm_counts = counts.fit_transform(words).toarray()
# 矩阵的列名称
columns = counts.get_feature_names()
# 将矩阵转换为数据框--即X变量
X = pd.DataFrame(dtm_counts, columns=columns)
# 情感标签变量
y = evaluation.Type
X.head()
```


```python
from sklearn import model_selection
from sklearn import naive_bayes
from sklearn import metrics
import matplotlib.pyplot as plt
import seaborn as sns
# 将数据集拆分为训练集和测试集
X_train,X_test,y_train,y_test = model_selection.train_test_split(X,y,test_size = 0.25, random_state=1)
# 构建伯努利贝叶斯分类器
bnb = naive_bayes.BernoulliNB()
# 模型在训练数据集上的拟合
bnb.fit(X_train,y_train)
# 模型在测试数据集上的预测
bnb_pred = bnb.predict(X_test)
# 构建混淆矩阵
cm = pd.crosstab(bnb_pred,y_test)
# 绘制混淆矩阵图
sns.heatmap(cm, annot = True, cmap = 'GnBu', fmt = 'd')
# 去除x轴和y轴标签
plt.xlabel('Real')
plt.ylabel('Predict')
# 显示图形
plt.show()

# 模型的预测准确率
print('模型的准确率为：\n',metrics.accuracy_score(y_test, bnb_pred))
print('模型的评估报告：\n',metrics.classification_report(y_test, bnb_pred))
```


```python
# 计算正例Positive所对应的概率，用于生成ROC曲线的数据
y_score = bnb.predict_proba(X_test)[:,1]
fpr,tpr,threshold = metrics.roc_curve(y_test.map({'Negative':0,'Positive':1}), y_score)
# 计算AUC的值
roc_auc = metrics.auc(fpr,tpr)

# 绘制面积图
plt.stackplot(fpr, tpr, color='steelblue', alpha = 0.5, edgecolor = 'black')
# 添加边际线
plt.plot(fpr, tpr, color='black', lw = 1)
# 添加对角线
plt.plot([0,1],[0,1], color = 'red', linestyle = '--')
# 添加文本信息
plt.text(0.5,0.3,'ROC curve (area = %0.2f)' % roc_auc)
# 添加x轴与y轴标签
plt.xlabel('1-Specificity')
plt.ylabel('Sensitivity')
# 显示图形
plt.show()
```