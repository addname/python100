# Pandas数据处理

## 问题1：什么是Pandas？如何安装Pandas？

Pandas是Python中用于数据分析和处理的重要库，提供了强大的数据结构和数据分析工具：

```python
# 安装Pandas
# pip install pandas

# 导入Pandas
import pandas as pd

# 创建Series
s = pd.Series([1, 2, 3, 4, 5])
print(s)

# 创建DataFrame
df = pd.DataFrame({
    'A': [1, 2, 3, 4],
    'B': [5, 6, 7, 8],
    'C': [9, 10, 11, 12]
})
print(df)
```

## 问题2：如何创建和操作DataFrame？

```python
import pandas as pd

# 1. 从字典创建DataFrame
data = {
    '姓名': ['张三', '李四', '王五', '赵六'],
    '年龄': [25, 30, 35, 28],
    '城市': ['北京', '上海', '广州', '深圳'],
    '工资': [8000, 12000, 15000, 10000]
}
df = pd.DataFrame(data)
print(df)

# 2. 从列表创建DataFrame
data_list = [
    ['张三', 25, '北京', 8000],
    ['李四', 30, '上海', 12000],
    ['王五', 35, '广州', 15000],
    ['赵六', 28, '深圳', 10000]
]
columns = ['姓名', '年龄', '城市', '工资']
df2 = pd.DataFrame(data_list, columns=columns)
print(df2)

# 3. 基本操作
print(df.shape)      # 形状
print(df.columns)    # 列名
print(df.index)      # 索引
print(df.dtypes)     # 数据类型
print(df.info())     # 详细信息
print(df.describe()) # 统计描述
```

## 问题3：如何读取和写入数据？

```python
import pandas as pd

# 1. 读取CSV文件
df = pd.read_csv('data.csv')
print(df.head())  # 显示前5行

# 2. 读取Excel文件
df_excel = pd.read_excel('data.xlsx', sheet_name='Sheet1')
print(df_excel.head())

# 3. 读取JSON文件
df_json = pd.read_json('data.json')
print(df_json.head())

# 4. 写入CSV文件
df.to_csv('output.csv', index=False)

# 5. 写入Excel文件
df.to_excel('output.xlsx', sheet_name='Sheet1', index=False)

# 6. 写入JSON文件
df.to_json('output.json', orient='records')

# 7. 读取带分隔符的文件
df_tsv = pd.read_csv('data.tsv', sep='\t')
print(df_tsv.head())
```

## 问题4：如何进行数据选择和过滤？

```python
import pandas as pd

# 创建示例数据
data = {
    '姓名': ['张三', '李四', '王五', '赵六', '钱七'],
    '年龄': [25, 30, 35, 28, 32],
    '城市': ['北京', '上海', '广州', '深圳', '北京'],
    '工资': [8000, 12000, 15000, 10000, 11000]
}
df = pd.DataFrame(data)

# 1. 选择列
print(df['姓名'])        # 选择单列
print(df[['姓名', '年龄']])  # 选择多列

# 2. 选择行
print(df.iloc[0])        # 选择第一行
print(df.iloc[0:3])      # 选择前3行
print(df.loc[0:2])       # 选择前3行（包含结束行）

# 3. 条件过滤
print(df[df['年龄'] > 30])  # 年龄大于30
print(df[df['城市'] == '北京'])  # 城市为北京
print(df[(df['年龄'] > 25) & (df['工资'] > 10000)])  # 复合条件

# 4. 使用query方法
print(df.query('年龄 > 30 and 工资 > 10000'))

# 5. 使用isin方法
print(df[df['城市'].isin(['北京', '上海'])])
```

## 问题5：如何进行数据清洗？

```python
import pandas as pd
import numpy as np

# 创建包含缺失值的数据
data = {
    '姓名': ['张三', '李四', '王五', '赵六', '钱七'],
    '年龄': [25, 30, np.nan, 28, 32],
    '城市': ['北京', '上海', '广州', np.nan, '北京'],
    '工资': [8000, 12000, 15000, 10000, np.nan]
}
df = pd.DataFrame(data)

# 1. 检查缺失值
print(df.isnull())      # 检查缺失值
print(df.isnull().sum()) # 统计缺失值数量

# 2. 删除缺失值
df_dropna = df.dropna()  # 删除包含缺失值的行
print(df_dropna)

# 3. 填充缺失值
df_fillna = df.fillna({'年龄': df['年龄'].mean(), '工资': df['工资'].median()})
print(df_fillna)

# 4. 删除重复值
df_duplicated = df.drop_duplicates()
print(df_duplicated)

# 5. 数据类型转换
df['年龄'] = df['年龄'].astype(int)
print(df.dtypes)

# 6. 字符串处理
df['姓名'] = df['姓名'].str.upper()
print(df)
```

## 问题6：如何进行数据分组和聚合？

```python
import pandas as pd

# 创建示例数据
data = {
    '部门': ['技术部', '销售部', '技术部', '销售部', '技术部', '销售部'],
    '姓名': ['张三', '李四', '王五', '赵六', '钱七', '孙八'],
    '工资': [8000, 12000, 15000, 10000, 11000, 13000],
    '奖金': [2000, 3000, 4000, 2500, 2800, 3200]
}
df = pd.DataFrame(data)

# 1. 基本分组
grouped = df.groupby('部门')
print(grouped.groups)  # 显示分组信息

# 2. 分组聚合
print(grouped['工资'].sum())    # 按部门求和
print(grouped['工资'].mean())   # 按部门求平均
print(grouped['工资'].max())    # 按部门求最大值
print(grouped['工资'].min())    # 按部门求最小值

# 3. 多列聚合
print(grouped[['工资', '奖金']].sum())

# 4. 自定义聚合函数
def custom_agg(x):
    return x.max() - x.min()

print(grouped['工资'].agg(custom_agg))

# 5. 多重分组
df['年份'] = [2023, 2023, 2024, 2024, 2023, 2024]
multi_grouped = df.groupby(['部门', '年份'])
print(multi_grouped['工资'].sum())
```

## 问题7：如何进行数据合并和连接？

```python
import pandas as pd

# 创建示例数据
df1 = pd.DataFrame({
    'ID': [1, 2, 3, 4],
    '姓名': ['张三', '李四', '王五', '赵六'],
    '部门': ['技术部', '销售部', '技术部', '销售部']
})

df2 = pd.DataFrame({
    'ID': [1, 2, 3, 5],
    '工资': [8000, 12000, 15000, 10000],
    '奖金': [2000, 3000, 4000, 2500]
})

# 1. 内连接
inner_join = pd.merge(df1, df2, on='ID', how='inner')
print(inner_join)

# 2. 左连接
left_join = pd.merge(df1, df2, on='ID', how='left')
print(left_join)

# 3. 右连接
right_join = pd.merge(df1, df2, on='ID', how='right')
print(right_join)

# 4. 外连接
outer_join = pd.merge(df1, df2, on='ID', how='outer')
print(outer_join)

# 5. 纵向合并
df3 = pd.DataFrame({
    'ID': [5, 6],
    '姓名': ['钱七', '孙八'],
    '部门': ['技术部', '销售部']
})
vertical_merge = pd.concat([df1, df3], ignore_index=True)
print(vertical_merge)

# 6. 横向合并
horizontal_merge = pd.concat([df1, df2], axis=1)
print(horizontal_merge)
```

## 问题8：如何进行数据透视和重塑？

```python
import pandas as pd

# 创建示例数据
data = {
    '日期': ['2023-01-01', '2023-01-01', '2023-01-02', '2023-01-02'],
    '产品': ['A', 'B', 'A', 'B'],
    '销售额': [1000, 1500, 1200, 1800],
    '数量': [10, 15, 12, 18]
}
df = pd.DataFrame(data)

# 1. 数据透视表
pivot_table = df.pivot_table(
    values='销售额',
    index='日期',
    columns='产品',
    aggfunc='sum'
)
print(pivot_table)

# 2. 多重聚合
pivot_multi = df.pivot_table(
    values=['销售额', '数量'],
    index='日期',
    columns='产品',
    aggfunc={'销售额': 'sum', '数量': 'mean'}
)
print(pivot_multi)

# 3. 数据重塑
df_melted = df.melt(
    id_vars=['日期', '产品'],
    value_vars=['销售额', '数量'],
    var_name='指标',
    value_name='数值'
)
print(df_melted)

# 4. 数据转置
df_transposed = df.set_index(['日期', '产品']).T
print(df_transposed)
```

## 问题9：如何进行时间序列处理？

```python
import pandas as pd
import numpy as np

# 1. 创建时间序列
dates = pd.date_range('2023-01-01', periods=10, freq='D')
ts = pd.Series(np.random.randn(10), index=dates)
print(ts)

# 2. 时间索引操作
print(ts['2023-01-01'])  # 选择特定日期
print(ts['2023-01'])     # 选择特定月份
print(ts['2023-01-01':'2023-01-05'])  # 选择日期范围

# 3. 时间重采样
ts_resampled = ts.resample('W').mean()  # 按周重采样
print(ts_resampled)

# 4. 时间偏移
ts_shifted = ts.shift(1)  # 向前偏移1天
print(ts_shifted)

# 5. 时间差计算
ts_diff = ts.diff()  # 计算差分
print(ts_diff)

# 6. 滚动窗口
ts_rolling = ts.rolling(window=3).mean()  # 3天滚动平均
print(ts_rolling)
```

## 问题10：Pandas的实际应用场景

```python
import pandas as pd
import numpy as np

# 1. 销售数据分析
def analyze_sales_data():
    # 创建销售数据
    sales_data = {
        '日期': pd.date_range('2023-01-01', periods=100, freq='D'),
        '产品': np.random.choice(['A', 'B', 'C'], 100),
        '销售额': np.random.randint(1000, 10000, 100),
        '数量': np.random.randint(1, 100, 100)
    }
    df = pd.DataFrame(sales_data)
    
    # 分析
    daily_sales = df.groupby('日期')['销售额'].sum()
    product_sales = df.groupby('产品')['销售额'].sum()
    
    return df, daily_sales, product_sales

# 2. 用户行为分析
def analyze_user_behavior():
    # 创建用户行为数据
    user_data = {
        '用户ID': np.random.randint(1, 1000, 1000),
        '行为': np.random.choice(['点击', '购买', '浏览'], 1000),
        '时间': pd.date_range('2023-01-01', periods=1000, freq='H')
    }
    df = pd.DataFrame(user_data)
    
    # 分析
    behavior_counts = df['行为'].value_counts()
    hourly_activity = df.groupby(df['时间'].dt.hour).size()
    
    return df, behavior_counts, hourly_activity

# 3. 财务数据分析
def analyze_financial_data():
    # 创建财务数据
    financial_data = {
        '日期': pd.date_range('2023-01-01', periods=365, freq='D'),
        '收入': np.random.normal(10000, 2000, 365),
        '支出': np.random.normal(8000, 1500, 365),
        '利润': 0
    }
    df = pd.DataFrame(financial_data)
    df['利润'] = df['收入'] - df['支出']
    
    # 分析
    monthly_summary = df.groupby(df['日期'].dt.month)[['收入', '支出', '利润']].sum()
    profit_trend = df['利润'].rolling(window=30).mean()
    
    return df, monthly_summary, profit_trend

# 4. 数据质量检查
def check_data_quality(df):
    quality_report = {
        '总行数': len(df),
        '总列数': len(df.columns),
        '缺失值': df.isnull().sum().to_dict(),
        '重复行': df.duplicated().sum(),
        '数据类型': df.dtypes.to_dict()
    }
    return quality_report
```

## 总结

Pandas是Python数据分析的核心库，主要特点：
- **数据结构**：Series和DataFrame
- **数据读取**：支持CSV、Excel、JSON等格式
- **数据选择**：灵活的行列选择方式
- **数据清洗**：处理缺失值、重复值等
- **数据分组**：强大的分组聚合功能
- **数据合并**：多种连接方式
- **数据透视**：数据重塑和透视表
- **时间序列**：专业的时间处理功能
- **实际应用**：销售分析、用户行为、财务分析等
