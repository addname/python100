# 第二章：数据结构与类型

!!! info "数据结构基础"
    本章将深入学习Python的核心数据结构，包括列表、元组、字典、集合和字符串。这些数据结构是Python编程的基础，掌握它们对于编写高效的程序至关重要。

## 问题21：Python中的列表有哪些特点和用法？

### 🤔 问题描述
列表是Python中最常用的数据结构之一，它有哪些特点？如何创建和操作列表？列表与其他数据结构有什么区别？

### 💡 详细解答

#### 列表的基本特点

列表（List）是Python中的有序集合，具有以下特点：

1. **有序性**：元素按插入顺序排列
2. **可变性**：可以修改、添加、删除元素
3. **异构性**：可以包含不同类型的元素
4. **索引访问**：支持正向和反向索引

#### 创建列表

```python
# 1. 空列表
empty_list = []
empty_list = list()

# 2. 包含元素的列表
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]
nested = [[1, 2], [3, 4], [5, 6]]

# 3. 使用list()构造函数
chars = list("hello")  # ['h', 'e', 'l', 'l', 'o']
range_list = list(range(5))  # [0, 1, 2, 3, 4]
```

#### 列表操作

```python
# 访问元素
numbers = [1, 2, 3, 4, 5]
print(numbers[0])    # 1 (第一个元素)
print(numbers[-1])   # 5 (最后一个元素)
print(numbers[1:3])  # [2, 3] (切片)

# 修改元素
numbers[0] = 10
print(numbers)  # [10, 2, 3, 4, 5]

# 添加元素
numbers.append(6)        # 末尾添加
numbers.insert(0, 0)     # 指定位置插入
numbers.extend([7, 8])   # 扩展列表

# 删除元素
del numbers[0]           # 删除指定位置
numbers.remove(3)        # 删除指定值
popped = numbers.pop()   # 删除并返回最后一个元素
```

### 📝 代码示例

```python
# 列表操作综合示例
def demonstrate_lists():
    """演示列表的各种操作"""
    
    # 创建列表
    fruits = ["apple", "banana", "orange"]
    print(f"原始列表: {fruits}")
    
    # 添加元素
    fruits.append("grape")
    fruits.insert(1, "mango")
    print(f"添加后: {fruits}")
    
    # 删除元素
    fruits.remove("banana")
    last_fruit = fruits.pop()
    print(f"删除后: {fruits}")
    print(f"删除的元素: {last_fruit}")
    
    # 列表推导式
    numbers = [1, 2, 3, 4, 5]
    squares = [x**2 for x in numbers]
    even_squares = [x**2 for x in numbers if x % 2 == 0]
    
    print(f"平方数: {squares}")
    print(f"偶数平方: {even_squares}")
    
    # 列表方法
    numbers = [3, 1, 4, 1, 5, 9, 2, 6]
    print(f"排序前: {numbers}")
    numbers.sort()
    print(f"排序后: {numbers}")
    
    # 统计
    print(f"元素个数: {len(numbers)}")
    print(f"最大值: {max(numbers)}")
    print(f"最小值: {min(numbers)}")
    print(f"求和: {sum(numbers)}")

if __name__ == "__main__":
    demonstrate_lists()
```

---

## 问题22：如何高效地操作列表？

### 🤔 问题描述
在实际编程中，如何高效地操作列表？有哪些性能优化的技巧？如何避免常见的列表操作陷阱？

### 💡 详细解答

#### 性能优化技巧

=== "使用列表推导式"
    ```python
    # 传统方式 - 较慢
    squares = []
    for x in range(1000):
        squares.append(x**2)
    
    # 列表推导式 - 更快
    squares = [x**2 for x in range(1000)]
    
    # 带条件的列表推导式
    even_squares = [x**2 for x in range(1000) if x % 2 == 0]
    ```

=== "避免频繁的列表重建"
    ```python
    # 低效 - 频繁重建列表
    result = []
    for i in range(1000):
        result = result + [i]  # 创建新列表
    
    # 高效 - 使用append
    result = []
    for i in range(1000):
        result.append(i)  # 原地修改
    
    # 最高效 - 预分配空间
    result = [0] * 1000
    for i in range(1000):
        result[i] = i
    ```

=== "使用适当的数据结构"
    ```python
    # 频繁查找 - 使用集合
    items = [1, 2, 3, 4, 5]
    item_set = set(items)  # O(1)查找
    
    if 3 in item_set:  # 快速查找
        print("找到元素")
    
    # 频繁插入删除 - 考虑使用deque
    from collections import deque
    queue = deque([1, 2, 3])
    queue.appendleft(0)  # O(1)左端插入
    queue.append(4)      # O(1)右端插入
    ```

#### 常见陷阱和解决方案

=== "浅拷贝vs深拷贝"
    ```python
    # 浅拷贝问题
    original = [[1, 2], [3, 4]]
    copy_list = original.copy()  # 浅拷贝
    copy_list[0][0] = 999
    print(original)  # [[999, 2], [3, 4]] - 原列表也被修改！
    
    # 深拷贝解决方案
    import copy
    original = [[1, 2], [3, 4]]
    deep_copy = copy.deepcopy(original)
    deep_copy[0][0] = 999
    print(original)  # [[1, 2], [3, 4]] - 原列表不受影响
    ```

=== "列表作为默认参数"
    ```python
    # 错误的方式
    def add_item(item, my_list=[]):  # 危险！
        my_list.append(item)
        return my_list
    
    # 正确的方式
    def add_item(item, my_list=None):
        if my_list is None:
            my_list = []
        my_list.append(item)
        return my_list
    ```

### 📝 代码示例

```python
# 高效列表操作示例
import time
from collections import deque

def performance_comparison():
    """性能对比示例"""
    
    # 1. 列表推导式 vs 传统循环
    n = 100000
    
    # 传统方式
    start = time.time()
    squares1 = []
    for i in range(n):
        squares1.append(i**2)
    time1 = time.time() - start
    
    # 列表推导式
    start = time.time()
    squares2 = [i**2 for i in range(n)]
    time2 = time.time() - start
    
    print(f"传统方式耗时: {time1:.4f}秒")
    print(f"列表推导式耗时: {time2:.4f}秒")
    print(f"性能提升: {time1/time2:.2f}倍")

def list_operations_demo():
    """列表操作演示"""
    
    # 创建测试数据
    numbers = list(range(10))
    print(f"原始列表: {numbers}")
    
    # 切片操作
    print(f"前5个元素: {numbers[:5]}")
    print(f"后5个元素: {numbers[-5:]}")
    print(f"每隔2个取一个: {numbers[::2]}")
    print(f"反转列表: {numbers[::-1]}")
    
    # 列表方法
    numbers.append(10)
    numbers.insert(0, -1)
    print(f"添加元素后: {numbers}")
    
    # 删除操作
    removed = numbers.pop(0)  # 删除第一个元素
    numbers.remove(5)         # 删除值为5的元素
    print(f"删除后: {numbers}")
    print(f"删除的元素: {removed}")
    
    # 排序和反转
    numbers.sort(reverse=True)
    print(f"降序排列: {numbers}")
    
    # 统计信息
    print(f"长度: {len(numbers)}")
    print(f"最大值: {max(numbers)}")
    print(f"最小值: {min(numbers)}")
    print(f"求和: {sum(numbers)}")
    print(f"平均值: {sum(numbers)/len(numbers):.2f}")

def advanced_list_techniques():
    """高级列表技巧"""
    
    # 1. 列表推导式的高级用法
    matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    
    # 展平二维列表
    flattened = [item for row in matrix for item in row]
    print(f"展平矩阵: {flattened}")
    
    # 转置矩阵
    transposed = [[row[i] for row in matrix] for i in range(len(matrix[0]))]
    print(f"转置矩阵: {transposed}")
    
    # 2. 过滤和映射
    numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    
    # 过滤偶数
    evens = [x for x in numbers if x % 2 == 0]
    print(f"偶数: {evens}")
    
    # 映射操作
    squares = [x**2 for x in numbers]
    print(f"平方数: {squares}")
    
    # 3. 条件列表推导式
    result = ["偶数" if x % 2 == 0 else "奇数" for x in range(1, 6)]
    print(f"奇偶判断: {result}")
    
    # 4. 嵌套列表推导式
    nested = [[i*j for j in range(1, 4)] for i in range(1, 4)]
    print(f"乘法表: {nested}")

def list_algorithms():
    """列表算法示例"""
    
    # 1. 查找算法
    def linear_search(lst, target):
        """线性查找"""
        for i, item in enumerate(lst):
            if item == target:
                return i
        return -1
    
    # 2. 排序算法（冒泡排序）
    def bubble_sort(lst):
        """冒泡排序"""
        n = len(lst)
        for i in range(n):
            for j in range(0, n-i-1):
                if lst[j] > lst[j+1]:
                    lst[j], lst[j+1] = lst[j+1], lst[j]
        return lst
    
    # 3. 去重算法
    def remove_duplicates(lst):
        """去除重复元素（保持顺序）"""
        seen = set()
        result = []
        for item in lst:
            if item not in seen:
                seen.add(item)
                result.append(item)
        return result
    
    # 测试算法
    test_list = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3]
    print(f"原始列表: {test_list}")
    
    # 查找
    index = linear_search(test_list, 5)
    print(f"查找5的位置: {index}")
    
    # 排序
    sorted_list = bubble_sort(test_list.copy())
    print(f"排序后: {sorted_list}")
    
    # 去重
    unique_list = remove_duplicates(test_list)
    print(f"去重后: {unique_list}")

if __name__ == "__main__":
    print("=== 性能对比 ===")
    performance_comparison()
    
    print("\n=== 列表操作演示 ===")
    list_operations_demo()
    
    print("\n=== 高级技巧 ===")
    advanced_list_techniques()
    
    print("\n=== 列表算法 ===")
    list_algorithms()
```

### 🎯 最佳实践

1. **优先使用列表推导式**：比传统循环更高效
2. **避免频繁的列表重建**：使用append而不是+
3. **注意浅拷贝陷阱**：需要深拷贝时使用copy.deepcopy()
4. **合理使用切片**：切片操作很高效
5. **预分配空间**：已知大小时预分配列表
6. **选择合适的数据结构**：根据使用场景选择

通过掌握这些列表操作技巧，你就能编写出更高效、更优雅的Python代码！
