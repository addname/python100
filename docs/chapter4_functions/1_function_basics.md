# 函数的定义与调用

## 问题89：什么是函数？为什么要使用函数？

函数是一段可重复使用的代码块，用于执行特定的任务：

```python
# 定义函数
def greet():
    print("Hello, World!")

# 调用函数
greet()  # Hello, World!
```

### 使用函数的好处：
1. **代码复用**：避免重复编写相同的代码
2. **模块化**：将复杂问题分解为小问题
3. **可维护性**：修改一处，影响全局
4. **可读性**：函数名可以表达功能意图

## 问题90：如何定义和调用函数？

```python
# 1. 无参数函数
def say_hello():
    print("Hello!")

# 2. 有参数函数
def greet(name):
    print(f"Hello, {name}!")

# 3. 有返回值函数
def add(a, b):
    return a + b

# 4. 多参数函数
def calculate_area(length, width):
    area = length * width
    return area

# 调用函数
say_hello()                    # Hello!
greet("张三")                  # Hello, 张三!
result = add(3, 5)            # result = 8
area = calculate_area(4, 5)   # area = 20
```

## 问题91：函数的参数有哪些类型？

```python
# 1. 位置参数
def greet(name, age):
    print(f"姓名: {name}, 年龄: {age}")

greet("张三", 25)  # 按位置传递参数

# 2. 关键字参数
greet(age=25, name="张三")  # 按名称传递参数

# 3. 默认参数
def greet_with_default(name, age=18):
    print(f"姓名: {name}, 年龄: {age}")

greet_with_default("李四")        # 使用默认年龄
greet_with_default("王五", 30)    # 覆盖默认年龄

# 4. 可变参数
def sum_numbers(*args):
    total = 0
    for num in args:
        total += num
    return total

result = sum_numbers(1, 2, 3, 4, 5)  # result = 15

# 5. 关键字可变参数
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="张三", age=25, city="北京")
```

## 问题92：函数的返回值如何处理？

```python
# 1. 单个返回值
def square(x):
    return x * x

result = square(5)  # result = 25

# 2. 多个返回值
def get_name_and_age():
    return "张三", 25

name, age = get_name_and_age()
print(f"姓名: {name}, 年龄: {age}")

# 3. 无返回值（返回None）
def print_message(msg):
    print(msg)
    # 没有return语句，默认返回None

result = print_message("Hello")
print(result)  # None

# 4. 条件返回值
def divide(a, b):
    if b == 0:
        return None  # 除零时返回None
    return a / b

result = divide(10, 2)  # result = 5.0
result = divide(10, 0)  # result = None
```

## 问题93：函数的作用域是什么？

```python
# 全局变量
global_var = "我是全局变量"

def test_scope():
    # 局部变量
    local_var = "我是局部变量"
    print(global_var)  # 可以访问全局变量
    print(local_var)   # 可以访问局部变量

test_scope()
# print(local_var)  # 错误：局部变量在函数外不可访问

# 修改全局变量
def modify_global():
    global global_var
    global_var = "修改后的全局变量"

modify_global()
print(global_var)  # 修改后的全局变量
```

## 问题94：函数的高级特性有哪些？

```python
# 1. 函数作为参数
def apply_operation(x, y, operation):
    return operation(x, y)

def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

result1 = apply_operation(3, 4, add)      # result1 = 7
result2 = apply_operation(3, 4, multiply) # result2 = 12

# 2. 函数作为返回值
def create_multiplier(factor):
    def multiplier(x):
        return x * factor
    return multiplier

double = create_multiplier(2)
triple = create_multiplier(3)

print(double(5))  # 10
print(triple(5))  # 15

# 3. 装饰器
def my_decorator(func):
    def wrapper():
        print("函数执行前")
        func()
        print("函数执行后")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

## 问题95：函数的实际应用场景有哪些？

```python
# 1. 数据处理
def process_data(data):
    # 数据清洗
    cleaned_data = [item for item in data if item is not None]
    
    # 数据转换
    processed_data = [item * 2 for item in cleaned_data]
    
    return processed_data

# 2. 计算工具
def calculate_statistics(numbers):
    if not numbers:
        return None
    
    return {
        'count': len(numbers),
        'sum': sum(numbers),
        'average': sum(numbers) / len(numbers),
        'max': max(numbers),
        'min': min(numbers)
    }

# 3. 验证函数
def validate_email(email):
    import re
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None

# 4. 文件处理
def read_file_lines(filename):
    try:
        with open(filename, 'r', encoding='utf-8') as file:
            return file.readlines()
    except FileNotFoundError:
        print(f"文件 {filename} 不存在")
        return []

# 5. 用户交互
def get_user_choice(options):
    while True:
        print("请选择:")
        for i, option in enumerate(options, 1):
            print(f"{i}. {option}")
        
        try:
            choice = int(input("请输入选择: "))
            if 1 <= choice <= len(options):
                return options[choice - 1]
            else:
                print("选择超出范围")
        except ValueError:
            print("请输入有效数字")
```

## 问题96：如何编写高质量的函数？

```python
# 1. 使用描述性的函数名
def calculate_circle_area(radius):
    return 3.14159 * radius ** 2

# 2. 添加文档字符串
def calculate_rectangle_area(length, width):
    """
    计算矩形的面积
    
    参数:
        length (float): 矩形的长度
        width (float): 矩形的宽度
    
    返回:
        float: 矩形的面积
    """
    return length * width

# 3. 参数验证
def safe_divide(a, b):
    if not isinstance(a, (int, float)) or not isinstance(b, (int, float)):
        raise TypeError("参数必须是数字")
    if b == 0:
        raise ValueError("除数不能为零")
    return a / b

# 4. 使用类型提示
def add_numbers(a: int, b: int) -> int:
    return a + b

# 5. 单一职责原则
def validate_user_input(username, password):
    errors = []
    
    if not username:
        errors.append("用户名不能为空")
    if len(password) < 6:
        errors.append("密码长度至少6位")
    
    return len(errors) == 0, errors
```

## 问题97：函数的调试技巧有哪些？

```python
# 1. 使用print语句调试
def debug_function(x, y):
    print(f"输入参数: x={x}, y={y}")
    result = x + y
    print(f"计算结果: {result}")
    return result

# 2. 使用断言
def divide(a, b):
    assert b != 0, "除数不能为零"
    return a / b

# 3. 使用日志
import logging

def process_data(data):
    logging.info(f"开始处理数据，长度: {len(data)}")
    
    for i, item in enumerate(data):
        logging.debug(f"处理第{i}个元素: {item}")
        # 处理逻辑
    
    logging.info("数据处理完成")

# 4. 使用异常处理
def safe_operation(data):
    try:
        result = process_data(data)
        return result
    except Exception as e:
        print(f"处理数据时出错: {e}")
        return None
```

## 问题98：函数的最佳实践

```python
# 1. 保持函数简短
def calculate_tax(income):
    if income <= 50000:
        return income * 0.1
    elif income <= 100000:
        return income * 0.2
    else:
        return income * 0.3

# 2. 避免副作用
def pure_function(x, y):
    return x + y  # 没有副作用

# 3. 使用默认参数
def create_user(name, age=18, city="未知"):
    return {"name": name, "age": age, "city": city}

# 4. 使用*args和**kwargs
def flexible_function(*args, **kwargs):
    print(f"位置参数: {args}")
    print(f"关键字参数: {kwargs}")

# 5. 函数组合
def compose(f, g):
    return lambda x: f(g(x))

def add_one(x):
    return x + 1

def multiply_two(x):
    return x * 2

add_one_then_multiply = compose(multiply_two, add_one)
result = add_one_then_multiply(5)  # (5 + 1) * 2 = 12
```

## 总结

函数是Python编程的基础，要点包括：
- **定义和调用**：使用def关键字定义函数
- **参数类型**：位置参数、关键字参数、默认参数、可变参数
- **返回值**：使用return语句返回值
- **作用域**：全局变量和局部变量的访问规则
- **高级特性**：函数作为参数、返回值、装饰器
- **最佳实践**：单一职责、参数验证、文档字符串
- **调试技巧**：print、断言、日志、异常处理
