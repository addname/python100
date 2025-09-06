# 第七章：数据科学

!!! info "数据科学基础"
    数据科学是Python的重要应用领域。本章将学习NumPy、Pandas、Matplotlib等数据科学工具，以及机器学习的基础知识。

## 问题91：什么是NumPy？如何使用NumPy进行数组操作？

### 🤔 问题描述
NumPy是什么？它有什么特点？如何创建和操作NumPy数组？NumPy在数据科学中有什么作用？

### 💡 详细解答

#### NumPy简介

NumPy（Numerical Python）是Python中用于科学计算的基础库，具有以下特点：
- 高性能的多维数组对象
- 丰富的数学函数库
- 线性代数、傅里叶变换等功能
- 与C/C++/Fortran代码的集成

#### 安装NumPy

```bash
# 安装NumPy
pip install numpy

# 或者使用conda
conda install numpy
```

#### 基本用法

```python
import numpy as np

# 1. 创建数组
arr1 = np.array([1, 2, 3, 4, 5])  # 一维数组
arr2 = np.array([[1, 2, 3], [4, 5, 6]])  # 二维数组
arr3 = np.zeros((3, 4))  # 零数组
arr4 = np.ones((2, 3))   # 一数组
arr5 = np.random.random((2, 3))  # 随机数组

# 2. 数组属性
print(arr2.shape)    # (2, 3) - 形状
print(arr2.ndim)     # 2 - 维度
print(arr2.size)     # 6 - 元素总数
print(arr2.dtype)    # int64 - 数据类型

# 3. 数组操作
print(arr1 + 10)     # 广播操作
print(arr1 * 2)      # 标量乘法
print(arr1 ** 2)     # 幂运算

# 4. 索引和切片
print(arr2[0, 1])    # 访问元素
print(arr2[0, :])    # 第一行
print(arr2[:, 1])    # 第二列
```

### 📝 代码示例

```python
# NumPy综合示例
import numpy as np
import matplotlib.pyplot as plt

def demonstrate_numpy_basics():
    """演示NumPy基础操作"""
    
    print("=== NumPy基础操作 ===")
    
    # 1. 创建不同类型的数组
    print("1. 创建数组:")
    arr1 = np.array([1, 2, 3, 4, 5])
    arr2 = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
    arr3 = np.zeros((3, 4))
    arr4 = np.ones((2, 3))
    arr5 = np.random.random((2, 3))
    
    print(f"一维数组: {arr1}")
    print(f"二维数组:\n{arr2}")
    print(f"零数组:\n{arr3}")
    print(f"一数组:\n{arr4}")
    print(f"随机数组:\n{arr5}")
    
    # 2. 数组属性
    print("\n2. 数组属性:")
    print(f"arr2的形状: {arr2.shape}")
    print(f"arr2的维度: {arr2.ndim}")
    print(f"arr2的元素总数: {arr2.size}")
    print(f"arr2的数据类型: {arr2.dtype}")
    
    # 3. 数组操作
    print("\n3. 数组操作:")
    print(f"arr1 + 10: {arr1 + 10}")
    print(f"arr1 * 2: {arr1 * 2}")
    print(f"arr1 ** 2: {arr1 ** 2}")
    
    # 4. 索引和切片
    print("\n4. 索引和切片:")
    print(f"arr2[0, 1]: {arr2[0, 1]}")
    print(f"arr2[0, :]: {arr2[0, :]}")
    print(f"arr2[:, 1]: {arr2[:, 1]}")
    print(f"arr2[1:, 1:]:\n{arr2[1:, 1:]}")

def demonstrate_numpy_functions():
    """演示NumPy函数"""
    
    print("\n=== NumPy函数演示 ===")
    
    # 创建测试数据
    data = np.random.random((5, 4))
    print(f"测试数据:\n{data}")
    
    # 统计函数
    print(f"\n统计函数:")
    print(f"平均值: {np.mean(data)}")
    print(f"中位数: {np.median(data)}")
    print(f"标准差: {np.std(data)}")
    print(f"方差: {np.var(data)}")
    print(f"最大值: {np.max(data)}")
    print(f"最小值: {np.min(data)}")
    
    # 按轴统计
    print(f"\n按轴统计:")
    print(f"每行平均值: {np.mean(data, axis=1)}")
    print(f"每列平均值: {np.mean(data, axis=0)}")
    
    # 数学函数
    print(f"\n数学函数:")
    print(f"平方根: {np.sqrt(data[0, 0]):.4f}")
    print(f"指数: {np.exp(data[0, 0]):.4f}")
    print(f"对数: {np.log(data[0, 0] + 1):.4f}")
    
    # 三角函数
    angles = np.array([0, np.pi/4, np.pi/2, np.pi])
    print(f"\n三角函数:")
    print(f"角度: {angles}")
    print(f"正弦: {np.sin(angles)}")
    print(f"余弦: {np.cos(angles)}")

def demonstrate_array_operations():
    """演示数组操作"""
    
    print("\n=== 数组操作演示 ===")
    
    # 1. 数组形状操作
    arr = np.array([[1, 2, 3], [4, 5, 6]])
    print(f"原始数组:\n{arr}")
    print(f"形状: {arr.shape}")
    
    # 重塑数组
    reshaped = arr.reshape(3, 2)
    print(f"重塑为(3,2):\n{reshaped}")
    
    # 展平数组
    flattened = arr.flatten()
    print(f"展平: {flattened}")
    
    # 2. 数组拼接
    arr1 = np.array([[1, 2], [3, 4]])
    arr2 = np.array([[5, 6], [7, 8]])
    
    # 垂直拼接
    vstacked = np.vstack((arr1, arr2))
    print(f"\n垂直拼接:\n{vstacked}")
    
    # 水平拼接
    hstacked = np.hstack((arr1, arr2))
    print(f"水平拼接:\n{hstacked}")
    
    # 3. 数组分割
    arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
    print(f"\n原始数组:\n{arr}")
    
    # 垂直分割
    vsplit = np.vsplit(arr, 3)
    print(f"垂直分割:")
    for i, part in enumerate(vsplit):
        print(f"  部分{i+1}:\n{part}")
    
    # 水平分割
    hsplit = np.hsplit(arr, 2)
    print(f"水平分割:")
    for i, part in enumerate(hsplit):
        print(f"  部分{i+1}:\n{part}")

def demonstrate_linear_algebra():
    """演示线性代数操作"""
    
    print("\n=== 线性代数演示 ===")
    
    # 创建矩阵
    A = np.array([[1, 2], [3, 4]])
    B = np.array([[5, 6], [7, 8]])
    v = np.array([1, 2])
    
    print(f"矩阵A:\n{A}")
    print(f"矩阵B:\n{B}")
    print(f"向量v: {v}")
    
    # 矩阵乘法
    C = np.dot(A, B)
    print(f"\n矩阵乘法 A @ B:\n{C}")
    
    # 矩阵向量乘法
    result = np.dot(A, v)
    print(f"矩阵向量乘法 A @ v: {result}")
    
    # 矩阵转置
    A_T = A.T
    print(f"矩阵转置 A^T:\n{A_T}")
    
    # 矩阵逆
    try:
        A_inv = np.linalg.inv(A)
        print(f"矩阵逆 A^(-1):\n{A_inv}")
        
        # 验证
        identity = np.dot(A, A_inv)
        print(f"验证 A @ A^(-1):\n{identity}")
    except np.linalg.LinAlgError:
        print("矩阵不可逆")
    
    # 特征值和特征向量
    eigenvalues, eigenvectors = np.linalg.eig(A)
    print(f"\n特征值: {eigenvalues}")
    print(f"特征向量:\n{eigenvectors}")
    
    # 行列式
    det = np.linalg.det(A)
    print(f"行列式: {det}")

def demonstrate_random_operations():
    """演示随机操作"""
    
    print("\n=== 随机操作演示 ===")
    
    # 设置随机种子
    np.random.seed(42)
    
    # 生成随机数
    random_nums = np.random.random(5)
    print(f"随机数: {random_nums}")
    
    # 生成随机整数
    random_ints = np.random.randint(1, 10, size=5)
    print(f"随机整数: {random_ints}")
    
    # 生成正态分布随机数
    normal_nums = np.random.normal(0, 1, 5)
    print(f"正态分布随机数: {normal_nums}")
    
    # 生成均匀分布随机数
    uniform_nums = np.random.uniform(0, 1, 5)
    print(f"均匀分布随机数: {uniform_nums}")
    
    # 随机排列
    arr = np.array([1, 2, 3, 4, 5])
    shuffled = np.random.permutation(arr)
    print(f"随机排列: {shuffled}")
    
    # 随机选择
    selected = np.random.choice(arr, size=3, replace=False)
    print(f"随机选择: {selected}")

def main():
    """主函数"""
    demonstrate_numpy_basics()
    demonstrate_numpy_functions()
    demonstrate_array_operations()
    demonstrate_linear_algebra()
    demonstrate_random_operations()

if __name__ == "__main__":
    main()
```

---

## 问题92：如何使用NumPy进行数学运算？

### 🤔 问题描述
NumPy提供了哪些数学运算功能？如何进行向量化运算？如何提高计算性能？

### 💡 详细解答

#### 向量化运算

NumPy的核心优势是向量化运算，它允许对整个数组进行操作，而不需要循环：

```python
import numpy as np

# 传统Python方式（慢）
def slow_calculation(data):
    result = []
    for x in data:
        result.append(x**2 + 2*x + 1)
    return result

# NumPy向量化方式（快）
def fast_calculation(data):
    return data**2 + 2*data + 1

# 性能对比
data = list(range(1000))
data_np = np.array(data)

# 向量化运算
result = data_np**2 + 2*data_np + 1
```

#### 数学函数

```python
# 基本数学函数
x = np.array([1, 4, 9, 16, 25])
print(np.sqrt(x))      # 平方根
print(np.exp(x))       # 指数
print(np.log(x))       # 自然对数
print(np.log10(x))     # 常用对数
print(np.sin(x))       # 正弦
print(np.cos(x))       # 余弦
print(np.tan(x))       # 正切

# 统计函数
data = np.random.random((5, 4))
print(np.mean(data))   # 平均值
print(np.median(data)) # 中位数
print(np.std(data))    # 标准差
print(np.var(data))    # 方差
print(np.min(data))    # 最小值
print(np.max(data))    # 最大值
```

### 📝 代码示例

```python
# NumPy数学运算示例
import numpy as np
import time

def performance_comparison():
    """性能对比示例"""
    
    print("=== 性能对比 ===")
    
    # 创建测试数据
    size = 1000000
    data_python = list(range(size))
    data_numpy = np.array(data_python)
    
    # Python循环方式
    start_time = time.time()
    result_python = [x**2 for x in data_python]
    python_time = time.time() - start_time
    
    # NumPy向量化方式
    start_time = time.time()
    result_numpy = data_numpy**2
    numpy_time = time.time() - start_time
    
    print(f"Python循环方式耗时: {python_time:.4f}秒")
    print(f"NumPy向量化方式耗时: {numpy_time:.4f}秒")
    print(f"性能提升: {python_time/numpy_time:.2f}倍")

def mathematical_functions_demo():
    """数学函数演示"""
    
    print("\n=== 数学函数演示 ===")
    
    # 创建测试数据
    x = np.linspace(0, 2*np.pi, 10)
    print(f"x值: {x}")
    
    # 基本数学函数
    print(f"\n基本数学函数:")
    print(f"平方根: {np.sqrt(x)}")
    print(f"平方: {x**2}")
    print(f"指数: {np.exp(x)}")
    print(f"自然对数: {np.log(x + 1)}")
    print(f"常用对数: {np.log10(x + 1)}")
    
    # 三角函数
    print(f"\n三角函数:")
    print(f"正弦: {np.sin(x)}")
    print(f"余弦: {np.cos(x)}")
    print(f"正切: {np.tan(x)}")
    
    # 反三角函数
    print(f"\n反三角函数:")
    print(f"反正弦: {np.arcsin(np.sin(x))}")
    print(f"反余弦: {np.arccos(np.cos(x))}")
    print(f"反正切: {np.arctan(np.tan(x))}")

def statistical_functions_demo():
    """统计函数演示"""
    
    print("\n=== 统计函数演示 ===")
    
    # 创建测试数据
    data = np.random.normal(100, 15, 1000)  # 正态分布
    print(f"数据样本: {data[:10]}...")
    
    # 基本统计
    print(f"\n基本统计:")
    print(f"平均值: {np.mean(data):.2f}")
    print(f"中位数: {np.median(data):.2f}")
    print(f"标准差: {np.std(data):.2f}")
    print(f"方差: {np.var(data):.2f}")
    print(f"最小值: {np.min(data):.2f}")
    print(f"最大值: {np.max(data):.2f}")
    print(f"范围: {np.ptp(data):.2f}")
    
    # 分位数
    print(f"\n分位数:")
    print(f"25%分位数: {np.percentile(data, 25):.2f}")
    print(f"50%分位数: {np.percentile(data, 50):.2f}")
    print(f"75%分位数: {np.percentile(data, 75):.2f}")
    
    # 其他统计
    print(f"\n其他统计:")
    print(f"总和: {np.sum(data):.2f}")
    print(f"乘积: {np.prod(data[:10]):.2e}")  # 只计算前10个
    print(f"累积和: {np.cumsum(data[:10])}")

def array_operations_demo():
    """数组操作演示"""
    
    print("\n=== 数组操作演示 ===")
    
    # 创建测试数据
    arr1 = np.array([1, 2, 3, 4, 5])
    arr2 = np.array([2, 3, 4, 5, 6])
    
    print(f"数组1: {arr1}")
    print(f"数组2: {arr2}")
    
    # 基本运算
    print(f"\n基本运算:")
    print(f"加法: {arr1 + arr2}")
    print(f"减法: {arr1 - arr2}")
    print(f"乘法: {arr1 * arr2}")
    print(f"除法: {arr1 / arr2}")
    print(f"幂运算: {arr1 ** arr2}")
    
    # 比较运算
    print(f"\n比较运算:")
    print(f"大于: {arr1 > arr2}")
    print(f"等于: {arr1 == arr2}")
    print(f"小于等于: {arr1 <= arr2}")
    
    # 逻辑运算
    print(f"\n逻辑运算:")
    print(f"逻辑与: {np.logical_and(arr1 > 2, arr2 < 5)}")
    print(f"逻辑或: {np.logical_or(arr1 > 3, arr2 < 4)}")
    print(f"逻辑非: {np.logical_not(arr1 > 3)}")

def broadcasting_demo():
    """广播机制演示"""
    
    print("\n=== 广播机制演示 ===")
    
    # 创建不同形状的数组
    arr1 = np.array([[1, 2, 3], [4, 5, 6]])  # (2, 3)
    arr2 = np.array([10, 20, 30])             # (3,)
    arr3 = np.array([[100], [200]])           # (2, 1)
    
    print(f"数组1 (2,3):\n{arr1}")
    print(f"数组2 (3,): {arr2}")
    print(f"数组3 (2,1):\n{arr3}")
    
    # 广播运算
    print(f"\n广播运算:")
    print(f"arr1 + arr2:\n{arr1 + arr2}")
    print(f"arr1 + arr3:\n{arr1 + arr3}")
    print(f"arr1 * arr2:\n{arr1 * arr2}")
    print(f"arr1 * arr3:\n{arr1 * arr3}")

def main():
    """主函数"""
    performance_comparison()
    mathematical_functions_demo()
    statistical_functions_demo()
    array_operations_demo()
    broadcasting_demo()

if __name__ == "__main__":
    main()
```

### 🎯 最佳实践

1. **使用向量化运算**：避免Python循环
2. **合理选择数据类型**：减少内存使用
3. **利用广播机制**：简化数组操作
4. **注意数值稳定性**：避免溢出和下溢
5. **使用NumPy函数**：而不是Python内置函数

通过掌握NumPy的数学运算功能，你就能高效地进行科学计算和数据分析！
