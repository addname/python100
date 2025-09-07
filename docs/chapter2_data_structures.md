# 第二章：数据结构

本章介绍Python中的核心数据结构：列表、元组、字典和集合，以及它们的操作和应用。

---

## 13. 如何创建和访问列表？

**答：**
列表是Python中最常用的数据结构，可以存储多个元素。

### 创建列表
```python
# 空列表
empty_list = []
empty_list = list()

# 包含元素的列表
numbers = [1, 2, 3, 4, 5]
fruits = ['apple', 'banana', 'orange']
mixed = [1, 'hello', 3.14, True]

# 使用list()函数
numbers = list(range(1, 6))  # [1, 2, 3, 4, 5]
```

### 访问列表元素
```python
fruits = ['apple', 'banana', 'orange', 'grape']

# 通过索引访问（从0开始）
first_fruit = fruits[0]    # 'apple'
second_fruit = fruits[1]   # 'banana'
last_fruit = fruits[-1]    # 'grape'（倒数第一个）

# 切片访问
first_two = fruits[0:2]    # ['apple', 'banana']
last_two = fruits[-2:]     # ['orange', 'grape']
all_fruits = fruits[:]     # 复制整个列表
```

### 修改列表元素
```python
fruits = ['apple', 'banana', 'orange']

# 修改单个元素
fruits[1] = 'grape'  # ['apple', 'grape', 'orange']

# 修改多个元素
fruits[0:2] = ['pear', 'kiwi']  # ['pear', 'kiwi', 'orange']
```

---

## 14. 列表的增删改查？

**答：**
列表提供了丰富的增删改查操作：

### 增加元素
```python
fruits = ['apple', 'banana']

# append()：在末尾添加一个元素
fruits.append('orange')  # ['apple', 'banana', 'orange']

# insert()：在指定位置插入元素
fruits.insert(1, 'grape')  # ['apple', 'grape', 'banana', 'orange']

# extend()：添加多个元素
fruits.extend(['kiwi', 'mango'])  # ['apple', 'grape', 'banana', 'orange', 'kiwi', 'mango']

# 使用+号连接
new_fruits = fruits + ['pear']  # 创建新列表
```

### 删除元素
```python
fruits = ['apple', 'banana', 'orange', 'banana']

# remove()：删除第一个匹配的元素
fruits.remove('banana')  # ['apple', 'orange', 'banana']

# pop()：删除并返回指定位置的元素
removed = fruits.pop(1)  # 删除'orange'，fruits变为['apple', 'banana']

# del：删除指定位置的元素
del fruits[0]  # 删除'apple'

# clear()：清空列表
fruits.clear()  # []
```

### 修改元素
```python
fruits = ['apple', 'banana', 'orange']

# 直接赋值修改
fruits[1] = 'grape'  # ['apple', 'grape', 'orange']

# 切片修改
fruits[0:2] = ['pear', 'kiwi']  # ['pear', 'kiwi', 'orange']
```

### 查找元素
```python
fruits = ['apple', 'banana', 'orange', 'banana']

# index()：查找元素第一次出现的位置
position = fruits.index('banana')  # 1

# count()：统计元素出现次数
count = fruits.count('banana')  # 2

# in操作符：检查元素是否存在
exists = 'apple' in fruits  # True
```

---

## 15. 列表的排序和切片？

**答：**
列表支持排序和切片操作：

### 排序操作
```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

# sort()：原地排序（修改原列表）
numbers.sort()  # [1, 1, 2, 3, 4, 5, 6, 9]

# sort(reverse=True)：降序排序
numbers.sort(reverse=True)  # [9, 6, 5, 4, 3, 2, 1, 1]

# sorted()：返回新排序列表（不修改原列表）
original = [3, 1, 4, 1, 5]
sorted_list = sorted(original)  # [1, 1, 3, 4, 5]
# original仍然是[3, 1, 4, 1, 5]

# 自定义排序
students = [('Alice', 85), ('Bob', 90), ('Charlie', 78)]
students.sort(key=lambda x: x[1])  # 按分数排序
```

### 切片操作
```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# 基本切片：[start:end]
first_half = numbers[0:5]    # [0, 1, 2, 3, 4]
second_half = numbers[5:]    # [5, 6, 7, 8, 9]

# 步长切片：[start:end:step]
even_numbers = numbers[0::2]  # [0, 2, 4, 6, 8]
odd_numbers = numbers[1::2]   # [1, 3, 5, 7, 9]

# 反向切片
reversed_list = numbers[::-1]  # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

# 切片赋值
numbers[0:3] = [10, 20, 30]  # [10, 20, 30, 3, 4, 5, 6, 7, 8, 9]
```

### 其他常用操作
```python
numbers = [1, 2, 3, 4, 5]

# reverse()：原地反转
numbers.reverse()  # [5, 4, 3, 2, 1]

# len()：获取长度
length = len(numbers)  # 5

# max()和min()：最大值和最小值
max_value = max(numbers)  # 5
min_value = min(numbers)  # 1

# sum()：求和
total = sum(numbers)  # 15
```

---

## 16. 元组和列表的区别？

**答：**
元组和列表是Python中两种重要的序列类型，它们有重要区别：

### 主要区别

| 特性 | 列表 (list) | 元组 (tuple) |
|------|-------------|--------------|
| 可变性 | 可变（mutable） | 不可变（immutable） |
| 语法 | 使用方括号 `[]` | 使用圆括号 `()` |
| 性能 | 较慢 | 较快 |
| 内存占用 | 较大 | 较小 |
| 安全性 | 较低 | 较高 |

### 代码示例
```python
# 列表：可变
my_list = [1, 2, 3]
my_list[0] = 10  # 可以修改
my_list.append(4)  # 可以添加元素
print(my_list)  # [10, 2, 3, 4]

# 元组：不可变
my_tuple = (1, 2, 3)
# my_tuple[0] = 10  # 错误！不能修改
# my_tuple.append(4)  # 错误！没有append方法
print(my_tuple)  # (1, 2, 3)
```

### 创建元组
```python
# 空元组
empty_tuple = ()
empty_tuple = tuple()

# 单元素元组（注意逗号）
single_tuple = (42,)  # 必须有逗号
not_tuple = (42)      # 这不是元组，是整数

# 多元素元组
coordinates = (10, 20)
colors = ('red', 'green', 'blue')
```

### 何时使用元组
```python
# 1. 坐标点
point = (10, 20)

# 2. 数据库记录
user = ('Alice', 25, 'alice@example.com')

# 3. 函数返回多个值
def get_name_age():
    return 'Bob', 30

name, age = get_name_age()

# 4. 字典的键（元组可以作为字典的键，列表不行）
locations = {
    (0, 0): 'origin',
    (1, 1): 'corner'
}
```

---

## 17. 如何创建和使用元组？

**答：**
元组是不可变的序列类型，适合存储不会改变的数据：

### 创建元组
```python
# 使用圆括号
coordinates = (10, 20)
colors = ('red', 'green', 'blue')

# 使用tuple()函数
numbers = tuple([1, 2, 3, 4, 5])
empty_tuple = tuple()

# 单元素元组（必须有逗号）
single = (42,)

# 无括号创建（逗号分隔）
point = 10, 20  # 自动创建元组
```

### 访问元组元素
```python
colors = ('red', 'green', 'blue')

# 通过索引访问
first_color = colors[0]   # 'red'
last_color = colors[-1]   # 'blue'

# 切片访问
first_two = colors[0:2]   # ('red', 'green')
last_two = colors[-2:]    # ('green', 'blue')
```

### 元组操作
```python
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)

# 连接元组
combined = tuple1 + tuple2  # (1, 2, 3, 4, 5, 6)

# 重复元组
repeated = tuple1 * 3  # (1, 2, 3, 1, 2, 3, 1, 2, 3)

# 检查元素是否存在
exists = 2 in tuple1  # True

# 获取长度
length = len(tuple1)  # 3

# 查找元素位置
position = tuple1.index(2)  # 1

# 统计元素出现次数
count = tuple1.count(1)  # 1
```

### 元组解包
```python
# 基本解包
point = (10, 20)
x, y = point  # x=10, y=20

# 多值解包
data = (1, 2, 3, 4, 5)
first, *middle, last = data  # first=1, middle=[2,3,4], last=5

# 函数返回多值
def get_coordinates():
    return 10, 20

x, y = get_coordinates()

# 交换变量
a, b = 1, 2
a, b = b, a  # a=2, b=1
```

---

## 18. 元组的应用场景？

**答：**
元组在Python中有多种重要应用场景：

### 1. 坐标和几何数据
```python
# 2D坐标
point = (10, 20)
rectangle = ((0, 0), (10, 10))

# 3D坐标
point_3d = (1, 2, 3)

# RGB颜色
color = (255, 128, 0)
```

### 2. 数据库记录
```python
# 用户信息
user = ('Alice', 25, 'alice@example.com', 'Engineer')

# 解包使用
name, age, email, job = user
print(f"姓名：{name}，年龄：{age}")
```

### 3. 函数返回多个值
```python
def calculate_stats(numbers):
    return min(numbers), max(numbers), sum(numbers) / len(numbers)

data = [1, 2, 3, 4, 5]
min_val, max_val, avg_val = calculate_stats(data)
```

### 4. 字典的键
```python
# 元组可以作为字典的键（列表不行）
locations = {
    (0, 0): 'origin',
    (1, 1): 'corner',
    (2, 3): 'center'
}

# 访问
position = locations[(1, 1)]  # 'corner'
```

### 5. 配置和常量
```python
# 配置信息
DATABASE_CONFIG = ('localhost', 5432, 'mydb', 'user', 'password')

# 常量组合
STATUS_CODES = (200, 404, 500)
HTTP_METHODS = ('GET', 'POST', 'PUT', 'DELETE')
```

### 6. 函数参数传递
```python
def draw_line(start, end, color):
    print(f"从{start}到{end}画线，颜色{color}")

# 使用元组传递坐标
start_point = (0, 0)
end_point = (10, 10)
color = (255, 0, 0)

draw_line(start_point, end_point, color)
```

### 7. 数据交换
```python
# 交换变量值
a, b = 1, 2
a, b = b, a  # a=2, b=1

# 批量赋值
x, y, z = 1, 2, 3
```

### 8. 不可变集合
```python
# 当需要不可变的序列时
valid_extensions = ('.jpg', '.png', '.gif', '.bmp')
weekdays = ('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday')
```

---

## 19. 如何创建和访问字典？

**答：**
字典是Python中的映射类型，存储键值对数据：

### 创建字典
```python
# 空字典
empty_dict = {}
empty_dict = dict()

# 包含键值对的字典
person = {
    'name': 'Alice',
    'age': 25,
    'city': 'Beijing'
}

# 使用dict()函数
person = dict(name='Alice', age=25, city='Beijing')

# 从列表创建
keys = ['name', 'age', 'city']
values = ['Alice', 25, 'Beijing']
person = dict(zip(keys, values))
```

### 访问字典元素
```python
person = {'name': 'Alice', 'age': 25, 'city': 'Beijing'}

# 使用方括号访问
name = person['name']  # 'Alice'
age = person['age']    # 25

# 使用get()方法（推荐）
name = person.get('name')        # 'Alice'
email = person.get('email')      # None（键不存在）
email = person.get('email', 'N/A')  # 'N/A'（提供默认值）

# 检查键是否存在
if 'name' in person:
    print(person['name'])
```

### 修改字典
```python
person = {'name': 'Alice', 'age': 25}

# 添加新键值对
person['city'] = 'Beijing'
person['email'] = 'alice@example.com'

# 修改现有值
person['age'] = 26

# 使用update()方法批量更新
person.update({
    'job': 'Engineer',
    'salary': 50000
})
```

---

## 20. 字典的增删改查？

**答：**
字典提供了完整的增删改查操作：

### 增加操作
```python
person = {'name': 'Alice'}

# 直接赋值添加
person['age'] = 25
person['city'] = 'Beijing'

# 使用setdefault()（如果键不存在才添加）
person.setdefault('country', 'China')
person.setdefault('name', 'Bob')  # 不会覆盖，因为'name'已存在

# 使用update()批量添加
person.update({
    'job': 'Engineer',
    'salary': 50000
})
```

### 删除操作
```python
person = {'name': 'Alice', 'age': 25, 'city': 'Beijing'}

# del语句删除
del person['age']

# pop()删除并返回值
removed_value = person.pop('city')  # 返回'Beijing'

# popitem()删除并返回最后一个键值对
key, value = person.popitem()

# clear()清空字典
person.clear()  # {}
```

### 修改操作
```python
person = {'name': 'Alice', 'age': 25}

# 直接赋值修改
person['age'] = 26

# 使用update()批量修改
person.update({'age': 27, 'city': 'Shanghai'})
```

### 查找操作
```python
person = {'name': 'Alice', 'age': 25, 'city': 'Beijing'}

# 检查键是否存在
exists = 'name' in person  # True

# 获取所有键
keys = person.keys()  # dict_keys(['name', 'age', 'city'])

# 获取所有值
values = person.values()  # dict_values(['Alice', 25, 'Beijing'])

# 获取所有键值对
items = person.items()  # dict_items([('name', 'Alice'), ('age', 25), ('city', 'Beijing')])

# 获取字典长度
length = len(person)  # 3
```

---

## 21. 字典的遍历方法？

**答：**
字典提供了多种遍历方法：

### 遍历键
```python
person = {'name': 'Alice', 'age': 25, 'city': 'Beijing'}

# 方法1：直接遍历字典（默认遍历键）
for key in person:
    print(key, person[key])

# 方法2：使用keys()方法
for key in person.keys():
    print(key, person[key])

# 方法3：使用enumerate()获取索引
for i, key in enumerate(person.keys()):
    print(f"{i}: {key} = {person[key]}")
```

### 遍历值
```python
person = {'name': 'Alice', 'age': 25, 'city': 'Beijing'}

# 遍历所有值
for value in person.values():
    print(value)

# 遍历值并获取索引
for i, value in enumerate(person.values()):
    print(f"{i}: {value}")
```

### 遍历键值对
```python
person = {'name': 'Alice', 'age': 25, 'city': 'Beijing'}

# 方法1：使用items()
for key, value in person.items():
    print(f"{key}: {value}")

# 方法2：同时遍历键和值
for key in person:
    value = person[key]
    print(f"{key}: {value}")
```

### 字典推导式
```python
# 创建新字典
squares = {x: x**2 for x in range(1, 6)}
# {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# 过滤字典
person = {'name': 'Alice', 'age': 25, 'city': 'Beijing', 'salary': 50000}
filtered = {k: v for k, v in person.items() if isinstance(v, str)}
# {'name': 'Alice', 'city': 'Beijing'}

# 转换值
person = {'name': 'Alice', 'age': 25}
upper_person = {k: v.upper() if isinstance(v, str) else v for k, v in person.items()}
# {'name': 'ALICE', 'age': 25}
```

### 嵌套字典遍历
```python
students = {
    'Alice': {'age': 20, 'grade': 'A'},
    'Bob': {'age': 21, 'grade': 'B'},
    'Charlie': {'age': 19, 'grade': 'A'}
}

# 遍历嵌套字典
for name, info in students.items():
    print(f"学生：{name}")
    for key, value in info.items():
        print(f"  {key}: {value}")
```

---

## 22. 集合的特点和用途？

**答：**
集合是Python中的无序、不重复元素的数据结构：

### 集合的特点
```python
# 1. 无序性：元素没有固定顺序
my_set = {3, 1, 4, 1, 5, 9, 2, 6}
print(my_set)  # {1, 2, 3, 4, 5, 6, 9}（顺序可能不同）

# 2. 唯一性：不允许重复元素
my_set = {1, 2, 2, 3, 3, 3}
print(my_set)  # {1, 2, 3}

# 3. 可变性：可以添加和删除元素
my_set.add(4)
my_set.remove(1)
```

### 创建集合
```python
# 空集合（注意：{}是空字典，不是空集合）
empty_set = set()

# 包含元素的集合
numbers = {1, 2, 3, 4, 5}
fruits = {'apple', 'banana', 'orange'}

# 从列表创建集合（去重）
numbers = set([1, 2, 2, 3, 3, 4])  # {1, 2, 3, 4}

# 从字符串创建集合
chars = set('hello')  # {'h', 'e', 'l', 'o'}
```

### 集合的用途
```python
# 1. 去重
numbers = [1, 2, 2, 3, 3, 4, 4, 5]
unique_numbers = list(set(numbers))  # [1, 2, 3, 4, 5]

# 2. 成员测试（比列表快）
large_set = set(range(1000000))
if 999999 in large_set:  # O(1)时间复杂度
    print("存在")

# 3. 数学集合运算
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

# 并集
union = set1 | set2  # {1, 2, 3, 4, 5, 6, 7, 8}

# 交集
intersection = set1 & set2  # {4, 5}

# 差集
difference = set1 - set2  # {1, 2, 3}

# 对称差集
symmetric_diff = set1 ^ set2  # {1, 2, 3, 6, 7, 8}
```

---

## 23. 集合的运算操作？

**答：**
集合支持丰富的数学集合运算：

### 基本集合运算
```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

# 并集（union）
union1 = set1 | set2           # {1, 2, 3, 4, 5, 6, 7, 8}
union2 = set1.union(set2)      # 同上

# 交集（intersection）
intersection1 = set1 & set2    # {4, 5}
intersection2 = set1.intersection(set2)  # 同上

# 差集（difference）
diff1 = set1 - set2            # {1, 2, 3}
diff2 = set1.difference(set2)  # 同上

# 对称差集（symmetric difference）
sym_diff1 = set1 ^ set2                    # {1, 2, 3, 6, 7, 8}
sym_diff2 = set1.symmetric_difference(set2)  # 同上
```

### 集合关系判断
```python
set1 = {1, 2, 3}
set2 = {1, 2, 3, 4, 5}
set3 = {4, 5, 6}

# 子集判断
is_subset = set1.issubset(set2)     # True
is_subset = set1 <= set2            # True

# 真子集判断
is_proper_subset = set1 < set2      # True

# 超集判断
is_superset = set2.issuperset(set1) # True
is_superset = set2 >= set1          # True

# 真超集判断
is_proper_superset = set2 > set1    # True

# 不相交判断
is_disjoint = set1.isdisjoint(set3) # True
```

### 原地修改操作
```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

# 原地并集
set1 |= set2  # set1变为{1, 2, 3, 4, 5, 6, 7, 8}
set1.update(set2)  # 同上

# 原地交集
set1 &= set2  # set1变为{4, 5}
set1.intersection_update(set2)  # 同上

# 原地差集
set1 -= set2  # set1变为{1, 2, 3}
set1.difference_update(set2)  # 同上

# 原地对称差集
set1 ^= set2  # set1变为{1, 2, 3, 6, 7, 8}
set1.symmetric_difference_update(set2)  # 同上
```

---

## 24. 如何创建和操作集合？

**答：**
集合的创建和操作包括增删改查等基本操作：

### 创建集合
```python
# 空集合
empty_set = set()

# 包含元素的集合
numbers = {1, 2, 3, 4, 5}
fruits = {'apple', 'banana', 'orange'}

# 从其他数据结构创建
from_list = set([1, 2, 2, 3, 3])  # {1, 2, 3}（去重）
from_string = set('hello')         # {'h', 'e', 'l', 'o'}
from_tuple = set((1, 2, 3, 2))    # {1, 2, 3}

# 集合推导式
squares = {x**2 for x in range(1, 6)}  # {1, 4, 9, 16, 25}
```

### 添加元素
```python
my_set = {1, 2, 3}

# add()：添加单个元素
my_set.add(4)        # {1, 2, 3, 4}
my_set.add(2)        # {1, 2, 3, 4}（重复元素不会添加）

# update()：添加多个元素
my_set.update([5, 6, 7])  # {1, 2, 3, 4, 5, 6, 7}
my_set.update({8, 9})     # {1, 2, 3, 4, 5, 6, 7, 8, 9}
```

### 删除元素
```python
my_set = {1, 2, 3, 4, 5}

# remove()：删除指定元素（元素不存在会报错）
my_set.remove(3)     # {1, 2, 4, 5}

# discard()：删除指定元素（元素不存在不会报错）
my_set.discard(2)    # {1, 4, 5}
my_set.discard(10)   # {1, 4, 5}（不会报错）

# pop()：删除并返回任意一个元素
removed = my_set.pop()  # 返回1，my_set变为{4, 5}

# clear()：清空集合
my_set.clear()  # set()
```

### 查询操作
```python
my_set = {1, 2, 3, 4, 5}

# 检查元素是否存在
exists = 3 in my_set      # True
not_exists = 10 in my_set # False

# 获取集合长度
length = len(my_set)      # 5

# 检查集合是否为空
is_empty = len(my_set) == 0  # False
is_empty = not my_set        # False
```

### 集合转换
```python
my_set = {1, 2, 3, 4, 5}

# 转换为列表
my_list = list(my_set)    # [1, 2, 3, 4, 5]

# 转换为元组
my_tuple = tuple(my_set)  # (1, 2, 3, 4, 5)

# 转换为字符串
my_string = str(my_set)   # "{1, 2, 3, 4, 5}"
```

### 实际应用示例
```python
# 1. 去重
numbers = [1, 2, 2, 3, 3, 4, 4, 5]
unique_numbers = list(set(numbers))

# 2. 查找共同元素
list1 = [1, 2, 3, 4, 5]
list2 = [4, 5, 6, 7, 8]
common = set(list1) & set(list2)  # {4, 5}

# 3. 查找不同元素
different = set(list1) ^ set(list2)  # {1, 2, 3, 6, 7, 8}

# 4. 权限管理
user_permissions = {'read', 'write', 'execute'}
required_permissions = {'read', 'write'}
has_permission = required_permissions.issubset(user_permissions)
```
