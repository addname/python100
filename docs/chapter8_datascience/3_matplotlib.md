# Matplotlib数据可视化

## 问题1：什么是Matplotlib？如何安装Matplotlib？

Matplotlib是Python中最流行的数据可视化库，提供了丰富的绘图功能：

```python
# 安装Matplotlib
# pip install matplotlib

# 导入Matplotlib
import matplotlib.pyplot as plt
import numpy as np

# 基本绘图
x = np.linspace(0, 10, 100)
y = np.sin(x)
plt.plot(x, y)
plt.show()
```

## 问题2：如何创建基本图表？

```python
import matplotlib.pyplot as plt
import numpy as np

# 1. 线图
x = np.linspace(0, 10, 100)
y = np.sin(x)
plt.plot(x, y)
plt.title('正弦函数')
plt.xlabel('x')
plt.ylabel('sin(x)')
plt.show()

# 2. 散点图
x = np.random.randn(100)
y = np.random.randn(100)
plt.scatter(x, y)
plt.title('散点图')
plt.xlabel('x')
plt.ylabel('y')
plt.show()

# 3. 柱状图
categories = ['A', 'B', 'C', 'D']
values = [23, 45, 56, 78]
plt.bar(categories, values)
plt.title('柱状图')
plt.xlabel('类别')
plt.ylabel('数值')
plt.show()

# 4. 饼图
sizes = [30, 25, 20, 15, 10]
labels = ['A', 'B', 'C', 'D', 'E']
plt.pie(sizes, labels=labels, autopct='%1.1f%%')
plt.title('饼图')
plt.show()
```

## 问题3：如何自定义图表样式？

```python
import matplotlib.pyplot as plt
import numpy as np

# 1. 设置图表大小
plt.figure(figsize=(10, 6))

# 2. 设置标题和标签
plt.title('自定义样式图表', fontsize=16, fontweight='bold')
plt.xlabel('x轴标签', fontsize=12)
plt.ylabel('y轴标签', fontsize=12)

# 3. 设置坐标轴
plt.xlim(0, 10)
plt.ylim(-1, 1)
plt.xticks(np.arange(0, 11, 2))
plt.yticks(np.arange(-1, 1.5, 0.5))

# 4. 设置网格
plt.grid(True, alpha=0.3)

# 5. 设置图例
x = np.linspace(0, 10, 100)
y1 = np.sin(x)
y2 = np.cos(x)
plt.plot(x, y1, label='sin(x)', linewidth=2, color='red')
plt.plot(x, y2, label='cos(x)', linewidth=2, color='blue')
plt.legend()

# 6. 设置背景色
plt.gca().set_facecolor('lightgray')

plt.show()
```

## 问题4：如何创建子图？

```python
import matplotlib.pyplot as plt
import numpy as np

# 1. 创建子图
fig, axes = plt.subplots(2, 2, figsize=(12, 8))

# 2. 在子图中绘图
x = np.linspace(0, 10, 100)

# 第一个子图
axes[0, 0].plot(x, np.sin(x))
axes[0, 0].set_title('正弦函数')
axes[0, 0].set_xlabel('x')
axes[0, 0].set_ylabel('sin(x)')

# 第二个子图
axes[0, 1].plot(x, np.cos(x))
axes[0, 1].set_title('余弦函数')
axes[0, 1].set_xlabel('x')
axes[0, 1].set_ylabel('cos(x)')

# 第三个子图
axes[1, 0].scatter(x, np.random.randn(100))
axes[1, 0].set_title('散点图')
axes[1, 0].set_xlabel('x')
axes[1, 0].set_ylabel('y')

# 第四个子图
categories = ['A', 'B', 'C', 'D']
values = [23, 45, 56, 78]
axes[1, 1].bar(categories, values)
axes[1, 1].set_title('柱状图')
axes[1, 1].set_xlabel('类别')
axes[1, 1].set_ylabel('数值')

# 3. 调整子图间距
plt.tight_layout()
plt.show()
```

## 问题5：如何创建3D图表？

```python
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import numpy as np

# 1. 创建3D图形
fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')

# 2. 创建3D数据
x = np.linspace(-5, 5, 50)
y = np.linspace(-5, 5, 50)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))

# 3. 绘制3D表面
surf = ax.plot_surface(X, Y, Z, cmap='viridis', alpha=0.8)

# 4. 设置标签和标题
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')
ax.set_title('3D表面图')

# 5. 添加颜色条
plt.colorbar(surf)

plt.show()
```

## 问题6：如何处理时间序列数据？

```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# 1. 创建时间序列数据
dates = pd.date_range('2023-01-01', periods=365, freq='D')
values = np.cumsum(np.random.randn(365)) + 100

# 2. 创建时间序列图
plt.figure(figsize=(12, 6))
plt.plot(dates, values)
plt.title('时间序列图')
plt.xlabel('日期')
plt.ylabel('数值')
plt.xticks(rotation=45)

# 3. 添加趋势线
from scipy import stats
slope, intercept, r_value, p_value, std_err = stats.linregress(range(len(values)), values)
trend_line = slope * np.arange(len(values)) + intercept
plt.plot(dates, trend_line, 'r--', label='趋势线')

# 4. 添加移动平均线
window = 30
moving_avg = pd.Series(values).rolling(window=window).mean()
plt.plot(dates, moving_avg, 'g-', label=f'{window}天移动平均')

plt.legend()
plt.tight_layout()
plt.show()
```

## 问题7：如何创建统计图表？

```python
import matplotlib.pyplot as plt
import numpy as np

# 1. 直方图
data = np.random.normal(0, 1, 1000)
plt.figure(figsize=(10, 6))
plt.hist(data, bins=30, alpha=0.7, color='skyblue', edgecolor='black')
plt.title('直方图')
plt.xlabel('数值')
plt.ylabel('频次')
plt.show()

# 2. 箱线图
data1 = np.random.normal(0, 1, 100)
data2 = np.random.normal(2, 1.5, 100)
data3 = np.random.normal(-1, 0.5, 100)
plt.figure(figsize=(8, 6))
plt.boxplot([data1, data2, data3], labels=['组1', '组2', '组3'])
plt.title('箱线图')
plt.ylabel('数值')
plt.show()

# 3. 密度图
from scipy import stats
x = np.linspace(-4, 4, 100)
y = stats.norm.pdf(x, 0, 1)
plt.figure(figsize=(8, 6))
plt.plot(x, y)
plt.fill_between(x, y, alpha=0.3)
plt.title('概率密度函数')
plt.xlabel('x')
plt.ylabel('密度')
plt.show()
```

## 问题8：如何创建热力图？

```python
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns

# 1. 创建数据
data = np.random.randn(10, 10)

# 2. 使用matplotlib创建热力图
plt.figure(figsize=(8, 6))
plt.imshow(data, cmap='viridis', aspect='auto')
plt.colorbar()
plt.title('热力图')
plt.show()

# 3. 使用seaborn创建热力图
plt.figure(figsize=(8, 6))
sns.heatmap(data, annot=True, cmap='coolwarm', center=0)
plt.title('Seaborn热力图')
plt.show()

# 4. 相关性热力图
import pandas as pd
df = pd.DataFrame(np.random.randn(100, 5), columns=['A', 'B', 'C', 'D', 'E'])
correlation_matrix = df.corr()
plt.figure(figsize=(8, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title('相关性热力图')
plt.show()
```

## 问题9：如何保存和导出图表？

```python
import matplotlib.pyplot as plt
import numpy as np

# 1. 创建图表
x = np.linspace(0, 10, 100)
y = np.sin(x)
plt.figure(figsize=(10, 6))
plt.plot(x, y)
plt.title('正弦函数')
plt.xlabel('x')
plt.ylabel('sin(x)')

# 2. 保存为不同格式
plt.savefig('sine_plot.png', dpi=300, bbox_inches='tight')  # PNG格式
plt.savefig('sine_plot.pdf', bbox_inches='tight')           # PDF格式
plt.savefig('sine_plot.svg', bbox_inches='tight')           # SVG格式
plt.savefig('sine_plot.jpg', dpi=300, bbox_inches='tight')  # JPG格式

# 3. 设置保存参数
plt.savefig('sine_plot_high_quality.png', 
           dpi=300,                    # 高分辨率
           bbox_inches='tight',        # 紧凑布局
           facecolor='white',          # 背景色
           edgecolor='none')           # 边框色

plt.show()
```

## 问题10：Matplotlib的实际应用场景

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# 1. 销售数据分析
def plot_sales_analysis():
    # 创建销售数据
    months = ['1月', '2月', '3月', '4月', '5月', '6月']
    sales = [12000, 15000, 18000, 16000, 20000, 22000]
    
    plt.figure(figsize=(10, 6))
    plt.plot(months, sales, marker='o', linewidth=2, markersize=8)
    plt.title('月度销售趋势', fontsize=16, fontweight='bold')
    plt.xlabel('月份', fontsize=12)
    plt.ylabel('销售额', fontsize=12)
    plt.grid(True, alpha=0.3)
    plt.tight_layout()
    plt.show()

# 2. 用户行为分析
def plot_user_behavior():
    # 创建用户行为数据
    behaviors = ['点击', '浏览', '购买', '分享']
    counts = [1500, 800, 200, 50]
    colors = ['skyblue', 'lightgreen', 'orange', 'pink']
    
    plt.figure(figsize=(8, 6))
    plt.pie(counts, labels=behaviors, colors=colors, autopct='%1.1f%%', startangle=90)
    plt.title('用户行为分布', fontsize=16, fontweight='bold')
    plt.axis('equal')
    plt.show()

# 3. 性能监控
def plot_performance_monitoring():
    # 创建性能数据
    time_points = pd.date_range('2023-01-01', periods=24, freq='H')
    cpu_usage = np.random.normal(50, 15, 24)
    memory_usage = np.random.normal(60, 10, 24)
    
    plt.figure(figsize=(12, 6))
    plt.plot(time_points, cpu_usage, label='CPU使用率', linewidth=2)
    plt.plot(time_points, memory_usage, label='内存使用率', linewidth=2)
    plt.title('系统性能监控', fontsize=16, fontweight='bold')
    plt.xlabel('时间', fontsize=12)
    plt.ylabel('使用率 (%)', fontsize=12)
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()

# 4. 数据分布分析
def plot_data_distribution():
    # 创建数据
    data1 = np.random.normal(0, 1, 1000)
    data2 = np.random.normal(2, 1.5, 1000)
    
    plt.figure(figsize=(10, 6))
    plt.hist(data1, bins=30, alpha=0.7, label='数据集1', color='skyblue')
    plt.hist(data2, bins=30, alpha=0.7, label='数据集2', color='lightcoral')
    plt.title('数据分布对比', fontsize=16, fontweight='bold')
    plt.xlabel('数值', fontsize=12)
    plt.ylabel('频次', fontsize=12)
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.show()
```

## 总结

Matplotlib是Python数据可视化的核心库，主要特点：
- **基本图表**：线图、散点图、柱状图、饼图等
- **自定义样式**：颜色、线型、标记、标签等
- **子图功能**：多子图布局和组合
- **3D绘图**：3D表面图、散点图等
- **时间序列**：专业的时间数据可视化
- **统计图表**：直方图、箱线图、密度图等
- **热力图**：数据矩阵和相关性可视化
- **保存导出**：多种格式的图表保存
- **实际应用**：销售分析、用户行为、性能监控等
