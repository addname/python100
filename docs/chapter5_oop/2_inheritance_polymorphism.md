# 继承与多态

## 问题49：什么是继承？

**答：**
继承是面向对象编程的核心概念，允许一个类继承另一个类的属性和方法：

```python
# 父类（基类）
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return "Some sound"

# 子类（派生类）
class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# 使用继承
dog = Dog("Buddy")
cat = Cat("Whiskers")

print(dog.name)  # Buddy
print(dog.speak())  # Woof!
print(cat.speak())  # Meow!
```

---

## 问题50：如何实现继承？

**答：**
Python中实现继承的几种方式：

### 单继承
```python
class Vehicle:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model
    
    def start(self):
        return "Vehicle started"

class Car(Vehicle):
    def __init__(self, brand, model, doors):
        super().__init__(brand, model)  # 调用父类构造函数
        self.doors = doors
    
    def start(self):
        return f"{self.brand} {self.model} car started"
```

### 多继承
```python
class Flyable:
    def fly(self):
        return "Flying"

class Swimmable:
    def swim(self):
        return "Swimming"

class Duck(Animal, Flyable, Swimmable):
    def speak(self):
        return "Quack!"
```

---

## 问题51：什么是多态？

**答：**
多态允许不同类的对象对同一方法调用做出不同的响应：

```python
class Shape:
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2

# 多态的使用
shapes = [Rectangle(5, 3), Circle(2)]

for shape in shapes:
    print(f"Area: {shape.area()}")  # 不同的类，相同的方法调用
```
