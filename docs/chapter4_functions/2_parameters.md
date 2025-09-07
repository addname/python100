# 参数传递

## 问题99：位置参数和关键字参数？

**答：**
Python支持两种参数传递方式：

### 位置参数
```python
def greet(name, age, city):
    return f"Hello {name}, you are {age} years old from {city}"

# 按位置传递参数
result = greet("Alice", 25, "Beijing")
```

### 关键字参数
```python
# 使用关键字传递参数
result = greet(name="Alice", age=25, city="Beijing")

# 混合使用（位置参数必须在关键字参数之前）
result = greet("Alice", age=25, city="Beijing")
```

---

## 问题100：默认参数的使用？

**答：**
默认参数允许函数在没有提供参数时使用预设值：

```python
def greet(name, age=18, city="Unknown"):
    return f"Hello {name}, you are {age} years old from {city}"

# 使用默认值
result1 = greet("Alice")  # Hello Alice, you are 18 years old from Unknown

# 部分使用默认值
result2 = greet("Bob", 30)  # Hello Bob, you are 30 years old from Unknown

# 覆盖默认值
result3 = greet("Charlie", 25, "Shanghai")  # Hello Charlie, you are 25 years old from Shanghai
```

---

## 问题101：可变参数*args和**kwargs？

**答：**
可变参数允许函数接受任意数量的参数：

### *args（位置参数）
```python
def sum_all(*args):
    total = 0
    for num in args:
        total += num
    return total

# 可以传递任意数量的参数
result1 = sum_all(1, 2, 3)  # 6
result2 = sum_all(1, 2, 3, 4, 5)  # 15
```

### **kwargs（关键字参数）
```python
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

# 可以传递任意数量的关键字参数
print_info(name="Alice", age=25, city="Beijing")
```

### 组合使用
```python
def complex_function(required, *args, **kwargs):
    print(f"Required: {required}")
    print(f"Args: {args}")
    print(f"Kwargs: {kwargs}")

complex_function("hello", 1, 2, 3, name="Alice", age=25)
```
