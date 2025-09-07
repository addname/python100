# 作用域

## 问题102：局部变量和全局变量？

**答：**
Python中有不同的变量作用域：

### 局部变量
```python
def my_function():
    local_var = "I'm local"  # 局部变量
    print(local_var)

my_function()
# print(local_var)  # 错误！局部变量在函数外不可访问
```

### 全局变量
```python
global_var = "I'm global"  # 全局变量

def my_function():
    print(global_var)  # 可以访问全局变量

my_function()
print(global_var)  # 在函数外也可以访问
```

---

## 问题103：global关键字的作用？

**答：**
global关键字用于在函数内修改全局变量：

```python
count = 0  # 全局变量

def increment():
    global count  # 声明使用全局变量
    count += 1

def show_count():
    print(f"Count is: {count}")

increment()
increment()
show_count()  # Count is: 2
```

---

## 问题104：nonlocal关键字的作用？

**答：**
nonlocal关键字用于在嵌套函数中修改外层函数的变量：

```python
def outer_function():
    outer_var = "outer"
    
    def inner_function():
        nonlocal outer_var  # 声明使用外层函数的变量
        outer_var = "modified"
        print(f"Inner: {outer_var}")
    
    print(f"Before: {outer_var}")
    inner_function()
    print(f"After: {outer_var}")

outer_function()
# 输出：
# Before: outer
# Inner: modified
# After: modified
```
