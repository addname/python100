# 第四章：面向对象编程

!!! info "面向对象编程基础"
    面向对象编程（OOP）是Python编程的重要范式。本章将学习类、对象、继承、多态等核心概念，以及如何设计和使用类。

## 问题51：什么是类和对象？

### 🤔 问题描述
在Python中什么是类？什么是对象？如何定义类？如何创建对象？类和对象有什么关系？

### 💡 详细解答

#### 类的基本概念

类（Class）是对象的蓝图或模板，它定义了对象的属性和方法。对象（Object）是类的实例，具有类定义的属性和行为。

#### 定义类

```python
class Person:
    """人类"""
    
    def __init__(self, name, age):
        """初始化方法"""
        self.name = name
        self.age = age
    
    def introduce(self):
        """自我介绍方法"""
        return f"我是{self.name}，今年{self.age}岁"
    
    def have_birthday(self):
        """过生日方法"""
        self.age += 1
        print(f"{self.name}过生日了，现在{self.age}岁")
```

#### 创建对象

```python
# 创建Person对象
person1 = Person("张三", 25)
person2 = Person("李四", 30)

# 访问属性
print(person1.name)  # 张三
print(person1.age)   # 25

# 调用方法
print(person1.introduce())  # 我是张三，今年25岁
person1.have_birthday()     # 张三过生日了，现在26岁
```

### 📝 代码示例

```python
# 类和对象综合示例
class BankAccount:
    """银行账户类"""
    
    def __init__(self, account_number, owner_name, initial_balance=0):
        """
        初始化银行账户
        
        Args:
            account_number (str): 账户号码
            owner_name (str): 账户持有人姓名
            initial_balance (float): 初始余额，默认为0
        """
        self.account_number = account_number
        self.owner_name = owner_name
        self.balance = initial_balance
        self.transactions = []  # 交易记录
    
    def deposit(self, amount):
        """
        存款
        
        Args:
            amount (float): 存款金额
        """
        if amount > 0:
            self.balance += amount
            self.transactions.append(f"存款: +{amount}")
            print(f"存款成功，当前余额: {self.balance}")
        else:
            print("存款金额必须大于0")
    
    def withdraw(self, amount):
        """
        取款
        
        Args:
            amount (float): 取款金额
        """
        if amount > 0:
            if amount <= self.balance:
                self.balance -= amount
                self.transactions.append(f"取款: -{amount}")
                print(f"取款成功，当前余额: {self.balance}")
            else:
                print("余额不足")
        else:
            print("取款金额必须大于0")
    
    def get_balance(self):
        """获取余额"""
        return self.balance
    
    def get_transaction_history(self):
        """获取交易记录"""
        return self.transactions
    
    def __str__(self):
        """字符串表示"""
        return f"账户: {self.account_number}, 持有人: {self.owner_name}, 余额: {self.balance}"

def main():
    """主函数"""
    print("=== 银行账户系统 ===")
    
    # 创建银行账户
    account = BankAccount("123456789", "张三", 1000)
    print(f"创建账户: {account}")
    
    # 存款
    account.deposit(500)
    account.deposit(200)
    
    # 取款
    account.withdraw(300)
    account.withdraw(2000)  # 余额不足
    
    # 查看余额
    print(f"当前余额: {account.get_balance()}")
    
    # 查看交易记录
    print("交易记录:")
    for transaction in account.get_transaction_history():
        print(f"  {transaction}")

if __name__ == "__main__":
    main()
```

---

## 问题52：什么是继承？

### 🤔 问题描述
什么是继承？如何在Python中实现继承？继承有什么好处？如何正确使用继承？

### 💡 详细解答

#### 继承的基本概念

继承是面向对象编程的重要特性，它允许一个类（子类）继承另一个类（父类）的属性和方法。

#### 实现继承

```python
# 父类
class Animal:
    """动物类"""
    
    def __init__(self, name, species):
        self.name = name
        self.species = species
    
    def make_sound(self):
        return "动物发出声音"
    
    def move(self):
        return f"{self.name}在移动"

# 子类
class Dog(Animal):
    """狗类，继承自Animal"""
    
    def __init__(self, name, breed):
        super().__init__(name, "狗")  # 调用父类构造函数
        self.breed = breed
    
    def make_sound(self):  # 重写父类方法
        return f"{self.name}汪汪叫"
    
    def fetch(self):  # 子类特有方法
        return f"{self.name}去捡球"

# 子类
class Cat(Animal):
    """猫类，继承自Animal"""
    
    def __init__(self, name, color):
        super().__init__(name, "猫")
        self.color = color
    
    def make_sound(self):  # 重写父类方法
        return f"{self.name}喵喵叫"
    
    def climb(self):  # 子类特有方法
        return f"{self.name}爬树"
```

#### 使用继承

```python
# 创建对象
dog = Dog("旺财", "金毛")
cat = Cat("咪咪", "橘色")

# 调用继承的方法
print(dog.move())  # 旺财在移动
print(cat.move())  # 咪咪在移动

# 调用重写的方法
print(dog.make_sound())  # 旺财汪汪叫
print(cat.make_sound())  # 咪咪喵喵叫

# 调用子类特有方法
print(dog.fetch())  # 旺财去捡球
print(cat.climb())  # 咪咪爬树
```

### 📝 代码示例

```python
# 继承综合示例
class Vehicle:
    """交通工具基类"""
    
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year
        self.speed = 0
        self.is_running = False
    
    def start(self):
        """启动"""
        if not self.is_running:
            self.is_running = True
            print(f"{self.brand} {self.model} 已启动")
        else:
            print("车辆已经在运行中")
    
    def stop(self):
        """停止"""
        if self.is_running:
            self.is_running = False
            self.speed = 0
            print(f"{self.brand} {self.model} 已停止")
        else:
            print("车辆已经停止")
    
    def accelerate(self, increment):
        """加速"""
        if self.is_running:
            self.speed += increment
            print(f"加速到 {self.speed} km/h")
        else:
            print("请先启动车辆")
    
    def brake(self, decrement):
        """刹车"""
        if self.speed > 0:
            self.speed = max(0, self.speed - decrement)
            print(f"减速到 {self.speed} km/h")
        else:
            print("车辆已经停止")

class Car(Vehicle):
    """汽车类"""
    
    def __init__(self, brand, model, year, doors):
        super().__init__(brand, model, year)
        self.doors = doors
        self.fuel_level = 100
    
    def refuel(self, amount):
        """加油"""
        self.fuel_level = min(100, self.fuel_level + amount)
        print(f"加油完成，油量: {self.fuel_level}%")
    
    def honk(self):
        """鸣笛"""
        return f"{self.brand} {self.model} 鸣笛：嘟嘟！"

class Motorcycle(Vehicle):
    """摩托车类"""
    
    def __init__(self, brand, model, year, engine_size):
        super().__init__(brand, model, year)
        self.engine_size = engine_size
        self.helmet_required = True
    
    def wheelie(self):
        """翘头"""
        if self.is_running and self.speed > 20:
            return f"{self.brand} {self.model} 翘头！"
        else:
            return "速度不够，无法翘头"
    
    def rev_engine(self):
        """轰油门"""
        return f"{self.brand} {self.model} 发动机轰鸣：Vroom!"

class Bicycle(Vehicle):
    """自行车类"""
    
    def __init__(self, brand, model, year, gears):
        super().__init__(brand, model, year)
        self.gears = gears
        self.current_gear = 1
    
    def shift_gear(self, gear):
        """换挡"""
        if 1 <= gear <= self.gears:
            self.current_gear = gear
            print(f"换到 {gear} 挡")
        else:
            print(f"无效挡位，共有 {self.gears} 个挡位")
    
    def pedal(self):
        """踩踏板"""
        if self.current_gear > 0:
            return f"在 {self.current_gear} 挡踩踏板"
        else:
            return "请先换挡"

def main():
    """主函数"""
    print("=== 交通工具系统 ===")
    
    # 创建不同类型的交通工具
    car = Car("丰田", "凯美瑞", 2023, 4)
    motorcycle = Motorcycle("本田", "CBR600", 2023, 600)
    bicycle = Bicycle("捷安特", "ATX", 2023, 21)
    
    # 测试汽车
    print("\n--- 汽车测试 ---")
    car.start()
    car.accelerate(50)
    print(car.honk())
    car.refuel(20)
    car.brake(30)
    car.stop()
    
    # 测试摩托车
    print("\n--- 摩托车测试 ---")
    motorcycle.start()
    motorcycle.accelerate(80)
    print(motorcycle.rev_engine())
    print(motorcycle.wheelie())
    motorcycle.brake(50)
    motorcycle.stop()
    
    # 测试自行车
    print("\n--- 自行车测试 ---")
    bicycle.shift_gear(5)
    print(bicycle.pedal())
    bicycle.shift_gear(10)
    print(bicycle.pedal())

if __name__ == "__main__":
    main()
```

### 🎯 最佳实践

1. **合理使用继承**：继承表示"是一个"关系
2. **遵循里氏替换原则**：子类应该能够替换父类
3. **使用super()调用父类方法**：保持继承链
4. **避免过深的继承层次**：保持继承结构简单
5. **优先使用组合而非继承**：灵活性和可维护性更好

通过掌握面向对象编程的基础概念，你就能设计出更优雅、更可维护的Python程序！
