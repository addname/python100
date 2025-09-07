# for循环与while循环

## 问题69：Python中有哪些循环语句？

Python中有两种主要的循环语句：

### 1. for循环
```python
# 基本for循环
fruits = ["苹果", "香蕉", "橙子"]
for fruit in fruits:
    print(fruit)

# 使用range()函数
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# 指定范围
for i in range(1, 6):
    print(i)  # 1, 2, 3, 4, 5

# 指定步长
for i in range(0, 10, 2):
    print(i)  # 0, 2, 4, 6, 8
```

### 2. while循环
```python
# 基本while循环
count = 0
while count < 5:
    print(count)
    count += 1

# 条件循环
password = ""
while password != "123456":
    password = input("请输入密码: ")
print("密码正确！")
```

## 问题70：for循环的常见用法有哪些？

```python
# 1. 遍历列表
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num * 2)

# 2. 遍历字符串
text = "Python"
for char in text:
    print(char)

# 3. 遍历字典
person = {"name": "张三", "age": 25, "city": "北京"}
for key, value in person.items():
    print(f"{key}: {value}")

# 4. 使用enumerate()获取索引
fruits = ["苹果", "香蕉", "橙子"]
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# 5. 使用zip()遍历多个序列
names = ["张三", "李四", "王五"]
ages = [25, 30, 28]
for name, age in zip(names, ages):
    print(f"{name}: {age}岁")
```

## 问题71：while循环的常见用法有哪些？

```python
# 1. 计数器循环
count = 0
while count < 3:
    print(f"第{count + 1}次循环")
    count += 1

# 2. 条件循环
import random
target = random.randint(1, 10)
guess = 0
while guess != target:
    guess = int(input("猜一个1-10的数字: "))
    if guess < target:
        print("太小了")
    elif guess > target:
        print("太大了")
print("猜对了！")

# 3. 无限循环（需要break退出）
while True:
    user_input = input("输入'quit'退出: ")
    if user_input.lower() == 'quit':
        break
    print(f"你输入了: {user_input}")

# 4. 文件读取
# 模拟文件读取
lines = ["第一行", "第二行", "第三行"]
index = 0
while index < len(lines):
    print(lines[index])
    index += 1
```

## 问题72：循环中的break和continue如何使用？

```python
# break - 跳出整个循环
for i in range(10):
    if i == 5:
        break
    print(i)  # 0, 1, 2, 3, 4

# continue - 跳过当前迭代
for i in range(5):
    if i == 2:
        continue
    print(i)  # 0, 1, 3, 4

# 实际应用示例
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for num in numbers:
    if num % 2 == 0:
        continue  # 跳过偶数
    if num > 7:
        break    # 遇到大于7的数就停止
    print(num)   # 1, 3, 5, 7
```

## 问题73：嵌套循环如何使用？

```python
# 基本嵌套循环
for i in range(3):
    for j in range(3):
        print(f"({i}, {j})")

# 打印乘法表
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j} × {i} = {i * j}", end="\t")
    print()  # 换行

# 二维列表遍历
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for row in matrix:
    for element in row:
        print(element, end=" ")
    print()
```

## 问题74：循环的else子句如何使用？

```python
# for循环的else子句
for i in range(5):
    print(i)
else:
    print("循环正常结束")

# 如果循环被break中断，else不会执行
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("这行不会执行")

# while循环的else子句
count = 0
while count < 3:
    print(count)
    count += 1
else:
    print("while循环正常结束")

# 实际应用：查找元素
def find_element(lst, target):
    for i, element in enumerate(lst):
        if element == target:
            print(f"找到元素 {target}，位置: {i}")
            break
    else:
        print(f"未找到元素 {target}")

find_element([1, 2, 3, 4, 5], 3)  # 找到元素 3，位置: 2
find_element([1, 2, 3, 4, 5], 6)  # 未找到元素 6
```

## 问题75：循环的性能优化技巧有哪些？

```python
# 1. 使用列表推导式替代简单循环
# 传统方式
squares = []
for i in range(10):
    squares.append(i**2)

# 列表推导式
squares = [i**2 for i in range(10)]

# 2. 使用生成器表达式处理大数据
# 传统方式（占用大量内存）
large_list = [i**2 for i in range(1000000)]

# 生成器表达式（节省内存）
large_generator = (i**2 for i in range(1000000))

# 3. 使用enumerate()替代range(len())
# 不推荐
fruits = ["苹果", "香蕉", "橙子"]
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# 推荐
for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")

# 4. 使用zip()处理多个序列
# 不推荐
names = ["张三", "李四", "王五"]
ages = [25, 30, 28]
for i in range(len(names)):
    print(f"{names[i]}: {ages[i]}岁")

# 推荐
for name, age in zip(names, ages):
    print(f"{name}: {age}岁")
```

## 问题76：循环的实际应用场景有哪些？

```python
# 1. 数据处理
def process_scores(scores):
    total = 0
    count = 0
    for score in scores:
        if score >= 0:  # 过滤无效分数
            total += score
            count += 1
    return total / count if count > 0 else 0

# 2. 文件处理
def count_lines(filename):
    try:
        with open(filename, 'r', encoding='utf-8') as file:
            count = 0
            for line in file:
                count += 1
        return count
    except FileNotFoundError:
        return 0

# 3. 用户输入验证
def get_valid_input():
    while True:
        try:
            number = int(input("请输入一个正整数: "))
            if number > 0:
                return number
            else:
                print("请输入正整数")
        except ValueError:
            print("请输入有效数字")

# 4. 游戏循环
def number_guessing_game():
    import random
    target = random.randint(1, 100)
    attempts = 0
    
    while attempts < 7:  # 最多7次机会
        guess = int(input("猜一个1-100的数字: "))
        attempts += 1
        
        if guess == target:
            print(f"恭喜！你用了{attempts}次猜对了！")
            return
        elif guess < target:
            print("太小了")
        else:
            print("太大了")
    
    print(f"游戏结束！答案是{target}")

# 5. 数据统计
def analyze_data(data):
    stats = {
        'count': 0,
        'sum': 0,
        'max': float('-inf'),
        'min': float('inf')
    }
    
    for value in data:
        stats['count'] += 1
        stats['sum'] += value
        stats['max'] = max(stats['max'], value)
        stats['min'] = min(stats['min'], value)
    
    stats['average'] = stats['sum'] / stats['count']
    return stats
```

## 问题77：如何避免常见的循环错误？

```python
# 1. 避免在循环中修改列表
# 错误做法
numbers = [1, 2, 3, 4, 5]
for i in range(len(numbers)):
    if numbers[i] % 2 == 0:
        numbers.remove(numbers[i])  # 这会导致索引错误

# 正确做法1：倒序遍历
numbers = [1, 2, 3, 4, 5]
for i in range(len(numbers) - 1, -1, -1):
    if numbers[i] % 2 == 0:
        numbers.pop(i)

# 正确做法2：创建新列表
numbers = [1, 2, 3, 4, 5]
numbers = [x for x in numbers if x % 2 != 0]

# 2. 避免无限循环
# 错误做法
# count = 0
# while count < 5:
#     print(count)  # 忘记增加count，导致无限循环

# 正确做法
count = 0
while count < 5:
    print(count)
    count += 1

# 3. 避免在循环中重复计算
# 错误做法
data = [1, 2, 3, 4, 5]
for i in range(len(data)):  # 每次都计算len(data)
    print(data[i])

# 正确做法
data = [1, 2, 3, 4, 5]
length = len(data)  # 只计算一次
for i in range(length):
    print(data[i])

# 或者直接遍历
for item in data:
    print(item)
```

## 问题78：循环的最佳实践

```python
# 1. 使用描述性的变量名
def calculate_total_price(items):
    total = 0
    for item in items:
        total += item['price'] * item['quantity']
    return total

# 2. 使用函数封装复杂循环逻辑
def find_duplicates(lst):
    seen = set()
    duplicates = set()
    
    for item in lst:
        if item in seen:
            duplicates.add(item)
        else:
            seen.add(item)
    
    return list(duplicates)

# 3. 使用生成器处理大数据
def read_large_file(filename):
    with open(filename, 'r') as file:
        for line in file:
            yield line.strip()

# 4. 使用适当的循环类型
# 当知道循环次数时使用for循环
for i in range(10):
    print(i)

# 当条件不确定时使用while循环
user_input = ""
while user_input.lower() != 'quit':
    user_input = input("输入'quit'退出: ")

# 5. 使用循环的else子句
def search_item(items, target):
    for i, item in enumerate(items):
        if item == target:
            return i
    else:
        return -1

# 6. 合理使用break和continue
def process_numbers(numbers):
    result = []
    for num in numbers:
        if num < 0:
            continue  # 跳过负数
        if num > 100:
            break    # 遇到大于100的数就停止
        result.append(num)
    return result
```

## 总结

循环是编程中的基础概念，要点包括：
- **for循环**：适合已知循环次数或遍历序列
- **while循环**：适合条件不确定的循环
- **break和continue**：控制循环流程
- **嵌套循环**：处理多维数据
- **else子句**：循环正常结束时的处理
- **性能优化**：使用推导式、生成器等
- **最佳实践**：避免常见错误，使用合适的循环类型
