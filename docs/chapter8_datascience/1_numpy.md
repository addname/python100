# NumPy基础

## 问题1：什么是NumPy？如何安装NumPy？

NumPy是Python中用于科学计算的基础库，提供了高性能的多维数组对象和工具：

```python
# 安装NumPy
# pip install numpy

# 导入NumPy
import numpy as np

# 创建数组
arr = np.array([1, 2, 3, 4, 5])
print(arr)  # [1 2 3 4 5]
print(type(arr))  # <class 'numpy.ndarray'>
```

## 问题2：如何创建NumPy数组？

```python
import numpy as np

# 1. 从列表创建
list_data = [1, 2, 3, 4, 5]
arr1 = np.array(list_data)
print(arr1)

# 2. 创建零数组
zeros = np.zeros(5)
print(zeros)  # [0. 0. 0. 0. 0.]

# 3. 创建一数组
ones = np.ones(5)
print(ones)  # [1. 1. 1. 1. 1.]

# 4. 创建范围数组
range_arr = np.arange(0, 10, 2)
print(range_arr)  # [0 2 4 6 8]

# 5. 创建等间距数组
linspace_arr = np.linspace(0, 1, 5)
print(linspace_arr)  # [0.   0.25 0.5  0.75 1.  ]

# 6. 创建随机数组
random_arr = np.random.random(5)
print(random_arr)

# 7. 创建二维数组
matrix = np.array([[1, 2, 3], [4, 5, 6]])
print(matrix)
```

## 问题3：NumPy数组的基本操作有哪些？

```python
import numpy as np

# 创建数组
arr = np.array([1, 2, 3, 4, 5])

# 1. 数组属性
print(arr.shape)    # 形状: (5,)
print(arr.size)     # 大小: 5
print(arr.dtype)    # 数据类型: int64
print(arr.ndim)     # 维度: 1

# 2. 数组索引和切片
print(arr[0])       # 第一个元素: 1
print(arr[-1])      # 最后一个元素: 5
print(arr[1:4])     # 切片: [2 3 4]

# 3. 数组运算
arr2 = np.array([2, 3, 4, 5, 6])
print(arr + arr2)   # 加法: [3 5 7 9 11]
print(arr - arr2)   # 减法: [-1 -1 -1 -1 -1]
print(arr * arr2)   # 乘法: [2 6 12 20 30]
print(arr / arr2)   # 除法: [0.5 0.66666667 0.75 0.8 0.83333333]

# 4. 标量运算
print(arr + 2)      # 每个元素加2: [3 4 5 6 7]
print(arr * 3)      # 每个元素乘3: [3 6 9 12 15]
```

## 问题4：如何处理多维数组？

```python
import numpy as np

# 创建二维数组
matrix = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(matrix)
print(matrix.shape)  # (3, 3)

# 1. 索引和切片
print(matrix[0, 0])    # 第一行第一列: 1
print(matrix[1, 2])    # 第二行第三列: 6
print(matrix[0, :])    # 第一行: [1 2 3]
print(matrix[:, 1])    # 第二列: [2 5 8]
print(matrix[1:3, 1:3]) # 子矩阵: [[5 6] [8 9]]

# 2. 数组变形
arr = np.arange(12)
reshaped = arr.reshape(3, 4)
print(reshaped)

# 3. 数组转置
transposed = reshaped.T
print(transposed)

# 4. 数组展平
flattened = reshaped.flatten()
print(flattened)
```

## 问题5：NumPy的数学函数有哪些？

```python
import numpy as np

# 创建数组
arr = np.array([1, 4, 9, 16, 25])

# 1. 基本数学函数
print(np.sqrt(arr))      # 平方根: [1. 2. 3. 4. 5.]
print(np.square(arr))    # 平方: [1 16 81 256 625]
print(np.exp(arr))       # 指数
print(np.log(arr))       # 对数
print(np.sin(arr))       # 正弦
print(np.cos(arr))       # 余弦

# 2. 统计函数
print(np.sum(arr))       # 求和: 55
print(np.mean(arr))      # 平均值: 11.0
print(np.std(arr))       # 标准差
print(np.var(arr))       # 方差
print(np.min(arr))       # 最小值: 1
print(np.max(arr))       # 最大值: 25
print(np.argmin(arr))    # 最小值的索引: 0
print(np.argmax(arr))    # 最大值的索引: 4

# 3. 数组操作
print(np.sort(arr))      # 排序
print(np.unique(arr))    # 去重
print(np.concatenate([arr, arr]))  # 连接数组
```

## 问题6：如何处理数组的广播？

```python
import numpy as np

# 1. 标量广播
arr = np.array([1, 2, 3, 4, 5])
result = arr + 10
print(result)  # [11 12 13 14 15]

# 2. 数组广播
arr1 = np.array([[1, 2, 3], [4, 5, 6]])
arr2 = np.array([10, 20, 30])
result = arr1 + arr2
print(result)  # [[11 22 33] [14 25 36]]

# 3. 不同形状的广播
arr1 = np.array([[1], [2], [3]])
arr2 = np.array([10, 20])
result = arr1 + arr2
print(result)  # [[11 21] [12 22] [13 23]]

# 4. 广播规则
# 从右到左比较维度，如果维度大小相等或其中一个为1，则可以广播
```

## 问题7：如何使用NumPy进行线性代数运算？

```python
import numpy as np

# 1. 矩阵乘法
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
C = np.dot(A, B)
print(C)  # [[19 22] [43 50]]

# 2. 矩阵转置
A_T = A.T
print(A_T)  # [[1 3] [2 4]]

# 3. 矩阵逆
A_inv = np.linalg.inv(A)
print(A_inv)  # [[-2.   1. ] [ 1.5 -0.5]]

# 4. 行列式
det = np.linalg.det(A)
print(det)  # -2.0

# 5. 特征值和特征向量
eigenvalues, eigenvectors = np.linalg.eig(A)
print("特征值:", eigenvalues)
print("特征向量:", eigenvectors)

# 6. 解线性方程组
# Ax = b
A = np.array([[3, 1], [1, 2]])
b = np.array([9, 8])
x = np.linalg.solve(A, b)
print("解:", x)
```

## 问题8：如何使用NumPy处理随机数？

```python
import numpy as np

# 1. 设置随机种子
np.random.seed(42)

# 2. 生成随机数
random_nums = np.random.random(5)
print(random_nums)

# 3. 生成随机整数
random_ints = np.random.randint(1, 10, 5)
print(random_ints)

# 4. 生成正态分布随机数
normal_nums = np.random.normal(0, 1, 5)
print(normal_nums)

# 5. 生成均匀分布随机数
uniform_nums = np.random.uniform(0, 1, 5)
print(uniform_nums)

# 6. 随机选择
arr = np.array([1, 2, 3, 4, 5])
random_choice = np.random.choice(arr, 3)
print(random_choice)

# 7. 随机排列
shuffled = np.random.permutation(arr)
print(shuffled)
```

## 问题9：如何使用NumPy进行数据预处理？

```python
import numpy as np

# 1. 数据标准化
data = np.array([1, 2, 3, 4, 5])
normalized = (data - np.mean(data)) / np.std(data)
print(normalized)

# 2. 数据归一化
min_max_normalized = (data - np.min(data)) / (np.max(data) - np.min(data))
print(min_max_normalized)

# 3. 处理缺失值
data_with_nan = np.array([1, 2, np.nan, 4, 5])
# 检查缺失值
print(np.isnan(data_with_nan))
# 删除缺失值
clean_data = data_with_nan[~np.isnan(data_with_nan)]
print(clean_data)

# 4. 数据去重
duplicate_data = np.array([1, 2, 2, 3, 3, 4])
unique_data = np.unique(duplicate_data)
print(unique_data)

# 5. 数据分箱
data = np.random.normal(0, 1, 100)
bins = np.linspace(-3, 3, 10)
digitized = np.digitize(data, bins)
print(digitized)
```

## 问题10：NumPy的实际应用场景

```python
import numpy as np

# 1. 图像处理
def process_image(image_array):
    # 转换为灰度图
    if len(image_array.shape) == 3:
        gray = np.mean(image_array, axis=2)
    else:
        gray = image_array
    
    # 归一化
    normalized = gray / 255.0
    
    # 应用滤波器
    filtered = np.convolve(normalized.flatten(), [1, 0, -1])
    
    return filtered

# 2. 信号处理
def generate_signal(frequency, duration, sample_rate):
    t = np.linspace(0, duration, int(sample_rate * duration))
    signal = np.sin(2 * np.pi * frequency * t)
    return t, signal

# 3. 数据分析
def analyze_data(data):
    analysis = {
        'mean': np.mean(data),
        'std': np.std(data),
        'min': np.min(data),
        'max': np.max(data),
        'median': np.median(data),
        'percentile_25': np.percentile(data, 25),
        'percentile_75': np.percentile(data, 75)
    }
    return analysis

# 4. 数值计算
def numerical_integration(func, a, b, n=1000):
    x = np.linspace(a, b, n)
    y = func(x)
    integral = np.trapz(y, x)
    return integral

# 5. 矩阵运算
def matrix_operations():
    # 创建随机矩阵
    A = np.random.rand(3, 3)
    B = np.random.rand(3, 3)
    
    # 矩阵运算
    C = A + B
    D = A * B  # 元素级乘法
    E = np.dot(A, B)  # 矩阵乘法
    
    return A, B, C, D, E
```

## 总结

NumPy是Python科学计算的基础，主要特点：
- **高性能数组**：C语言实现，计算速度快
- **多维数组**：支持1D、2D、3D等数组
- **丰富的函数**：数学、统计、线性代数等
- **广播机制**：自动处理不同形状的数组运算
- **内存效率**：连续内存存储，访问速度快
- **广泛兼容**：与其他科学计算库兼容
- **易于使用**：简洁的API设计
- **实际应用**：图像处理、信号处理、数据分析等
