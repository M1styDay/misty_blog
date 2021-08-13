---
title: Association：Practise
author: "Misty"
tags: ["Association","Model"]
categories: ["Data Mining"]
date: 2021-01-06
---

```python
#we run apriori on the order_data.csv file

import math
import pandas as pd
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules


data = pd.read_csv(r"order_data.csv",delimiter=" ",header=None)

#preprocessing: change to one hot encoding so as to be able to use apriori from mlxtend
d=data.values.tolist()

#removing nan values
for i in range(len(d)):
    j=0
    while(True):
        if (type(d[i][j])==float and math.isnan(d[i][j])) :
            del d[i][j]
            j-=1
        j+=1
        if (j>len(d[i])-1):
            break

te = TransactionEncoder()
te_ary = te.fit(d).transform(d)
df = pd.DataFrame(te_ary, columns=te.columns_)

#computing frequent itemsets and association rules
frequent_itemsets = apriori(df, min_support=0.2, use_colnames=True)

a=association_rules(frequent_itemsets, metric="confidence", min_threshold=0.6)

#visualizing association rules results
a[["antecedents","consequents","support","confidence"]]

type(a["antecedents"][99]) #prints frozenset

#frozenset is very similar to a set in Python with the main difference that cannot be changed.
#so we can check if a rule contains shampoo and honey as follows
i=99
if ("shampoo" in a["antecedents"][i] and "honey" in a["consequents"][i] ):
    print ("The "+str(i)+" rule talks about shampoo and honey:" )
else:
    print ("The "+str(i)+"th rule does not talk about shampoo and honey:" )
```

```python
import math
import pandas as pd
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules


data = pd.read_csv(r"mammographic_masses.csv",delimiter=",",header=0)

#preprocessing: change to one hot encoding so as to be able to use apriori from mlxtend
d=data.values.tolist()

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

#this part needs to be filled...
```