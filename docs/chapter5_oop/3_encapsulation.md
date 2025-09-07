# 封装与访问控制

## 问题121：什么是封装？

**答：**
封装是面向对象编程的基本概念，将数据和方法包装在类中，并控制对它们的访问：

```python
class BankAccount:
    def __init__(self, initial_balance):
        self._balance = initial_balance  # 受保护的属性
    
    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            return True
        return False
    
    def get_balance(self):
        return self._balance

# 使用封装
account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 1500
```

---

## 问题122：私有属性和方法？

**答：**
Python使用下划线约定来表示访问级别：

### 单下划线（受保护）
```python
class MyClass:
    def __init__(self):
        self._protected_var = "protected"  # 约定为受保护
    
    def _protected_method(self):
        return "This is protected"
```

### 双下划线（私有）
```python
class MyClass:
    def __init__(self):
        self.__private_var = "private"  # 私有属性
    
    def __private_method(self):
        return "This is private"
    
    def public_method(self):
        return self.__private_var  # 类内部可以访问
```

---

## 问题123：属性装饰器@property？

**答：**
@property装饰器允许将方法当作属性来访问：

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def radius(self):
        return self._radius
    
    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value
    
    @property
    def area(self):
        return 3.14159 * self._radius ** 2

# 使用属性
circle = Circle(5)
print(circle.radius)  # 5
print(circle.area)    # 78.54

circle.radius = 10    # 使用setter
print(circle.area)    # 314.159
```
