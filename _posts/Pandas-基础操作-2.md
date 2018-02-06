---
title: Pandas 基础操作 2
date: 2018-02-05 15:08:57
tags: 机器学习
---

```python
# 筛选出某个字段满足某个条件的列
import pandas as pd
df = pd.read_csv('store_data.csv')
df_a = df[df['storeA'] < 1000]		# 创建一个新的DataFrame, 容纳storeA这个字段<1000的所有列
df_b = df[df['storeA'] > 10000]		# 创建一个新的DataFrame, 容纳storeA这个字体>10000的所有列
df_b	# 显示df_a这个DataFrame所有的数据
```

```python
# 表合并，及添加新的列
import pandas as pd
import numpy as np

# 读取数据，分别存在两个DataFrame中
red_df = pd.read_csv('winequality-red.csv',sep=';')
white_df = pd.read_csv('winequality-white.csv',sep=';')

# 使用numpy创建一个新的列，要跟原始表的列数相同
color_red = np.repeat('color_red',1599)
color_white = np.repeat('color_white',4899)

# 分别将颜色赋予两个表
red_df['color'] = color_red
white_df['color'] = color_white

# 列重命名(这里要用inplace=True,如果不用，将会导致创建一个新的副本，并不会在原始表中操作)
red_df.rename(columns={'total_sulfur-dioxide':'total_sulfur_dioxide'},inplace=True)
# 附加数据
wine_df = red_df.append(white_df)

```

