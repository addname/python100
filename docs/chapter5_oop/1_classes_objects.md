# 类与对象的概念

## 问题108：什么是类和对象？

类(Class)是创建对象的模板，对象(Object)是类的实例：

```python
# 定义类
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def introduce(self):
        return f"我是{self.name}，今年{self.age}岁"

# 创建对象
person1 = Person("张三", 25)
person2 = Person("李四", 30)

# 使用对象
print(person1.introduce())  # 我是张三，今年25岁
print(person2.introduce())  # 我是李四，今年30岁
```

## 问题109：如何定义类的属性和方法？

```python
class Student:
    # 类属性
    school = "Python大学"
    
    def __init__(self, name, age, student_id):
        # 实例属性
        self.name = name
        self.age = age
        self.student_id = student_id
        self.grades = []
    
    # 实例方法
    def add_grade(self, grade):
        self.grades.append(grade)
    
    def get_average(self):
        if not self.grades:
            return 0
        return sum(self.grades) / len(self.grades)
    
    def __str__(self):
        return f"学生: {self.name}, 学号: {self.student_id}"

# 使用类
student = Student("王五", 20, "2023001")
student.add_grade(85)
student.add_grade(92)
print(student)  # 学生: 王五, 学号: 2023001
print(f"平均分: {student.get_average()}")  # 平均分: 88.5
```

## 问题110：类的构造函数__init__如何使用？

```python
class Car:
    def __init__(self, brand, model, year, color="白色"):
        self.brand = brand
        self.model = model
        self.year = year
        self.color = color
        self.mileage = 0
        self.is_running = False
    
    def start(self):
        if not self.is_running:
            self.is_running = True
            print(f"{self.brand} {self.model} 已启动")
        else:
            print("汽车已经在运行")
    
    def stop(self):
        if self.is_running:
            self.is_running = False
            print(f"{self.brand} {self.model} 已停止")
        else:
            print("汽车已经停止")
    
    def drive(self, distance):
        if self.is_running:
            self.mileage += distance
            print(f"行驶了{distance}公里，总里程: {self.mileage}公里")
        else:
            print("请先启动汽车")

# 创建汽车对象
my_car = Car("丰田", "凯美瑞", 2023, "蓝色")
my_car.start()
my_car.drive(50)
my_car.stop()
```

## 问题111：类的属性和方法有哪些类型？

```python
class BankAccount:
    # 类属性
    bank_name = "Python银行"
    interest_rate = 0.02
    
    def __init__(self, account_number, initial_balance=0):
        # 实例属性
        self.account_number = account_number
        self.balance = initial_balance
        self.transaction_history = []
    
    # 实例方法
    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self.transaction_history.append(f"存款: +{amount}")
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            self.transaction_history.append(f"取款: -{amount}")
            return True
        return False
    
    # 类方法
    @classmethod
    def create_account(cls, account_number, initial_balance=0):
        return cls(account_number, initial_balance)
    
    # 静态方法
    @staticmethod
    def calculate_interest(principal, rate, time):
        return principal * rate * time
    
    # 特殊方法
    def __str__(self):
        return f"账户: {self.account_number}, 余额: {self.balance}"
    
    def __len__(self):
        return len(self.transaction_history)

# 使用不同类型的属性和方法
account = BankAccount("123456789", 1000)
print(account.bank_name)  # 类属性
print(account.balance)    # 实例属性

account.deposit(500)      # 实例方法
print(account)

# 类方法
new_account = BankAccount.create_account("987654321", 2000)
print(new_account)

# 静态方法
interest = BankAccount.calculate_interest(1000, 0.02, 1)
print(f"利息: {interest}")
```

## 问题112：类的封装是什么？

```python
class BankAccount:
    def __init__(self, account_number, initial_balance=0):
        # 私有属性（使用双下划线）
        self.__account_number = account_number
        self.__balance = initial_balance
        self.__transaction_history = []
    
    # 公共方法
    def get_balance(self):
        return self.__balance
    
    def get_account_number(self):
        return self.__account_number
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            self.__transaction_history.append(f"存款: +{amount}")
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            self.__transaction_history.append(f"取款: -{amount}")
            return True
        return False
    
    def get_transaction_history(self):
        return self.__transaction_history.copy()  # 返回副本

# 使用封装
account = BankAccount("123456789", 1000)
print(account.get_balance())  # 1000
account.deposit(500)
print(account.get_balance())  # 1500

# 无法直接访问私有属性
# print(account.__balance)  # 错误：AttributeError
```

## 问题113：类的继承是什么？

```python
# 父类
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def eat(self):
        print(f"{self.name} 正在吃东西")
    
    def sleep(self):
        print(f"{self.name} 正在睡觉")
    
    def make_sound(self):
        print(f"{self.name} 发出了声音")

# 子类
class Dog(Animal):
    def __init__(self, name, age, breed):
        super().__init__(name, age)  # 调用父类构造函数
        self.breed = breed
    
    def make_sound(self):  # 重写父类方法
        print(f"{self.name} 汪汪叫")
    
    def fetch(self):  # 子类特有方法
        print(f"{self.name} 正在捡球")

class Cat(Animal):
    def __init__(self, name, age, color):
        super().__init__(name, age)
        self.color = color
    
    def make_sound(self):
        print(f"{self.name} 喵喵叫")
    
    def climb(self):
        print(f"{self.name} 正在爬树")

# 使用继承
dog = Dog("旺财", 3, "金毛")
cat = Cat("咪咪", 2, "橘色")

dog.eat()        # 继承自父类
dog.make_sound() # 重写的方法
dog.fetch()      # 子类特有方法

cat.sleep()      # 继承自父类
cat.make_sound() # 重写的方法
cat.climb()      # 子类特有方法
```

## 问题114：类的多态是什么？

```python
# 多态示例
class Shape:
    def area(self):
        pass
    
    def perimeter(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

# 多态的使用
def print_shape_info(shape):
    print(f"面积: {shape.area():.2f}")
    print(f"周长: {shape.perimeter():.2f}")

# 创建不同形状的对象
rectangle = Rectangle(5, 3)
circle = Circle(4)

# 多态调用
print_shape_info(rectangle)  # 面积: 15.00, 周长: 16.00
print_shape_info(circle)     # 面积: 50.27, 周长: 25.13
```

## 问题115：类的特殊方法有哪些？

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    # 字符串表示
    def __str__(self):
        return f"《{self.title}》- {self.author}"
    
    def __repr__(self):
        return f"Book('{self.title}', '{self.author}', {self.pages})"
    
    # 比较方法
    def __eq__(self, other):
        return self.title == other.title and self.author == other.author
    
    def __lt__(self, other):
        return self.pages < other.pages
    
    # 长度
    def __len__(self):
        return self.pages
    
    # 哈希
    def __hash__(self):
        return hash((self.title, self.author))

# 使用特殊方法
book1 = Book("Python编程", "张三", 300)
book2 = Book("Java编程", "李四", 250)
book3 = Book("Python编程", "张三", 300)

print(book1)           # 《Python编程》- 张三
print(repr(book1))     # Book('Python编程', '张三', 300)
print(book1 == book3)  # True
print(book1 < book2)   # False
print(len(book1))      # 300
```

## 问题116：类的实际应用场景有哪些？

```python
# 1. 用户管理系统
class User:
    def __init__(self, username, email, password):
        self.username = username
        self.email = email
        self.__password = password
        self.is_active = True
        self.created_at = "2023-01-01"
    
    def authenticate(self, password):
        return self.__password == password
    
    def change_password(self, old_password, new_password):
        if self.authenticate(old_password):
            self.__password = new_password
            return True
        return False

# 2. 购物车系统
class ShoppingCart:
    def __init__(self):
        self.items = {}
        self.total = 0
    
    def add_item(self, product, quantity=1):
        if product in self.items:
            self.items[product] += quantity
        else:
            self.items[product] = quantity
        self.calculate_total()
    
    def remove_item(self, product):
        if product in self.items:
            del self.items[product]
            self.calculate_total()
    
    def calculate_total(self):
        self.total = sum(self.items.values())

# 3. 文件管理系统
class File:
    def __init__(self, name, size, content=""):
        self.name = name
        self.size = size
        self.content = content
        self.created_at = "2023-01-01"
        self.modified_at = "2023-01-01"
    
    def read(self):
        return self.content
    
    def write(self, content):
        self.content = content
        self.size = len(content)
        self.modified_at = "2023-01-02"
    
    def append(self, content):
        self.content += content
        self.size = len(self.content)
        self.modified_at = "2023-01-02"
```

## 问题117：类的最佳实践

```python
# 1. 使用属性装饰器
class Temperature:
    def __init__(self, celsius=0):
        self._celsius = celsius
    
    @property
    def celsius(self):
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("温度不能低于绝对零度")
        self._celsius = value
    
    @property
    def fahrenheit(self):
        return self._celsius * 9/5 + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        self.celsius = (value - 32) * 5/9

# 2. 使用数据类
from dataclasses import dataclass

@dataclass
class Point:
    x: float
    y: float
    
    def distance_from_origin(self):
        return (self.x**2 + self.y**2)**0.5

# 3. 使用抽象基类
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
    
    @abstractmethod
    def perimeter(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
```

## 总结

类和对象是面向对象编程的基础，要点包括：
- **类定义**：使用class关键字定义类
- **对象创建**：通过类创建对象实例
- **属性和方法**：实例属性、类属性、实例方法、类方法、静态方法
- **封装**：使用私有属性和公共方法
- **继承**：子类继承父类的属性和方法
- **多态**：同一接口，不同实现
- **特殊方法**：__init__、__str__、__eq__等
- **最佳实践**：属性装饰器、数据类、抽象基类
