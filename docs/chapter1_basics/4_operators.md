# 常用操作符

## 问题1：Python中有哪些算术操作符？

Python提供了丰富的算术操作符：

```python
# 基本算术运算
a = 10
b = 3

print(a + b)   # 13 (加法)
print(a - b)   # 7  (减法)
print(a * b)   # 30 (乘法)
print(a / b)   # 3.3333333333333335 (除法，返回浮点数)
print(a // b)  # 3  (整数除法，向下取整)
print(a % b)   # 1  (取余)
print(a ** b)  # 1000 (幂运算)

# 复合赋值操作符
x = 5
x += 3  # 等价于 x = x + 3
print(x)  # 8

x -= 2  # 等价于 x = x - 2
print(x)  # 6

x *= 2  # 等价于 x = x * 2
print(x)  # 12

x /= 3  # 等价于 x = x / 3
print(x)  # 4.0
```

## 问题2：比较操作符如何使用？

比较操作符用于比较两个值，返回布尔值：

```python
a = 10
b = 5

print(a == b)  # False (等于)
print(a != b)  # True  (不等于)
print(a > b)   # True  (大于)
print(a < b)   # False (小于)
print(a >= b)  # True  (大于等于)
print(a <= b)  # False (小于等于)

# 字符串比较
name1 = "Alice"
name2 = "Bob"
print(name1 < name2)  # True (按字典序比较)

# 链式比较
age = 25
print(18 <= age <= 65)  # True
```

## 问题3：逻辑操作符有什么特点？

Python中的逻辑操作符包括 `and`、`or`、`not`：

```python
# 逻辑与 (and)
age = 25
has_license = True

if age >= 18 and has_license:
    print("可以开车")

# 逻辑或 (or)
is_weekend = False
is_holiday = True

if is_weekend or is_holiday:
    print("可以休息")

# 逻辑非 (not)
is_raining = False
if not is_raining:
    print("天气不错，可以出门")

# 复杂逻辑表达式
score = 85
attendance = 0.9

if score >= 80 and attendance >= 0.8:
    print("成绩优秀且出勤良好")
elif score >= 60 or attendance >= 0.6:
    print("成绩或出勤达到基本要求")
else:
    print("需要努力")
```

## 问题4：成员操作符如何使用？

`in` 和 `not in` 用于检查成员关系：

```python
# 字符串中的成员检查
text = "Hello, Python!"
print("Python" in text)    # True
print("Java" in text)      # False
print("Python" not in text) # False

# 列表中的成员检查
fruits = ["苹果", "香蕉", "橙子"]
print("苹果" in fruits)     # True
print("葡萄" in fruits)     # False

# 字典中的成员检查
person = {"name": "张三", "age": 25}
print("name" in person)    # True
print("salary" in person)  # False
```

## 问题5：身份操作符有什么用途？

`is` 和 `is not` 用于比较对象的身份（内存地址）：

```python
# 身份比较
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True (值相等)
print(a is b)  # False (不是同一个对象)
print(a is c)  # True (是同一个对象)

# 小整数缓存
x = 5
y = 5
print(x is y)  # True (小整数被缓存)

# None 的比较
value = None
print(value is None)     # True
print(value is not None) # False
```

## 问题6：位操作符如何使用？

位操作符用于对二进制位进行操作：

```python
a = 5  # 二进制: 101
b = 3  # 二进制: 011

print(a & b)   # 1  (按位与: 001)
print(a | b)   # 7  (按位或: 111)
print(a ^ b)   # 6  (按位异或: 110)
print(~a)      # -6 (按位取反)
print(a << 1)  # 10 (左移: 1010)
print(a >> 1)  # 2  (右移: 010)

# 位操作的应用
# 检查奇偶性
number = 7
if number & 1:
    print("奇数")
else:
    print("偶数")

# 快速计算2的幂
power = 1 << 3  # 等价于 2**3
print(power)  # 8
```

## 问题7：操作符优先级如何影响运算结果？

Python中的操作符有优先级，优先级高的先计算：

```python
# 算术操作符优先级
result = 2 + 3 * 4  # 先算乘法，再算加法
print(result)  # 14

result = (2 + 3) * 4  # 括号改变优先级
print(result)  # 20

# 比较和逻辑操作符
age = 25
score = 85
attendance = 0.9

# 注意优先级
if age >= 18 and score >= 80 or attendance >= 0.9:
    print("条件满足")

# 使用括号明确优先级
if (age >= 18 and score >= 80) or attendance >= 0.9:
    print("条件满足")
```

## 问题8：如何重载操作符？

在类中可以重载操作符：

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)
    
    def __eq__(self, other):
        return self.x == other.x and self.y == other.y
    
    def __str__(self):
        return f"Point({self.x}, {self.y})"

# 使用重载的操作符
p1 = Point(1, 2)
p2 = Point(3, 4)
p3 = p1 + p2  # 调用 __add__ 方法
print(p3)     # Point(4, 6)

print(p1 == p2)  # False
print(p1 == Point(1, 2))  # True
```

## 问题9：三元操作符如何使用？

Python中的三元操作符语法：`值1 if 条件 else 值2`

```python
# 基本用法
age = 20
status = "成年" if age >= 18 else "未成年"
print(status)  # 成年

# 嵌套使用
score = 85
grade = "优秀" if score >= 90 else "良好" if score >= 80 else "及格" if score >= 60 else "不及格"
print(grade)  # 良好

# 在函数中使用
def get_max(a, b):
    return a if a > b else b

print(get_max(10, 20))  # 20
```

## 问题10：操作符的实际应用场景有哪些？

```python
# 1. 数据验证
def validate_age(age):
    return isinstance(age, int) and 0 <= age <= 150

# 2. 权限检查
def check_permission(user_role, required_role):
    roles = ["guest", "user", "admin"]
    return roles.index(user_role) >= roles.index(required_role)

# 3. 范围检查
def is_in_range(value, min_val, max_val):
    return min_val <= value <= max_val

# 4. 字符串处理
def format_name(first_name, last_name):
    return f"{first_name} {last_name}".strip()

# 5. 数学计算
def calculate_discount(price, discount_rate):
    return price * (1 - discount_rate) if 0 <= discount_rate <= 1 else price

# 使用示例
print(validate_age(25))  # True
print(check_permission("admin", "user"))  # True
print(is_in_range(15, 10, 20))  # True
print(format_name("  John  ", "  Doe  "))  # John Doe
print(calculate_discount(100, 0.1))  # 90.0
```

## 总结

Python的操作符包括：
- **算术操作符**: +, -, *, /, //, %, **
- **比较操作符**: ==, !=, <, >, <=, >=
- **逻辑操作符**: and, or, not
- **成员操作符**: in, not in
- **身份操作符**: is, is not
- **位操作符**: &, |, ^, ~, <<, >>

掌握这些操作符的使用方法和优先级，是编写Python程序的基础。
