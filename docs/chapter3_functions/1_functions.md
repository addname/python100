# 第三章：函数与模块

!!! info "函数编程基础"
    函数是Python编程的核心概念之一。本章将深入学习函数的定义、调用、参数传递、作用域等概念，以及模块和包的使用。

## 问题36：如何定义和调用函数？

### 🤔 问题描述
在Python中如何定义函数？函数有哪些组成部分？如何正确调用函数？函数的作用域是什么？

### 💡 详细解答

#### 函数的基本结构

```python
def function_name(parameters):
    """
    函数文档字符串
    描述函数的功能、参数和返回值
    """
    # 函数体
    statements
    return value  # 可选
```

#### 函数定义示例

```python
# 1. 简单函数
def greet():
    """简单的问候函数"""
    print("Hello, World!")

# 2. 带参数的函数
def greet_person(name):
    """问候指定的人"""
    print(f"Hello, {name}!")

# 3. 带返回值的函数
def add_numbers(a, b):
    """计算两个数的和"""
    return a + b

# 4. 带默认参数的函数
def greet_with_title(name, title="先生"):
    """带称谓的问候"""
    print(f"Hello, {title}{name}!")

# 5. 可变参数函数
def sum_all(*numbers):
    """计算所有数字的和"""
    return sum(numbers)
```

#### 函数调用

```python
# 调用函数
greet()                    # Hello, World!
greet_person("Alice")      # Hello, Alice!
result = add_numbers(3, 5) # result = 8
greet_with_title("张三")   # Hello, 先生张三!
total = sum_all(1, 2, 3, 4) # total = 10
```

### 📝 代码示例

```python
# 函数定义和调用综合示例
def calculate_circle_area(radius):
    """
    计算圆的面积
    
    Args:
        radius (float): 圆的半径
        
    Returns:
        float: 圆的面积
    """
    import math
    return math.pi * radius ** 2

def calculate_rectangle_area(length, width):
    """
    计算矩形的面积
    
    Args:
        length (float): 长度
        width (float): 宽度
        
    Returns:
        float: 矩形的面积
    """
    return length * width

def calculate_triangle_area(base, height):
    """
    计算三角形的面积
    
    Args:
        base (float): 底边
        height (float): 高
        
    Returns:
        float: 三角形的面积
    """
    return 0.5 * base * height

def main():
    """主函数"""
    print("几何图形面积计算器")
    print("=" * 30)
    
    # 计算圆面积
    radius = 5
    circle_area = calculate_circle_area(radius)
    print(f"半径为{radius}的圆面积: {circle_area:.2f}")
    
    # 计算矩形面积
    length, width = 4, 6
    rectangle_area = calculate_rectangle_area(length, width)
    print(f"长{length}宽{width}的矩形面积: {rectangle_area}")
    
    # 计算三角形面积
    base, height = 3, 4
    triangle_area = calculate_triangle_area(base, height)
    print(f"底{base}高{height}的三角形面积: {triangle_area}")

if __name__ == "__main__":
    main()
```

---

## 问题37：函数的参数传递有哪些方式？

### 🤔 问题描述
Python中函数参数传递有哪些方式？位置参数、关键字参数、默认参数、可变参数有什么区别？如何正确使用它们？

### 💡 详细解答

#### 参数类型

=== "位置参数"
    ```python
    def greet(name, age, city):
        print(f"姓名: {name}, 年龄: {age}, 城市: {city}")
    
    # 按位置传递参数
    greet("张三", 25, "北京")
    ```

=== "关键字参数"
    ```python
    def greet(name, age, city):
        print(f"姓名: {name}, 年龄: {age}, 城市: {city}")
    
    # 使用关键字传递参数
    greet(name="李四", age=30, city="上海")
    greet(city="广州", name="王五", age=28)  # 顺序可以改变
    ```

=== "默认参数"
    ```python
    def greet(name, age=25, city="北京"):
        print(f"姓名: {name}, 年龄: {age}, 城市: {city}")
    
    greet("赵六")                    # 使用默认值
    greet("钱七", 35)                # 部分使用默认值
    greet("孙八", city="深圳")        # 使用关键字参数
    ```

=== "可变位置参数"
    ```python
    def sum_numbers(*args):
        """计算任意数量数字的和"""
        return sum(args)
    
    print(sum_numbers(1, 2, 3))        # 6
    print(sum_numbers(1, 2, 3, 4, 5))  # 15
    ```

=== "可变关键字参数"
    ```python
    def create_profile(**kwargs):
        """创建用户档案"""
        profile = {}
        for key, value in kwargs.items():
            profile[key] = value
        return profile
    
    profile = create_profile(name="周九", age=32, city="杭州", job="程序员")
    print(profile)
    ```

#### 参数组合

```python
def complex_function(required_arg, default_arg="默认值", *args, **kwargs):
    """
    复杂参数函数示例
    
    Args:
        required_arg: 必需参数
        default_arg: 默认参数
        *args: 可变位置参数
        **kwargs: 可变关键字参数
    """
    print(f"必需参数: {required_arg}")
    print(f"默认参数: {default_arg}")
    print(f"位置参数: {args}")
    print(f"关键字参数: {kwargs}")

# 调用示例
complex_function("必需", "自定义", 1, 2, 3, name="测试", age=25)
```

### 📝 代码示例

```python
# 参数传递综合示例
def process_data(data, operation="sum", *filters, **options):
    """
    数据处理函数
    
    Args:
        data: 要处理的数据
        operation: 操作类型，默认为"sum"
        *filters: 过滤条件
        **options: 其他选项
    """
    print(f"处理数据: {data}")
    print(f"操作类型: {operation}")
    print(f"过滤条件: {filters}")
    print(f"其他选项: {options}")
    
    # 根据操作类型处理数据
    if operation == "sum":
        result = sum(data)
    elif operation == "max":
        result = max(data)
    elif operation == "min":
        result = min(data)
    else:
        result = data
    
    return result

def main():
    """主函数"""
    numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    
    # 使用默认参数
    result1 = process_data(numbers)
    print(f"求和结果: {result1}")
    
    # 指定操作类型
    result2 = process_data(numbers, "max")
    print(f"最大值: {result2}")
    
    # 使用关键字参数
    result3 = process_data(numbers, operation="min")
    print(f"最小值: {result3}")
    
    # 使用可变参数
    result4 = process_data(numbers, "sum", "even", "positive", debug=True, verbose=False)
    print(f"复杂处理结果: {result4}")

if __name__ == "__main__":
    main()
```

---

## 问题38：什么是函数的作用域？

### 🤔 问题描述
Python中函数的作用域是什么？局部变量和全局变量有什么区别？如何在函数中访问和修改全局变量？

### 💡 详细解答

#### 作用域类型

=== "局部作用域"
    ```python
    def my_function():
        local_var = "这是局部变量"
        print(local_var)
    
    my_function()
    # print(local_var)  # 错误：局部变量在函数外不可访问
    ```

=== "全局作用域"
    ```python
    global_var = "这是全局变量"
    
    def my_function():
        print(global_var)  # 可以访问全局变量
    
    my_function()
    print(global_var)  # 在函数外也可以访问
    ```

=== "修改全局变量"
    ```python
    counter = 0
    
    def increment():
        global counter  # 声明使用全局变量
        counter += 1
    
    def decrement():
        global counter
        counter -= 1
    
    print(f"初始值: {counter}")  # 0
    increment()
    print(f"增加后: {counter}")  # 1
    decrement()
    print(f"减少后: {counter}")  # 0
    ```

#### 嵌套作用域

```python
def outer_function():
    outer_var = "外部函数变量"
    
    def inner_function():
        inner_var = "内部函数变量"
        print(f"内部函数访问外部变量: {outer_var}")
        print(f"内部函数变量: {inner_var}")
    
    inner_function()
    # print(inner_var)  # 错误：内部变量在外部不可访问

outer_function()
```

### 📝 代码示例

```python
# 作用域综合示例
# 全局变量
global_counter = 0
global_list = []

def demonstrate_scope():
    """演示作用域概念"""
    # 局部变量
    local_var = "局部变量"
    print(f"函数内访问局部变量: {local_var}")
    print(f"函数内访问全局变量: {global_counter}")
    
    # 修改全局变量
    global global_counter
    global_counter += 1
    
    # 修改全局列表（不需要global声明）
    global_list.append("新元素")
    
    def nested_function():
        """嵌套函数"""
        nested_var = "嵌套函数变量"
        print(f"嵌套函数访问外部局部变量: {local_var}")
        print(f"嵌套函数访问全局变量: {global_counter}")
        
        # 修改外部函数的局部变量
        nonlocal local_var
        local_var = "被嵌套函数修改"
        
        return nested_var
    
    result = nested_function()
    print(f"嵌套函数返回值: {result}")
    print(f"修改后的局部变量: {local_var}")

def main():
    """主函数"""
    print("=== 作用域演示 ===")
    print(f"初始全局计数器: {global_counter}")
    print(f"初始全局列表: {global_list}")
    
    demonstrate_scope()
    
    print(f"调用函数后全局计数器: {global_counter}")
    print(f"调用函数后全局列表: {global_list}")

if __name__ == "__main__":
    main()
```

### 🎯 最佳实践

1. **避免使用全局变量**：尽量使用参数传递和返回值
2. **明确变量作用域**：使用有意义的变量名
3. **谨慎修改全局变量**：使用global关键字时要小心
4. **利用嵌套作用域**：合理使用闭包
5. **遵循最小作用域原则**：变量在最小必要的作用域内定义

通过掌握函数的作用域概念，你就能编写出更清晰、更安全的Python代码！
