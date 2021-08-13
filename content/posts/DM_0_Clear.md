---
title: Pre-processing
author: "Misty"
tags: ["Model"]
categories: ["Data Mining"]
date: 2021-01-01
---

## 常用工具

### numpy

#### 构建数组

* Numpy中常用的数据结构是ndarray格式

* 使用array函数创建，语法格式为array(列表或元组)

* 可以使用其他函数例如arange、linspace、zeros等创建 
	  
```python
import numpy as np
arr1 = np.array([-9,7,4,3]) np.arange(0,10,1) np.linspace(1,10,10) np.zeros (1,5) 
```	  

#### 常用方法

* 常用方法名称：ndim、shape、size、dtype、运算
	  
* 数组访问方法：array$[行，列]$
	  
#### 排序
  * sort函数：从小到大进行排序
  * argsort函数：返回的是数据中, 从小到大的索引值 

```python	  
s = np.array([1,2,3,4,3,1,2,2,4,6,7,2,4,8,4,5]) 
np.sort(s) 
np.argsort(s) 
```  

#### 搜索

```python
np.where
np.extract
	  
np.where(s>3,1,-1) 
np.extract(s>3,s) 
```  

### pandas

#### 构建数组（series）

```python
series1 = pd.Series([2.8,3.01,8.99,8.59,5.18])
	  
series2 = pd.Series([2.8,3.01,8.99,8.59,5.18],index = ['a','b','c','d','e'],name ='这是一个series’) 
	  
series3 = pd.Series(np.array((2.8,3.10,8.99,8.59,5.18)),index = ['a','b','c','d','e’])
	  
series4 = pd.Series({'北京':2.8,'上海':3.01,'广东':8.99,'江苏':8.59,'浙江':5.18}) 
``` 
	  
#### 构建数组（dataframe）

```python
list1 = [['张三',23,'男'],['李四',27,'女'],['王二',26,'女']]#使用嵌套列表
df1 = pd.DataFrame(list1,columns=['姓名','年龄','性别'])
	  
df2 = pd.DataFrame({'姓名':['张三','李四','王二'],'年龄':[23,27,26],'性别':['男','女','女']}) 
	  
array1 = np.array([['张三',23,'男'],['李四',27,'女'],['王二',26,'女']])# 使用numpy
df3 = pd.DataFrame(array1,columns=['姓名','年龄','性别'],index = ['a','b','c’] ) 
```  

#### 常用方法

* 常用方法名称：values、index、dtypes、shape、ndim、size、columns



## 数据清洗步骤

### 数据获取

#### 更改文件路径

```python
# 更改文件路径
os.chdir('F:\CSDN\课程内容\代码和数据')

#设置最大显示列数
pd.set_option('display.max_columns', 20)

#设置最大显示行数
pd.set_option('display.max_rows', 100)
```  

#### csv文件读写

* pandas内置了10多种数据源读取函数,常见的就是CSV和EXCEL 

* 使用read_csv方法读取，结果为dataframe格式

* 在读取csv文件时，文件名称尽量是英文

* 参数较多，可以自行控制，但很多时候用默认参数 

* 读取csv时，注意编码，常用编码为utf-8、gbk 、gbk2312和gb18030等 

* 使用to_csv方法快速保存 

```python
df = pd.read_csv('meal_order_info.csv',encoding = ‘gbk’)
  
df = pd.read_csv('meal_order_info.csv',encoding = 'gbk’,nrows=10) 
  
df.to_csv(‘df.csv’,index=False) 
```  
  
#### excel文件读写

* 使用read_excel读取,读取后的结果为dataframe格式

* 读取excel文件和csv文件参数大致一样, 但要考虑工作表sheet页

* 参数较多，可以自行控制，但很多时候用默认参数

* 读取excel时，注意编码，常用编码为utf-8、gbk 、gbk2312和gb18030等 

* 使用to_excel快速保存为xlsx格式 
  
```python
df = pd.read_excel('meal_order_info.xlsx', sheet_name = ‘sheet1')
  
df = pd. read_excel('meal_order_info.xlsx',encoding = ‘utf-8’,nrows=10) 
  
df.to_excel('a1.xlsx', sheet_name=‘sheet1', index= False,encoding='utf-8) 
```  

#### 数据库文件读写

* 使用sqlalchemy建立连接
  
* 需要知道数据库的相关参数，如数据库IP地址、用户名和密码等 

* 通过pandas中read_sql函数读入, 读取完以后是dataframe格式 

* 通过dataframe的to_sql方法保存 

```python 
sql = 'select * from meal_order_info' #选择数据库中表名称 
  
df1 = pd.read_sql(sql,conn) 
  
df.to_sql('testdf',con = conn, index= False,if_exists= 'replace') 
```  

#### 数据库建立连接参数

```python
conn = create_engine('mysql+pymysql://user:passward@IP:3306/test01') 
```

* root: 用户名 
* passward: 密码 
* IP : 服务器IP，本地电脑用localhost 
* 3306: 端口号 
* test01 : 数据库名称 

```python
df.to_sql(name, con=engine, if_exists='replace/append/fail',index=False) 
```

* name是表名 
* con是连接 
* if_exists:表如果存在怎么处理。三个选项 append代表追加, replace代表删除原表，建立新表，fail代表什么都不干 
* index=False:不插入索引index 
  


### 数据探索

* shape
* describe
* info
* head
* dtypes

### 行列操作

#### 数据常用筛选方法(loc/iloc)
* loc$[行索引名称或者条件,列索引名称或者标签]$
* iloc$[行索引位置,列索引位置]$

```python  
basic[['户主姓名','农户生产经营类型']] 
  
basic.loc[0:2,['户主姓名', '户主身份证号']] 
  
order.iloc[:,[0,2]] 
  
basic.loc[basic['健康状况']== '良好',['户主姓名', '户主身份证号','健康状况']] 
  
basic.iloc[3,[1,2]] 
``` 

#### 数据增加和删除(insert/del/drop)

* 在数据中,直接添加列
* 使用df.insert方法在数据中添加一列
* 掌握drop(labels,axis,inplace=True) 的用法
* labels表示删除的数据, axis表示作用轴，inplace=True表示是否对原数据生效 
* axis=0按行操作, axis=1按列操作
* 使用del函数直接删除其中一列 
  
```python
del basic['数据']
  
basic.drop(labels = ['敬老爱幼情况', '家庭和睦情况'],axis = 1,inplace=True) 
  
basic.drop(labels= range(6,11),axis=0,inplace=True) 
  
basic.insert(0, '出生年月', mid) 
```

#### 数据修改和查找

* 在数据中, 可以使用rename修改列名称或者行索引名称
* 使用loc方法修改数据
* 使用loc方法查找符合条件的数据
* 条件与条件之间用&或者|连接，分别代表‘且’和‘或’ 
* 使用between和isin选择满足条件的行 

```python
basic[['户主身份证号','性别']][(basic.健康状况== '良好') & (basic['农户家庭人数'] >3)] 
  
basic[['户主身份证号','性别','婚姻状况']][ basic['农户家庭人数'].between(4,10,inclusive=True)] 
  
basic.loc[basic['是否加入农民合作社']== '未知', '是否加入农民合作社'] = '否‘ 
  
basic.rename(columns = {'出生年月':'出生日期','文化程度':'受教育水平' },inplace = True) 
  
basic.rename(index = {1:'one','10':'ten' },inplace = True) 
```
  

### 数据整合

#### 数据整理(concat/append)

```python
merge1 = pd.concat([df1,df2],axis=1,join='inner’)
  
merge1 = pd.concat([df1,df2],axis=1,join='outer’)
  
order_merge = pd.concat([order1,order2,order3],axis=0, ignore_index=False) 
  
order_merge.reset_index(inplace=True) 
  
append
```

#### 层次化索引

```python
df.loc[(28,[82830661,532110457]),['auction_id','cat_id']]
# 第二层索引选择，选择2个变量
```

* 直接引用两层
* df3.loc$[(a,b),:]$ # a和b分别代表第一层和第二层的索引
* 接受tuple


### 数据转换

#### 日期格式数据处理(datatime/dt/Timedelta)

* Pandas中使用to_datetime()方法将文本格式转换为日期格式
* dataframe数据类型如果为datetime64,可以使用dt方法取出年月日等
* 对于时间差数据,可以使用timedelta函数将其转换为指定时间单位的数值 
* 时间差数据,可以使用dt方法访问其常用属性 

#### 字符串数据处理

* Pandas中提供了字符串的函数,但只能对字符型变量进行使用 
* 通过str方法访问相关属性
* 可以使用字符串的相关方法进行数据处理 
  * contains()
  * replace()
  * lower()
  * upper()
  * split()
  * strip()
  * join()
  
#### 高阶函数数据处理

* 在dataframe中使用apply方法，调用自定义函数对数据进行处理 
* 函数apply, axis=0表示对行进行操作,axis=1表示对列进行操作
* 可以使用astype函数对数据进行转换
* 可以使用map函数进行数据转换

```python
# 0代表女，1代表男，2代表未知
df2['性别'] = df2['gender'].apply(f)
  
#使用map函数
df2['性别'] = df2['gender'].map({'0':'女','1':'男','2':'未知'})

#lambda
df2['user_id'].apply(lambda x: x.replace(x[1:3],'**')) 
```  

### 分组汇总

```python
var_name = ['Food%', 'Fresh%', 'Drinks%']

df[var_name].apply(np.sum,axis = 0) #相当于计算每列的总和

df['sum'] = df[var_name].apply(np.sum,axis=1)

var_name.append('sum')

df[var_name]

df[var_name].apply(lambda x: x[0] - x[1],axis = 1) 
#计算食物在订单总价中占比 - 生鲜类食物在订单总中占比
```

#### 数据分组运算$(df.groupby(by=[' ']))$

* 使用groupby方法进行分组计算，得到分组对象GroupBy
* 语法为df.groupby(by=)
* 分组对象GroupBy可以运用描述性统计方法, 如count、mean、 median、max和min等 

```python
Group = loan_info.groupby(by = 'product’) 
Group1= loan_info.groupby(by = ['product','jgmc’]) Group.mean()
Group.sum()
Group.max() 
```

#### 聚合函数使用(Groupby.agg(func))

* 对分组对象使用agg聚合函数
* 针对不同的变量使用不同的统计方法 

```python
grouped.agg({'total_items':[np.sum],'Food%':[np.mean,np.median]})
```

#### 分组对象和apply函数(Groupby.apply(func))

* 函数apply即可用于分组对象,也可以作用于dataframe数据 
* 需要注意axis=0和axis=1的区别 

```python
df[var_name].apply(lambda x: x[0]-x[1],axis =1)
  
df['sum'] = df[var_name].apply(np.sum,axis = 1)
```

#### 透视图与交叉表

* 透视表
```python
pivot_table( data, index, columns,values, aggfunc, fill_value, margins, margins_name=)
```
  * Index : 行分组键
  * columns: 列分组键 
  * values: 分组的字段，只能为数值型变量 
  * aggfunc: 聚合函数
  * margins: 是否需要总计 
  
* 交叉表用于计算分组频率
```python
pd.crosstab(index,columns,normalize)
```
  * Index: 行索引
  * Columns: 列索引
  * Normalize: 数据对数据进行标准化，index表示行，column表示列 


### 处理重复值、缺失值和异常值以及数据离散化

#### 重复值处理

* 查找

```python
df[df.duplicated()]
np.sum(df.duplicated())
```
* 删除

```python
df.drop_duplicates()
df.drop_duplicates(subset= ['appname','size'],inplace=True) 
``` 

#### 缺失值处理

* 查找
```python
df.apply(lambda x: sum(x.isnull())/len(x),axis= 0) #缺失比例
  
df[df['Exterior_Color'].isnull()]
```  

* 删除

```python
df.dropna() #直接删除法
	  
df.dropna(how='any',axis = 1 ) #只要有缺失，就删除这一列
	  
df.dropna(axis = 0,how='any',subset=['Condition','Price','Mileage']) 
# 1代表列，0代表行，只要有缺失，就删除这一行,基于三个变量
```	  

* 填补

```python
df.Mileage.fillna(df.Mileage.mean()) # 年龄用均值填补
	  
df.Mileage.fillna(df.Mileage.median()) # 中位数填补
	  
df.fillna(20) # 所有缺失用20填补
	  
df.Exterior_Color.fillna(df.Exterior_Color.mode()[0])  # 众数填补 

# 婚姻状况使用众数,年龄使用均值,农户家庭人数使用中位数
df.fillna(value = {'Exterior_Color':df.Exterior_Color.mode()[0],'Mileage':df.Mileage.mean()})
	
# 前向填补
df['Exterior_Color'].fillna(method='ffill')
  
# 后向填补bfill
```  

#### 异常值处理

指那些偏离正常范围的值，不是错误值

异常值出现频率较低，但又会对实际项目分析造成偏差

异常值一般用过箱线图法(分位差法)或者分布图(标准差法)来判断 

异常值往往采取盖帽法或者数据离散化


* 检查

**异常值检测之标准差法**

```python
xbar = df.Price.mean() 
xstd = df.Price.std()
print('标准差法异常值上限检测：\n',any(df.Price> xbar + 2.5 * xstd))
print('标准差法异常值下限检测：\n',any(df.Price< xbar - 2.5 * xstd))
```	  
		  

**异常值检测之箱线图法**

```python
Q1 = df.Price.quantile(q = 0.25)
Q3 = df.Price.quantile(q = 0.75)
IQR = Q3 - Q1
		  
print('箱线图法异常值上限检测：\n',any(df.Price > Q3 + 1.5 * IQR))
print('箱线图法异常值下限检测：\n',any(df.Price < Q1 - 1.5 * IQR))
```		  

**绘图**

```python
#箱图
df.Price.plot(kind ='box')
		  
# 设置绘图风格
plt.style.use('seaborn')
# 绘制直方图
df.Price.plot(kind = 'hist', bins = 30, density = True)
# 绘制核密度图
df.Price.plot(kind = 'kde')
# 图形展现
plt.show()
```	  

* 处理

```python
#用99分位数和1分位数替换
#计算P1和P99
P1 =df.Price.quantile(0.01); 
P99 = df.Price.quantile(0.99)
	  
#先创建一个新变量，进行赋值，然后将满足条件的数据进行替换
df['Price_new'] = df['Price']
df.loc[df['Price'] > P99,'Price_new']  = P99
df.loc[df['Price'] < P1,'Price_new']  = P1
	  
df[['Price','Price_new']].describe()
```	  

#### 数据离散化

数据离散化就是分箱

一般常用分箱方法是等频分箱或者等宽分箱 

一般使用pd.cut或者pd.qcut函数 
  
* cut

```python
pandas.cut(x, bins, right=True, labels=None, retbins=False, precision=3, include_lowest=False)
```
	  
* qcut

```python
pandas.qcut(x, q, labels=None, retbins=False, precision=3, duplicates=’raise’)
```  

## 知识点

### 数据清洗操作顺序

1. 选择子集
2. 重命名列
3. 缺失数据处理
4. 数据类型的转换
5. 字符串的处理
6. 时间日期的处理
7. 数据排序
8. 异常值处理

### 脏数据

* 数据缺失
* 数据噪声
* 数据不一致
* 数据冗余
* 离群点/异常值
* 数据重复是在数据集中出现多次的数据

## Reference

[整理一份详细的数据预处理方法](https://cloud.tencent.com/developer/article/1463854)