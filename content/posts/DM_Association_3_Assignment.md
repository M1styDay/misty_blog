---
title: Association：Assignment
author: "Misty"
tags: ["Association","HKU"]
categories: ["Data Mining"]
date: 2021-01-08
---

# Association

## Frequent Itemsets

### Qustion 1

#### Qustion 1-1
* Table 1 shows a list of baskets as well as the items they contain. For example, this could be the set of products bought by each customer during a single trip to a grocery store. Using the A-priori algorithm, find all frequent itemsets with support threshold 0.4 (i.e. in this example they occur at least 40% of 7 times, i.e. at least three times.) In particular you should specify for each pass of the algorithm, the frequent itemsets, as well as the counters (and their values) kept in main memory by the A-priori algorithm.

#### Qustion 1-2
* Use the results from the previous step so as to compute the confidence and support of the rule b → d. In order to answer this question, are the results from the previous step sufficient or some information is missing?

#### Qustion 1-3
* Table 2 shows a new list of baskets as well as the items they contain. Using the PCY algorithm, find all frequent itemsets with support threshold 0.33 (i.e. in this example they occur at least 33% of 6, i.e. at least two times.) To this end, we are going to use the hash function f(i,j) = (i+j)%3 (% and mod are equivalent). In particular you should specify for each pass of the algorithm, the frequent itemsets, as well as all the counters (and their values) kept in main memory by the PCY algorithm.

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210313234142.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210313234207.png)

### Answer 1

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210316162335.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210316162403.png)

## Practical exercise on FI and AR

### Question 4

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210316162615.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210316164248.png)

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210316164324.png)

### Answer 4

```python
import math
import pandas as pd
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules

data = pd.read_csv(r"mammographic_masses.csv",delimiter=",",header=0)

d=data.values.tolist()

for i in range(0,len(d)):
    j=0
    while(True):
        if (type(d[i][j])==float and math.isnan(d[i][j])) :
            del d[i][j]
            j-=1
        j+=1
        if (j>len(d[i])-1):
            break

data

#adding attributes
print(d[:2])
for i in range(len(d)):
    for j in range (len(d[i])):
        d[i][j]=data.columns[j] + "=" +str(d[i][j])
print(d[:2])


te = TransactionEncoder()
te_ary = te.fit(d).transform(d)

df = pd.DataFrame(te_ary, columns=te.columns_)

#computing frequent itemsets and association rules
frequent_itemsets = apriori(df, min_support=0.2, use_colnames=True)

a=association_rules(frequent_itemsets, metric="confidence", min_threshold=0.9)

#visualizing association rules results
a[["antecedents","consequents","support","confidence"]]


#computing frequent itemsets and association rules
frequent_itemsets = apriori(df, min_support=0.1, use_colnames=True)

a=association_rules(frequent_itemsets, metric="confidence", min_threshold=0.9)

#visualizing association rules results
a[["antecedents","consequents","support","confidence"]]

for i in range(0,33):
    if ("Severity=1" in a["consequents"][i] ):
        print("the"+" "+str(i)+" "+"Severity=1")
        print(a["antecedents"][i])

for i in range(0,33):
    if ("Severity=0" in a["consequents"][i] ):
        print("the"+" "+str(i)+" "+"Severity=0")
        print(a["antecedents"][i])

#computing frequent itemsets and association rules
frequent_itemsets = apriori(df, min_support=0.01, use_colnames=True)

a=association_rules(frequent_itemsets, metric="confidence", min_threshold=0.01)

#visualizing association rules results
a[["antecedents","consequents","support","confidence"]]

for i in range(0,4676):
    if ("Age=35" in a["antecedents"][i] and "Severity=0" in a["consequents"][i] ):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])

```

```python
import math
import pandas as pd
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules

missing_values = ["?"]

data2 = pd.read_excel(r"mammographic_masses_v2.xlsx",na_values = missing_values)

data2.apply(lambda x: sum(x.isnull())/len(x),axis= 0) 

# pre-processing missing values
# Age BI-RADS(means)
data2.Age.fillna(data2.Age.mean(),inplace=True) 

data2.Age.mean()

data2.BI_RADS.fillna(data2.BI_RADS.mean(),inplace=True) 

data2.BI_RADS.mean()

# pre-processing missing values
# shape Margin Density(mode)

data2.Shape.fillna(data2.Shape.mode()[0],inplace=True) 

data2.Margin.fillna(data2.Margin.mode()[0],inplace=True) 

data2.Density.fillna(data2.Density.mode()[0],inplace=True)  

data2.apply(lambda x: sum(x.isnull())/len(x),axis= 0)

# Age gap 20
w = [0,20,40,60,80,100]

data2['Age_group'] = pd.cut(data2['Age'],bins = w)

data3 = data2.drop(labels = 'Age', axis = 1)

data3.head()

d = data3.values.tolist()

#removing nan values
for i in range(0,len(d)):
    j=0
    while(True):
        if (type(d[i][j])==float and math.isnan(d[i][j])) :
            del d[i][j]
            j-=1
        j+=1
        if (j>len(d[i])-1):
            break

data3

#adding attributes
print(d[:2])
for i in range(len(d)):
    for j in range (len(d[i])):
        d[i][j]=data3.columns[j] + "=" +str(d[i][j])
print(d[:2])


te = TransactionEncoder()
te_ary = te.fit(d).transform(d)

df = pd.DataFrame(te_ary, columns=te.columns_)

#computing frequent itemsets and association rules
frequent_itemsets = apriori(df, min_support=0.1, use_colnames=True)

a=association_rules(frequent_itemsets, metric="confidence", min_threshold=0.9)

#visualizing association rules results
a[["antecedents","consequents","support","confidence"]]

for i in range(0,81):
    if ("Age_group=(0, 20]" in a["antecedents"][i] and "Severity=0" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
    if ("Age_group=(20, 40]" in a["antecedents"][i] and "Severity=0" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
    if ("Age_group=(40, 60]" in a["antecedents"][i] and "Severity=0" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
    if ("Age_group=(60, 80]" in a["antecedents"][i] and "Severity=0" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
    if ("Age_group=(80, 100]" in a["antecedents"][i] and "Severity=0" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])

for i in range(0,81):
    if ("Age_group=(0, 20]" in a["antecedents"][i] and "Severity=1" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
    if ("Age_group=(20, 40]" in a["antecedents"][i] and "Severity=1" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
    if ("Age_group=(40, 60]" in a["antecedents"][i] and "Severity=1" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
    if ("Age_group=(60, 80]" in a["antecedents"][i] and "Severity=1" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
    if ("Age_group=(80, 100]" in a["antecedents"][i] and "Severity=1" in a["consequents"][i]):
        print(a["antecedents"][i],a["consequents"][i],a["support"][i],a["confidence"][i])
```