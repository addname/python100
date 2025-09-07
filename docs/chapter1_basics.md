# 第一章：Python基础

本章涵盖了Python编程的基础知识，包括环境搭建、基本语法、数据类型和操作符。

---

## 1. 如何安装Python？

**答：**
Python的安装方法取决于你的操作系统：

### Windows系统
1. 访问 [python.org](https://www.python.org/downloads/)
2. 下载最新版本的Python安装包
3. 运行安装程序，**务必勾选"Add Python to PATH"**
4. 选择"Install Now"完成安装

### macOS系统
```bash
# 使用Homebrew安装
brew install python3

# 或者从官网下载安装包
```

### Linux系统
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip

# CentOS/RHEL
sudo yum install python3 python3-pip
```

安装完成后，在终端运行 `python3 --version` 验证安装是否成功。

---

## 2. 如何配置pip？

**答：**
pip是Python的包管理器，通常随Python一起安装。

### 检查pip版本
```bash
pip3 --version
# 或者
python3 -m pip --version
```

### 升级pip
```bash
python3 -m pip install --upgrade pip
```

### 配置国内镜像源（加速下载）
```bash
# 临时使用清华源
pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple/ package_name

# 永久配置
pip3 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/
```

---

## 3. 如何管理虚拟环境？

**答：**
虚拟环境可以隔离不同项目的依赖包，避免版本冲突。

### 创建虚拟环境
```bash
# 使用venv（Python 3.3+内置）
python3 -m venv myenv

# 使用virtualenv
pip3 install virtualenv
virtualenv myenv
```

### 激活虚拟环境
```bash
# Windows
myenv\Scripts\activate

# macOS/Linux
source myenv/bin/activate
```

### 退出虚拟环境
```bash
deactivate
```

---

## 4. Python的基本语法规则？

**答：**
Python的语法特点：

### 缩进规则
```python
# 使用4个空格缩进（推荐）
if True:
    print("这是正确的缩进")
    if True:
        print("嵌套缩进")
```

### 注释
```python
# 单行注释

"""
多行注释
可以写多行内容
"""

'''
这也是多行注释
'''
```

### 语句分隔
```python
# 一行一条语句（推荐）
name = "Python"
age = 30

# 一行多条语句（不推荐）
name = "Python"; age = 30
```

---

## 5. 如何写注释？

**答：**
Python支持多种注释方式：

### 单行注释
```python
# 这是单行注释
name = "Python"  # 行尾注释
```

### 多行注释
```python
"""
这是多行注释
可以写多行内容
用于文档说明
"""

'''
这也是多行注释
功能相同
'''
```

### 文档字符串（Docstring）
```python
def greet(name):
    """
    问候函数
    
    参数:
        name (str): 要问候的名字
    
    返回:
        str: 问候语
    """
    return f"Hello, {name}!"
```

---

## 6. 变量命名规则？

**答：**
Python变量命名遵循以下规则：

### 基本规则
```python
# 正确命名
name = "Python"
age = 30
user_name = "admin"
total_count = 100

# 错误命名
2name = "Python"  # 不能以数字开头
user-name = "admin"  # 不能包含连字符
class = "Python"  # 不能使用关键字
```

### 命名约定
```python
# 变量名：小写字母+下划线
user_name = "admin"
total_count = 100

# 常量：全大写+下划线
MAX_SIZE = 1024
PI = 3.14159

# 类名：驼峰命名
class UserManager:
    pass

# 函数名：小写字母+下划线
def get_user_info():
    pass
```

### 关键字
```python
# Python关键字（不能用作变量名）
import keyword
print(keyword.kwlist)
```

---

## 7. Python有哪些基本数据类型？

**答：**
Python的基本数据类型包括：

### 数字类型
```python
# 整数
age = 25
count = -10

# 浮点数
price = 19.99
rate = 0.05

# 复数
complex_num = 3 + 4j
```

### 字符串
```python
# 单引号
name = 'Python'

# 双引号
message = "Hello World"

# 三引号（多行字符串）
text = """
这是多行字符串
可以包含换行
"""
```

### 布尔类型
```python
is_active = True
is_finished = False
```

### 空值
```python
result = None
```

---

## 8. 字符串如何操作？

**答：**
字符串是Python中常用的数据类型，支持多种操作：

### 字符串创建
```python
# 单引号
name = 'Python'

# 双引号
message = "Hello World"

# 三引号（多行）
text = """
多行字符串
可以包含换行
"""
```

### 字符串连接
```python
# 使用+号
first_name = "张"
last_name = "三"
full_name = first_name + last_name

# 使用join方法
words = ["Hello", "World", "Python"]
sentence = " ".join(words)
```

### 字符串格式化
```python
# f-string（推荐）
name = "Python"
version = 3.9
info = f"语言：{name}，版本：{version}"

# format方法
info = "语言：{}，版本：{}".format(name, version)

# %格式化
info = "语言：%s，版本：%.1f" % (name, version)
```

### 字符串方法
```python
text = "  Hello World  "

# 去除空格
clean_text = text.strip()

# 大小写转换
upper_text = text.upper()
lower_text = text.lower()

# 查找和替换
index = text.find("World")
new_text = text.replace("World", "Python")

# 分割字符串
words = text.split()
```

---

## 9. 数字类型有哪些？

**答：**
Python支持多种数字类型：

### 整数（int）
```python
# 十进制
age = 25

# 二进制
binary = 0b1010  # 10

# 八进制
octal = 0o12  # 10

# 十六进制
hexadecimal = 0xA  # 10

# 大整数（Python自动处理）
big_number = 2**1000
```

### 浮点数（float）
```python
# 普通浮点数
price = 19.99
rate = 0.05

# 科学计数法
scientific = 1.23e4  # 12300.0

# 特殊值
infinity = float('inf')
not_a_number = float('nan')
```

### 复数（complex）
```python
# 复数
z1 = 3 + 4j
z2 = complex(3, 4)

# 复数运算
real_part = z1.real  # 3.0
imag_part = z1.imag  # 4.0
```

### 数字运算
```python
a, b = 10, 3

# 基本运算
sum_result = a + b
diff_result = a - b
prod_result = a * b
div_result = a / b
floor_div = a // b  # 整除
mod_result = a % b  # 取余
power_result = a ** b  # 幂运算
```

---

## 10. 算术操作符有哪些？

**答：**
Python支持多种算术操作符：

### 基本算术操作符
```python
a, b = 10, 3

# 加法
result = a + b  # 13

# 减法
result = a - b  # 7

# 乘法
result = a * b  # 30

# 除法（返回浮点数）
result = a / b  # 3.333...

# 整除（返回整数）
result = a // b  # 3

# 取余
result = a % b  # 1

# 幂运算
result = a ** b  # 1000
```

### 复合赋值操作符
```python
x = 10

# 等价于 x = x + 5
x += 5  # 15

# 等价于 x = x - 3
x -= 3  # 12

# 等价于 x = x * 2
x *= 2  # 24

# 等价于 x = x / 4
x /= 4  # 6.0
```

### 操作符优先级
```python
# 优先级从高到低：
# 1. ** (幂运算)
# 2. *, /, //, % (乘除)
# 3. +, - (加减)

result = 2 + 3 * 4 ** 2  # 50
# 计算顺序：4**2=16, 3*16=48, 2+48=50

# 使用括号改变优先级
result = (2 + 3) * 4 ** 2  # 80
```

---

## 11. 比较操作符如何使用？

**答：**
比较操作符用于比较两个值，返回布尔值（True或False）：

### 基本比较操作符
```python
a, b = 10, 5

# 等于
result = a == b  # False

# 不等于
result = a != b  # True

# 大于
result = a > b   # True

# 小于
result = a < b   # False

# 大于等于
result = a >= b  # True

# 小于等于
result = a <= b  # False
```

### 字符串比较
```python
# 按字典序比较
result = "apple" < "banana"  # True
result = "cat" > "dog"       # False
result = "hello" == "hello"  # True
```

### 链式比较
```python
# 可以链式比较
age = 25
result = 18 <= age <= 65  # True

# 等价于
result = age >= 18 and age <= 65
```

### 身份比较
```python
# is 和 is not（比较对象身份）
a = [1, 2, 3]
b = [1, 2, 3]
c = a

result = a == b  # True（值相等）
result = a is b  # False（不是同一个对象）
result = a is c  # True（是同一个对象）
```

---

## 12. 逻辑操作符的作用？

**答：**
逻辑操作符用于组合多个条件，返回布尔值：

### 基本逻辑操作符
```python
# and（与）：两个条件都为True时返回True
result = True and True   # True
result = True and False  # False
result = False and False # False

# or（或）：至少一个条件为True时返回True
result = True or True    # True
result = True or False   # True
result = False or False  # False

# not（非）：取反
result = not True   # False
result = not False  # True
```

### 实际应用示例
```python
age = 25
has_license = True
has_car = False

# 可以开车：年龄>=18 且 有驾照
can_drive = age >= 18 and has_license

# 可以出行：有驾照 或 有车
can_travel = has_license or has_car

# 不能开车：年龄<18 或 没有驾照
cannot_drive = age < 18 or not has_license
```

### 短路求值
```python
# and：如果第一个条件为False，不会计算第二个条件
def expensive_check():
    print("执行了昂贵的检查")
    return True

result = False and expensive_check()  # 不会打印，因为短路

# or：如果第一个条件为True，不会计算第二个条件
result = True or expensive_check()    # 不会打印，因为短路
```

### 操作符优先级
```python
# 优先级从高到低：
# 1. not
# 2. and
# 3. or

result = not True and False or True
# 计算顺序：not True=False, False and False=False, False or True=True
```
