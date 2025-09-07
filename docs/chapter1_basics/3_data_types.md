# 基本数据类型

## 问题1：Python中有哪些基本数据类型？

Python中有以下几种基本数据类型：

### 1. 数字类型 (Numbers)

#### 整数 (int)
```python
# 整数
age = 25
temperature = -10
big_number = 1000000

print(type(age))  # <class 'int'>
```

#### 浮点数 (float)
```python
# 浮点数
price = 19.99
pi = 3.14159
scientific = 1.23e-4  # 科学计数法

print(type(price))  # <class 'float'>
```

#### 复数 (complex)
```python
# 复数
complex_num = 3 + 4j
print(complex_num.real)  # 3.0
print(complex_num.imag)  # 4.0
```

### 2. 字符串 (str)
```python
# 字符串
name = "Python"
message = 'Hello, World!'
multiline = """这是一个
多行字符串"""

print(type(name))  # <class 'str'>
```

### 3. 布尔值 (bool)
```python
# 布尔值
is_student = True
is_working = False

print(type(is_student))  # <class 'bool'>
```

### 4. 空值 (NoneType)
```python
# 空值
empty_value = None
print(type(empty_value))  # <class 'NoneType'>
```

## 问题2：如何检查变量的数据类型？

使用 `type()` 函数或 `isinstance()` 函数：

```python
# 使用 type() 函数
number = 42
print(type(number))  # <class 'int'>

# 使用 isinstance() 函数
if isinstance(number, int):
    print("这是一个整数")

# 检查多个类型
if isinstance(number, (int, float)):
    print("这是一个数字")
```

## 问题3：如何进行类型转换？

Python提供了内置的类型转换函数：

```python
# 字符串转整数
str_num = "123"
int_num = int(str_num)
print(int_num, type(int_num))  # 123 <class 'int'>

# 整数转字符串
num = 456
str_num = str(num)
print(str_num, type(str_num))  # 456 <class 'str'>

# 字符串转浮点数
str_float = "3.14"
float_num = float(str_float)
print(float_num, type(float_num))  # 3.14 <class 'float'>

# 数字转布尔值
print(bool(1))    # True
print(bool(0))    # False
print(bool(""))   # False
print(bool("hi")) # True
```

## 问题4：Python中的数字运算有什么特点？

```python
# 整数除法
print(10 / 3)   # 3.3333333333333335 (浮点数结果)
print(10 // 3)  # 3 (整数除法，向下取整)
print(10 % 3)   # 1 (取余)
print(10 ** 3)  # 1000 (幂运算)

# 混合运算
result = 5 + 3.14  # 整数和浮点数运算，结果为浮点数
print(result)  # 8.14
```

## 问题5：字符串有哪些基本操作？

```python
# 字符串连接
first_name = "张"
last_name = "三"
full_name = first_name + last_name
print(full_name)  # 张三

# 字符串重复
stars = "*" * 5
print(stars)  # *****

# 字符串长度
text = "Hello, Python!"
print(len(text))  # 14

# 字符串索引和切片
print(text[0])     # H
print(text[-1])    # !
print(text[0:5])   # Hello
print(text[7:])    # Python!
```

## 问题6：布尔值在条件判断中如何使用？

```python
# 布尔值的基本使用
is_raining = True
is_sunny = False

if is_raining:
    print("记得带伞")
else:
    print("天气不错")

# 布尔运算
print(True and False)  # False
print(True or False)   # True
print(not True)        # False

# 比较运算返回布尔值
age = 18
print(age >= 18)  # True
print(age == 20)  # False
```

## 问题7：None值有什么用途？

```python
# None表示空值或未定义
def find_user(user_id):
    # 模拟查找用户
    if user_id == 1:
        return "张三"
    else:
        return None

result = find_user(2)
if result is None:
    print("用户不存在")
else:
    print(f"找到用户: {result}")

# None与其他值的比较
print(None == None)  # True
print(None is None)  # True
print(None == 0)     # False
print(None == "")    # False
```

## 问题8：如何获取用户输入并处理数据类型？

```python
# 获取用户输入（总是字符串类型）
user_input = input("请输入您的年龄: ")
print(f"输入内容: {user_input}, 类型: {type(user_input)}")

# 转换为整数
try:
    age = int(user_input)
    print(f"您的年龄是: {age}")
    if age >= 18:
        print("您已成年")
    else:
        print("您未成年")
except ValueError:
    print("请输入有效的数字")

# 获取多个输入
name = input("请输入姓名: ")
age = int(input("请输入年龄: "))
print(f"姓名: {name}, 年龄: {age}")
```

## 总结

Python的基本数据类型包括：
- **数字类型**: int, float, complex
- **字符串**: str
- **布尔值**: bool
- **空值**: None

掌握这些基本数据类型是学习Python的基础，它们为后续学习更复杂的数据结构打下了坚实的基础。
