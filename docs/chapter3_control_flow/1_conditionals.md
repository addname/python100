# 条件判断

## 问题1：Python中的条件判断语句有哪些？

Python中的条件判断主要通过 `if`、`elif`、`else` 语句实现：

```python
# 基本if语句
age = 18
if age >= 18:
    print("您已成年")

# if-else语句
age = 16
if age >= 18:
    print("您已成年")
else:
    print("您未成年")

# if-elif-else语句
score = 85
if score >= 90:
    print("优秀")
elif score >= 80:
    print("良好")
elif score >= 70:
    print("中等")
elif score >= 60:
    print("及格")
else:
    print("不及格")
```

## 问题2：条件表达式中的比较操作符如何使用？

```python
# 数值比较
a = 10
b = 5

if a > b:
    print("a大于b")
if a >= b:
    print("a大于等于b")
if a < b:
    print("a小于b")
if a <= b:
    print("a小于等于b")
if a == b:
    print("a等于b")
if a != b:
    print("a不等于b")

# 字符串比较
name1 = "Alice"
name2 = "Bob"

if name1 < name2:  # 按字典序比较
    print("Alice在Bob之前")

# 链式比较
age = 25
if 18 <= age <= 65:
    print("工作年龄")
```

## 问题3：逻辑操作符在条件判断中如何使用？

```python
# and 操作符
age = 25
has_license = True

if age >= 18 and has_license:
    print("可以开车")

# or 操作符
is_weekend = False
is_holiday = True

if is_weekend or is_holiday:
    print("可以休息")

# not 操作符
is_raining = False
if not is_raining:
    print("天气不错，可以出门")

# 复杂逻辑表达式
score = 85
attendance = 0.9
homework_complete = True

if score >= 80 and attendance >= 0.8 and homework_complete:
    print("成绩优秀，出勤良好，作业完成")
elif score >= 60 or attendance >= 0.6:
    print("基本要求达到")
else:
    print("需要努力")
```

## 问题4：如何检查变量是否为真值或假值？

```python
# Python中的真值和假值
# 假值：False, None, 0, 0.0, "", [], {}, set()

# 检查真值
name = "张三"
if name:  # 非空字符串为真
    print(f"欢迎, {name}")

# 检查假值
empty_list = []
if not empty_list:
    print("列表为空")

# 检查None
value = None
if value is None:
    print("值为空")

# 检查零值
count = 0
if count:
    print("有数据")
else:
    print("无数据")
```

## 问题5：嵌套条件判断如何处理？

```python
# 嵌套if语句
age = 20
has_license = True
has_car = False

if age >= 18:
    if has_license:
        if has_car:
            print("可以开车出行")
        else:
            print("有驾照但没车")
    else:
        print("需要先考驾照")
else:
    print("年龄不够")

# 使用elif简化嵌套
if age < 18:
    print("年龄不够")
elif not has_license:
    print("需要先考驾照")
elif not has_car:
    print("有驾照但没车")
else:
    print("可以开车出行")
```

## 问题6：条件判断中的成员检查如何使用？

```python
# 检查字符串中的子串
text = "Hello, Python!"
if "Python" in text:
    print("包含Python")

# 检查列表中的元素
fruits = ["苹果", "香蕉", "橙子"]
if "苹果" in fruits:
    print("有苹果")

# 检查字典中的键
person = {"name": "张三", "age": 25}
if "name" in person:
    print("有姓名信息")

# 检查范围
score = 85
if score in range(80, 91):  # 80-90分
    print("成绩良好")
```

## 问题7：如何处理异常情况的条件判断？

```python
# 使用try-except处理可能的异常
def safe_divide(a, b):
    try:
        result = a / b
        if result > 0:
            print("结果为正数")
        elif result < 0:
            print("结果为负数")
        else:
            print("结果为零")
        return result
    except ZeroDivisionError:
        print("除数不能为零")
        return None
    except TypeError:
        print("参数类型错误")
        return None

# 测试
print(safe_divide(10, 2))   # 结果为正数, 5.0
print(safe_divide(10, 0))   # 除数不能为零, None
print(safe_divide(10, "a")) # 参数类型错误, None
```

## 问题8：条件判断的实际应用场景有哪些？

```python
# 1. 用户输入验证
def validate_input():
    user_input = input("请输入年龄: ")
    try:
        age = int(user_input)
        if age < 0:
            print("年龄不能为负数")
        elif age > 150:
            print("年龄不能超过150")
        else:
            print(f"年龄: {age}")
    except ValueError:
        print("请输入有效的数字")

# 2. 权限检查
def check_permission(user_role, action):
    admin_actions = ["delete", "modify", "create"]
    user_actions = ["read", "comment"]
    
    if user_role == "admin":
        return True
    elif user_role == "user" and action in user_actions:
        return True
    else:
        return False

# 3. 数据过滤
def filter_students(students, min_score=60):
    passed = []
    failed = []
    
    for student in students:
        name, score = student
        if score >= min_score:
            passed.append(student)
        else:
            failed.append(student)
    
    return passed, failed

# 使用示例
students = [("张三", 85), ("李四", 45), ("王五", 92)]
passed, failed = filter_students(students)
print("及格:", passed)
print("不及格:", failed)
```

## 问题9：如何优化条件判断的代码？

```python
# 1. 使用字典映射替代多个if-elif
def get_grade(score):
    grade_map = {
        (90, 101): "优秀",
        (80, 90): "良好", 
        (70, 80): "中等",
        (60, 70): "及格",
        (0, 60): "不及格"
    }
    
    for (min_score, max_score), grade in grade_map.items():
        if min_score <= score < max_score:
            return grade
    return "无效分数"

# 2. 使用any()和all()函数
def check_requirements(age, has_license, has_car):
    requirements = [age >= 18, has_license, has_car]
    
    if all(requirements):
        return "可以开车"
    elif any(requirements):
        return "部分满足条件"
    else:
        return "不满足条件"

# 3. 使用三元操作符简化简单判断
def get_status(score):
    return "及格" if score >= 60 else "不及格"

# 4. 提前返回减少嵌套
def process_user(user):
    if not user:
        return "用户不存在"
    
    if not user.get("active"):
        return "用户未激活"
    
    if not user.get("verified"):
        return "用户未验证"
    
    return "用户正常"
```

## 问题10：条件判断的常见错误和注意事项

```python
# 1. 避免使用==比较浮点数
# 错误做法
a = 0.1 + 0.2
if a == 0.3:  # 可能为False
    print("相等")

# 正确做法
if abs(a - 0.3) < 1e-9:
    print("相等")

# 2. 注意is和==的区别
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True (值相等)
print(a is b)  # False (不是同一个对象)
print(a is c)  # True (是同一个对象)

# 3. 避免在条件中使用赋值
# 错误做法
# if x = 5:  # 语法错误

# 正确做法
if x == 5:
    print("x等于5")

# 4. 注意空值的判断
value = None
if value is None:  # 推荐
    print("值为空")

# 或者
if not value:  # 但要注意0, "", []等也会为False
    print("值为空或假值")
```

## 总结

条件判断是编程中的基础概念，要点包括：
- **基本语法**：if, elif, else
- **比较操作符**：==, !=, <, >, <=, >=
- **逻辑操作符**：and, or, not
- **真值判断**：理解Python中的真值和假值
- **最佳实践**：避免嵌套过深，使用合适的比较方式
- **常见错误**：浮点数比较、is vs ==、赋值 vs 比较
