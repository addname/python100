# 字典(Dictionary)的操作

## 问题1：什么是字典？字典有什么特点？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

字典(dict)是Python中的一种映射类型，用花括号 `{}` 表示，存储键值对：

```python
# 创建字典
person = {
    "name": "张三",
    "age": 25,
    "city": "北京"
}

print(type(person))  # <class 'dict'>
print(person)        # {'name': '张三', 'age': 25, 'city': '北京'}
```

### 字典的特点：
1. **键值对存储**：每个元素包含键(key)和值(value)
2. **键唯一性**：键必须唯一，值可以重复
3. **键不可变**：键必须是不可变类型(字符串、数字、元组)
4. **无序性**：Python 3.7+字典保持插入顺序
5. **可变性**：可以添加、删除、修改元素

## 问题2：如何创建和访问字典？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
# 1. 直接创建
empty_dict = {}
student = {"name": "李四", "age": 20, "grade": "A"}

# 2. 使用dict()函数
colors = dict(red="#FF0000", green="#00FF00", blue="#0000FF")
numbers = dict([("one", 1), ("two", 2), ("three", 3)])

# 3. 字典推导式
squares = {x: x**2 for x in range(1, 6)}
print(squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# 访问字典元素
print(student["name"])     # 李四
print(student.get("age"))  # 20
print(student.get("phone", "未知"))  # 未知 (默认值)

# 检查键是否存在
if "name" in student:
    print("姓名存在")
```

## 问题3：如何修改字典？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
# 添加新元素
student = {"name": "王五", "age": 22}
student["grade"] = "B"
student["phone"] = "13800138000"
print(student)  # {'name': '王五', 'age': 22, 'grade': 'B', 'phone': '13800138000'}

# 修改现有元素
student["age"] = 23
print(student["age"])  # 23

# 使用update()方法批量更新
student.update({
    "city": "上海",
    "major": "计算机科学"
})
print(student)

# 删除元素
del student["phone"]  # 删除指定键
removed_grade = student.pop("grade")  # 删除并返回值
print(f"删除的分数: {removed_grade}")

# 清空字典
student.clear()
print(student)  # {}
```

## 问题4：字典的常用方法有哪些？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
# 创建示例字典
inventory = {
    "苹果": 50,
    "香蕉": 30,
    "橙子": 25,
    "葡萄": 40
}

# 1. 获取所有键
print(list(inventory.keys()))  # ['苹果', '香蕉', '橙子', '葡萄']

# 2. 获取所有值
print(list(inventory.values()))  # [50, 30, 25, 40]

# 3. 获取所有键值对
print(list(inventory.items()))  # [('苹果', 50), ('香蕉', 30), ('橙子', 25), ('葡萄', 40)]

# 4. 获取字典长度
print(len(inventory))  # 4

# 5. 复制字典
inventory_copy = inventory.copy()
print(inventory_copy)

# 6. 设置默认值
inventory.setdefault("西瓜", 0)
print(inventory["西瓜"])  # 0

# 7. 弹出元素
apple_count = inventory.pop("苹果", 0)
print(f"苹果数量: {apple_count}")

# 8. 弹出最后一个元素 (Python 3.7+)
last_item = inventory.popitem()
print(f"最后一项: {last_item}")
```

## 问题5：如何遍历字典？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
# 示例字典
scores = {
    "数学": 95,
    "英语": 88,
    "物理": 92,
    "化学": 85
}

# 1. 遍历键
for subject in scores:
    print(f"科目: {subject}")

# 2. 遍历键
for subject in scores.keys():
    print(f"科目: {subject}")

# 3. 遍历值
for score in scores.values():
    print(f"分数: {score}")

# 4. 遍历键值对
for subject, score in scores.items():
    print(f"{subject}: {score}")

# 5. 带索引的遍历
for i, (subject, score) in enumerate(scores.items()):
    print(f"{i+1}. {subject}: {score}")
```

## 问题6：嵌套字典如何处理？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
# 嵌套字典
students = {
    "001": {
        "name": "张三",
        "age": 20,
        "grades": {"数学": 95, "英语": 88}
    },
    "002": {
        "name": "李四", 
        "age": 21,
        "grades": {"数学": 92, "英语": 90}
    }
}

# 访问嵌套元素
print(students["001"]["name"])  # 张三
print(students["001"]["grades"]["数学"])  # 95

# 修改嵌套元素
students["001"]["age"] = 21
students["001"]["grades"]["物理"] = 88

# 添加新的学生
students["003"] = {
    "name": "王五",
    "age": 19,
    "grades": {"数学": 89, "英语": 85}
}

# 遍历嵌套字典
for student_id, info in students.items():
    print(f"学号: {student_id}")
    print(f"姓名: {info['name']}")
    print(f"年龄: {info['age']}")
    print("成绩:")
    for subject, grade in info["grades"].items():
        print(f"  {subject}: {grade}")
    print("-" * 20)
```

## 问题7：字典推导式如何使用？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
# 基本字典推导式
squares = {x: x**2 for x in range(1, 6)}
print(squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# 带条件的字典推导式
even_squares = {x: x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)  # {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}

# 字符串处理
words = ["hello", "world", "python", "programming"]
word_lengths = {word: len(word) for word in words}
print(word_lengths)  # {'hello': 5, 'world': 5, 'python': 6, 'programming': 11}

# 从两个列表创建字典
keys = ["name", "age", "city"]
values = ["张三", 25, "北京"]
person = {k: v for k, v in zip(keys, values)}
print(person)  # {'name': '张三', 'age': 25, 'city': '北京'}

# 字典转换
original = {"a": 1, "b": 2, "c": 3}
doubled = {k: v*2 for k, v in original.items()}
print(doubled)  # {'a': 2, 'b': 4, 'c': 6}
```

## 问题8：字典的实际应用场景有哪些？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
# 1. 配置管理
config = {
    "database": {
        "host": "localhost",
        "port": 3306,
        "username": "admin",
        "password": "secret"
    },
    "app": {
        "debug": True,
        "version": "1.0.0"
    }
}

# 2. 缓存系统
cache = {}

def expensive_calculation(n):
    if n in cache:
        print(f"从缓存获取: {n}")
        return cache[n]
    
    result = n ** 2  # 模拟复杂计算
    cache[n] = result
    print(f"计算结果: {n}")
    return result

# 3. 计数器
def count_words(text):
    words = text.split()
    word_count = {}
    
    for word in words:
        word_count[word] = word_count.get(word, 0) + 1
    
    return word_count

text = "python is great python is powerful"
result = count_words(text)
print(result)  # {'python': 2, 'is': 2, 'great': 1, 'powerful': 1}

# 4. 数据分组
students = [
    {"name": "张三", "grade": "A"},
    {"name": "李四", "grade": "B"},
    {"name": "王五", "grade": "A"},
    {"name": "赵六", "grade": "C"}
]

# 按成绩分组
grade_groups = {}
for student in students:
    grade = student["grade"]
    if grade not in grade_groups:
        grade_groups[grade] = []
    grade_groups[grade].append(student["name"])

print(grade_groups)  # {'A': ['张三', '王五'], 'B': ['李四'], 'C': ['赵六']}
```

## 问题9：字典的性能特点是什么？

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
import time

# 字典查找性能测试
large_dict = {i: i**2 for i in range(1000000)}

# 测试查找性能
start_time = time.time()
for i in range(1000):
    _ = large_dict.get(500000)
dict_time = time.time() - start_time

print(f"字典查找1000次耗时: {dict_time:.6f}秒")

# 列表查找性能对比
large_list = list(range(1000000))
start_time = time.time()
for i in range(1000):
    _ = 500000 in large_list
list_time = time.time() - start_time

print(f"列表查找1000次耗时: {list_time:.6f}秒")
print(f"字典比列表快 {list_time/dict_time:.1f} 倍")
```

## 问题10：字典的最佳实践

### 🤔 问题描述

### 💡 详细解答

### 📝 代码示例

```python
# 1. 使用get()方法避免KeyError
def safe_get_value(data, key, default=None):
    return data.get(key, default)

# 2. 使用setdefault()设置默认值
def add_to_group(groups, group_name, member):
    groups.setdefault(group_name, []).append(member)

# 3. 使用collections.defaultdict
from collections import defaultdict

# 自动创建默认值
dd = defaultdict(list)
dd["fruits"].append("apple")
dd["fruits"].append("banana")
print(dict(dd))  # {'fruits': ['apple', 'banana']}

# 4. 使用collections.Counter计数
from collections import Counter

text = "hello world"
counter = Counter(text)
print(counter)  # Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})

# 5. 字典合并 (Python 3.9+)
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}
merged = dict1 | dict2  # 新语法
print(merged)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# 6. 字典解包
def print_person(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_person(name="张三", age=25, city="北京")
```

## 总结

字典是Python中非常重要的数据结构，主要特点：
- **键值对存储**：高效的查找和存储
- **可变性**：支持增删改操作
- **唯一键**：键必须唯一且不可变
- **高性能**：平均O(1)的查找时间复杂度

适用场景：
- 配置管理
- 缓存系统
- 数据分组
- 计数器
- 映射关系存储
