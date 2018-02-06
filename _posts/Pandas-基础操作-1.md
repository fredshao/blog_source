---
title: Pandas 基础操作 1
date: 2018-01-31 15:43:36
tags: 机器学习
---

```python
# 读取CSV
import pandas as pd
df = pd.read_csv('cancer_data.csv')

# 如果csv文件不是以逗号分割的，则可以指定具体的分割符，例如以';'分割的csv文件
df = pd.read_csv('cancer_data.csv',sep=';')
```

```python
df.head()	# 返回前5行
df.head(20)	# 返回前20行
df.tail()	# 返回最后5行
df.tail(20)	# 返回最后20行
```

```python
df.types	# 返回列的数据类型
type(df['diagnosis'][0])	# 返回pandas object真正指向的类型
```

```python
df.info()	# 显示数据框的简明摘要，包括每列非空值的数量
df.describe()	# 返回每列数据的有效描述性统计
```

```python
# 查看每列的所引号和标签
for i , v in enumerate(df.columns):
  print(i,v)
```

```python
# 列选择 loc 使用行标签或列标签选择数据，iloc使用所引号
df_means = df.loc[:,'id','diagnosis']
df_means.head()

# 只显示第0列，第1列的数据
df_means = df.iloc[:,0:2]
df_means.head()

# 显示1，3，5列的数据
df_means = df.iloc[:,[1,3,5]]
df_means.head()
```

```python
# 把数据保存到csv，不包含所引号
df_means.to_csv('cancer_data_edited.csv', index=False)
```

```python
# 计算某一列的均值
texture_mean = df['texture_mean'].mean()

# 用刚刚计算的均值填充这一列中为空值的行
df['texture_mean'].fillna(texture_mean,inplace=True)

# 显示重复的行
df.duplicated()

# 统计重复的行
sum(df.duplicated())

# 从数据中去掉重复的行
df.drop_duplicates(inplace=True)
```

```python
# 遍历列名
for col in df.columns:
  print(col)
  
# 赋予新的列名 
df.columns=[...]
```

```python
#　绘图操作

#　显示整个表每列数据的直方图,figsize 可以调整图表大小
df.hist(figsize=(8,8))

# 为特定的一列显示直方图,下面两行代码能达到相同的效果
df['V'].hist()
df['V'].plot(kind='hist')

# 统计这一列数据中不同数值的数量
df['V'].value_counts()
df['V'].value_counts().plot(kind='bar')
df['V'].value_counts().hist()
df['V'].value_counts().plot(kind='pie',figsize=(8,8))	# 绘制饼状图

# 使用两列，绘制散点图
df.plot(x='AT',y='PE',kind='scatter')

# 为某一列绘制箱线图
df['AT'].plot(kind='box')
```

