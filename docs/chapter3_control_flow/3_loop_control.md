# break、continue与pass

## 问题1：break语句的作用是什么？

`break`语句用于跳出当前循环，继续执行循环后的代码：

```python
# 基本用法
for i in range(10):
    if i == 5:
        break
    print(i)  # 0, 1, 2, 3, 4

# 在while循环中使用
count = 0
while count < 10:
    if count == 3:
        break
    print(count)
    count += 1  # 0, 1, 2
```

## 问题2：continue语句的作用是什么？

`continue`语句用于跳过当前迭代，继续下一次循环：

```python
# 跳过偶数
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)  # 1, 3, 5, 7, 9

# 跳过特定值
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for num in numbers:
    if num == 5:
        continue
    print(num)  # 1, 2, 3, 4, 6, 7, 8, 9, 10
```

## 问题3：pass语句的作用是什么？

`pass`语句是空操作，什么都不做，用作占位符：

```python
# 在函数中使用
def future_function():
    pass  # 暂时不实现

# 在类中使用
class FutureClass:
    pass

# 在条件语句中使用
if condition:
    pass  # 暂时不处理
else:
    print("其他情况")
```

## 问题4：循环控制语句的实际应用场景有哪些？

```python
# 1. 查找第一个满足条件的元素
def find_first_even(numbers):
    for num in numbers:
        if num % 2 == 0:
            return num
    return None

# 2. 处理用户输入直到有效
def get_valid_age():
    while True:
        try:
            age = int(input("请输入年龄: "))
            if 0 <= age <= 150:
                return age
            else:
                print("年龄必须在0-150之间")
        except ValueError:
            print("请输入有效数字")

# 3. 跳过无效数据
def process_data(data):
    valid_data = []
    for item in data:
        if item is None or item == "":
            continue  # 跳过无效数据
        valid_data.append(item)
    return valid_data

# 4. 遇到错误时停止处理
def process_files(filenames):
    results = []
    for filename in filenames:
        try:
            with open(filename, 'r') as file:
                content = file.read()
                results.append(content)
        except FileNotFoundError:
            print(f"文件 {filename} 不存在，停止处理")
            break  # 遇到错误就停止
    return results
```

## 问题5：嵌套循环中的break和continue如何使用？

```python
# break只跳出内层循环
for i in range(3):
    for j in range(3):
        if j == 1:
            break  # 只跳出内层循环
        print(f"({i}, {j})")
    print(f"外层循环: {i}")

# 使用标志变量跳出外层循环
found = False
for i in range(3):
    for j in range(3):
        if i == 1 and j == 1:
            found = True
            break
        print(f"({i}, {j})")
    if found:
        break

# 使用函数和return跳出多层循环
def find_target(matrix, target):
    for i, row in enumerate(matrix):
        for j, value in enumerate(row):
            if value == target:
                return (i, j)
    return None
```

## 问题6：循环的else子句与break的关系是什么？

```python
# 如果循环正常结束（没有break），else会执行
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

# 实际应用：查找元素
def search_item(items, target):
    for i, item in enumerate(items):
        if item == target:
            print(f"找到元素 {target}，位置: {i}")
            break
    else:
        print(f"未找到元素 {target}")
```

## 问题7：如何避免循环控制语句的常见错误？

```python
# 1. 避免在循环中忘记更新变量
# 错误做法
count = 0
while count < 5:
    if count == 2:
        continue  # 忘记增加count，导致无限循环
    print(count)
    count += 1

# 正确做法
count = 0
while count < 5:
    if count == 2:
        count += 1  # 先增加count
        continue
    print(count)
    count += 1

# 2. 避免在循环中重复使用break
# 错误做法
for i in range(10):
    if i == 5:
        break
    if i == 3:
        break  # 这行永远不会执行

# 正确做法
for i in range(10):
    if i == 3 or i == 5:
        break
    print(i)
```

## 问题8：循环控制语句的性能考虑

```python
# 1. 使用break提前退出循环
def find_item(items, target):
    for item in items:
        if item == target:
            return item  # 找到就立即返回
    return None

# 2. 使用continue减少不必要的处理
def process_numbers(numbers):
    result = []
    for num in numbers:
        if num < 0:  # 跳过负数
            continue
        if num > 100:  # 遇到大于100的数就停止
            break
        result.append(num * 2)
    return result

# 3. 避免在循环中使用pass
# 不推荐
for i in range(10):
    if i % 2 == 0:
        pass  # 什么都不做
    else:
        print(i)

# 推荐
for i in range(10):
    if i % 2 != 0:
        print(i)
```

## 问题9：循环控制语句的最佳实践

```python
# 1. 使用描述性的条件
def process_user_input():
    while True:
        user_input = input("输入'quit'退出: ")
        if user_input.lower() == 'quit':
            break
        print(f"你输入了: {user_input}")

# 2. 使用函数封装复杂逻辑
def validate_and_process(data):
    for item in data:
        if not is_valid(item):
            continue
        if is_critical_error(item):
            break
        process_item(item)

# 3. 使用适当的循环控制
def find_common_elements(list1, list2):
    common = []
    for item in list1:
        if item in list2:
            common.append(item)
            if len(common) >= 5:  # 找到5个就停止
                break
    return common

# 4. 使用异常处理替代复杂的循环控制
def safe_divide(numbers, divisor):
    results = []
    for num in numbers:
        try:
            result = num / divisor
            results.append(result)
        except ZeroDivisionError:
            print("遇到除零错误，停止处理")
            break
    return results
```

## 问题10：循环控制语句的调试技巧

```python
# 1. 添加调试信息
def debug_loop():
    for i in range(5):
        print(f"循环开始: i = {i}")
        if i == 2:
            print("遇到break条件")
            break
        print(f"循环结束: i = {i}")

# 2. 使用日志记录
import logging

def process_with_logging(data):
    for i, item in enumerate(data):
        logging.info(f"处理第{i}个元素: {item}")
        if item is None:
            logging.warning("遇到空值，跳过")
            continue
        if item < 0:
            logging.error("遇到负数，停止处理")
            break
        logging.info(f"处理完成: {item}")

# 3. 使用断言检查条件
def process_with_assertions(data):
    for item in data:
        assert item is not None, "数据不能为空"
        if item < 0:
            print("遇到负数，停止处理")
            break
        print(f"处理: {item}")
```

## 总结

循环控制语句是编程中的重要工具：
- **break**：跳出当前循环
- **continue**：跳过当前迭代
- **pass**：空操作占位符
- **else子句**：循环正常结束时的处理

使用要点：
- 合理使用break和continue提高效率
- 注意嵌套循环中的控制范围
- 避免无限循环
- 使用函数封装复杂逻辑
- 添加适当的调试信息
