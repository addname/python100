# Python基础语法 (5-8问)

!!! info "Python语法基础"
    Python以其简洁优雅的语法而闻名。掌握Python的基础语法是编程的第一步，也是最重要的一步。

## 问题5：Python的语法特点是什么？

### 🤔 问题描述
Python与其他编程语言相比有什么独特的语法特点？为什么Python被称为"可读性最强的编程语言"？

### 💡 详细解答

#### Python语法特点

=== "简洁优雅"
    **特点：** 代码简洁，表达力强
    
    **对比示例：**
    ```python
    # Python - 简洁
    numbers = [1, 2, 3, 4, 5]
    squares = [x**2 for x in numbers]
    
    # Java - 冗长
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
    List<Integer> squares = new ArrayList<>();
    for (Integer x : numbers) {
        squares.add(x * x);
    }
    ```

=== "强制缩进"
    **特点：** 使用缩进来表示代码块，而不是大括号
    
    ```python
    # Python使用缩进
    if condition:
        print("条件为真")
        if nested_condition:
            print("嵌套条件为真")
    else:
        print("条件为假")
    
    # 其他语言使用大括号
    # if (condition) {
    #     print("条件为真");
    #     if (nested_condition) {
    #         print("嵌套条件为真");
    #     }
    # } else {
    #     print("条件为假");
    # }
    ```

=== "动态类型"
    **特点：** 变量类型在运行时确定
    
    ```python
    # 同一个变量可以存储不同类型的值
    x = 42          # 整数
    x = "Hello"     # 字符串
    x = [1, 2, 3]   # 列表
    x = {"a": 1}    # 字典
    ```

=== "解释型语言"
    **特点：** 代码逐行执行，便于调试
    
    ```python
    # 可以逐行测试
    >>> 2 + 3
    5
    >>> "Hello" + " World"
    'Hello World'
    >>> import math
    >>> math.sqrt(16)
    4.0
    ```

#### Python设计哲学

Python遵循"Python之禅"（The Zen of Python）：

```python
import this
```

**核心原则：**
- **Beautiful is better than ugly** - 优美胜于丑陋
- **Explicit is better than implicit** - 明确胜于隐晦
- **Simple is better than complex** - 简单胜于复杂
- **Readability counts** - 可读性很重要

### 📝 代码示例

**Python语法优势展示：**

```python
# 1. 简洁的列表操作
numbers = [1, 2, 3, 4, 5]
even_squares = [x**2 for x in numbers if x % 2 == 0]
print(even_squares)  # [4, 16]

# 2. 优雅的字符串处理
name = "  Python  "
clean_name = name.strip().title()
print(f"Hello, {clean_name}!")  # Hello, Python!

# 3. 简洁的字典操作
person = {"name": "Alice", "age": 30, "city": "Beijing"}
person_info = f"{person['name']} is {person['age']} years old"
print(person_info)  # Alice is 30 years old

# 4. 函数式编程风格
def is_even(x):
    return x % 2 == 0

numbers = [1, 2, 3, 4, 5, 6]
even_numbers = list(filter(is_even, numbers))
print(even_numbers)  # [2, 4, 6]

# 5. 简洁的异常处理
try:
    result = 10 / 0
except ZeroDivisionError:
    print("不能除以零")
```

---

## 问题6：Python中的注释和文档字符串如何使用？

### 🤔 问题描述
在Python中如何添加注释？单行注释和多行注释有什么区别？什么是文档字符串？如何编写规范的文档？

### 💡 详细解答

#### 注释类型

=== "单行注释"
    ```python
    # 这是单行注释
    x = 5  # 这也是单行注释
    
    # 注释可以解释代码的作用
    result = x * 2  # 计算x的两倍
    ```

=== "多行注释"
    ```python
    """
    这是多行注释
    可以跨越多行
    通常用于函数或类的说明
    """
    
    # 或者使用多个单行注释
    # 这是多行注释的另一种方式
    # 可以跨越多行
    # 通常用于临时注释掉代码块
    ```

#### 文档字符串（Docstring）

文档字符串是Python的重要特性，用于描述函数、类、模块的功能。

=== "函数文档字符串"
    ```python
    def calculate_area(length, width):
        """
        计算矩形的面积
        
        Args:
            length (float): 矩形的长度
            width (float): 矩形的宽度
            
        Returns:
            float: 矩形的面积
            
        Raises:
            ValueError: 当长度或宽度为负数时抛出
            
        Example:
            >>> calculate_area(5, 3)
            15.0
        """
        if length < 0 or width < 0:
            raise ValueError("长度和宽度必须为正数")
        return length * width
    ```

=== "类文档字符串"
    ```python
    class Rectangle:
        """
        矩形类
        
        用于表示和操作矩形对象，提供面积和周长计算功能。
        
        Attributes:
            length (float): 矩形的长度
            width (float): 矩形的宽度
            
        Example:
            >>> rect = Rectangle(5, 3)
            >>> rect.area()
            15.0
        """
        
        def __init__(self, length, width):
            """
            初始化矩形对象
            
            Args:
                length (float): 矩形的长度
                width (float): 矩形的宽度
            """
            self.length = length
            self.width = width
        
        def area(self):
            """计算矩形面积"""
            return self.length * self.width
        
        def perimeter(self):
            """计算矩形周长"""
            return 2 * (self.length + self.width)
    ```

=== "模块文档字符串"
    ```python
    """
    数学工具模块
    
    提供常用的数学计算函数，包括几何图形计算、
    统计函数等。
    
    Author: 夏光
    Version: 1.0.0
    Date: 2024-01-01
    """
    
    import math
    
    def circle_area(radius):
        """计算圆的面积"""
        return math.pi * radius ** 2
    
    def circle_circumference(radius):
        """计算圆的周长"""
        return 2 * math.pi * radius
    ```

#### 文档字符串规范

=== "Google风格"
    ```python
    def process_data(data, options=None):
        """处理数据并返回结果
        
        Args:
            data (list): 要处理的数据列表
            options (dict, optional): 处理选项. Defaults to None.
            
        Returns:
            dict: 处理结果，包含统计信息和处理后的数据
            
        Raises:
            ValueError: 当数据为空时抛出
            TypeError: 当数据类型不正确时抛出
            
        Example:
            >>> data = [1, 2, 3, 4, 5]
            >>> result = process_data(data)
            >>> print(result['count'])
            5
        """
        if not data:
            raise ValueError("数据不能为空")
        
        if not isinstance(data, list):
            raise TypeError("数据必须是列表类型")
        
        return {
            'count': len(data),
            'sum': sum(data),
            'average': sum(data) / len(data),
            'processed_data': [x * 2 for x in data]
        }
    ```

=== "NumPy风格"
    ```python
    def normalize_data(data, method='minmax'):
        """标准化数据
        
        Parameters
        ----------
        data : array_like
            要标准化的数据
        method : {'minmax', 'zscore'}, optional
            标准化方法，默认为'minmax'
            
        Returns
        -------
        numpy.ndarray
            标准化后的数据
            
        Raises
        ------
        ValueError
            当method参数无效时
        TypeError
            当data不是数值类型时
            
        Examples
        --------
        >>> data = [1, 2, 3, 4, 5]
        >>> normalized = normalize_data(data)
        >>> print(normalized)
        [0.   0.25 0.5  0.75 1.  ]
        """
        import numpy as np
        
        data = np.array(data)
        
        if method == 'minmax':
            return (data - data.min()) / (data.max() - data.min())
        elif method == 'zscore':
            return (data - data.mean()) / data.std()
        else:
            raise ValueError(f"不支持的标准化方法: {method}")
    ```

### 📝 代码示例

**完整的文档示例：**

```python
"""
用户管理模块

提供用户注册、登录、信息管理等功能。

Author: 夏光
Version: 1.0.0
Created: 2024-01-01
"""

import hashlib
import re
from datetime import datetime
from typing import Dict, List, Optional, Tuple


class User:
    """
    用户类
    
    表示系统中的用户对象，包含用户的基本信息和操作方法。
    
    Attributes:
        username (str): 用户名
        email (str): 邮箱地址
        created_at (datetime): 创建时间
        is_active (bool): 是否激活状态
        
    Example:
        >>> user = User("alice", "alice@example.com")
        >>> user.set_password("password123")
        >>> user.verify_password("password123")
        True
    """
    
    def __init__(self, username: str, email: str):
        """
        初始化用户对象
        
        Args:
            username (str): 用户名，长度3-20字符
            email (str): 邮箱地址，必须符合邮箱格式
            
        Raises:
            ValueError: 当用户名或邮箱格式不正确时
        """
        if not self._validate_username(username):
            raise ValueError("用户名必须是3-20个字符的字母数字组合")
        
        if not self._validate_email(email):
            raise ValueError("邮箱格式不正确")
        
        self.username = username
        self.email = email
        self.created_at = datetime.now()
        self.is_active = True
        self._password_hash = None
    
    def set_password(self, password: str) -> None:
        """
        设置用户密码
        
        密码会被哈希处理后存储，不会保存明文密码。
        
        Args:
            password (str): 明文密码，长度至少6位
            
        Raises:
            ValueError: 当密码长度不足时
        """
        if len(password) < 6:
            raise ValueError("密码长度至少6位")
        
        # 使用SHA-256哈希密码
        self._password_hash = hashlib.sha256(password.encode()).hexdigest()
    
    def verify_password(self, password: str) -> bool:
        """
        验证用户密码
        
        Args:
            password (str): 要验证的明文密码
            
        Returns:
            bool: 密码是否正确
        """
        if self._password_hash is None:
            return False
        
        password_hash = hashlib.sha256(password.encode()).hexdigest()
        return password_hash == self._password_hash
    
    @staticmethod
    def _validate_username(username: str) -> bool:
        """验证用户名格式"""
        return bool(re.match(r'^[a-zA-Z0-9_]{3,20}$', username))
    
    @staticmethod
    def _validate_email(email: str) -> bool:
        """验证邮箱格式"""
        pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
        return bool(re.match(pattern, email))
    
    def to_dict(self) -> Dict:
        """
        将用户对象转换为字典
        
        Returns:
            dict: 包含用户信息的字典，不包含密码哈希
        """
        return {
            'username': self.username,
            'email': self.email,
            'created_at': self.created_at.isoformat(),
            'is_active': self.is_active
        }
    
    def __str__(self) -> str:
        """返回用户的字符串表示"""
        return f"User(username='{self.username}', email='{self.email}')"
    
    def __repr__(self) -> str:
        """返回用户的详细字符串表示"""
        return (f"User(username='{self.username}', email='{self.email}', "
                f"created_at='{self.created_at}', is_active={self.is_active})")


class UserManager:
    """
    用户管理器
    
    提供用户的增删改查功能，以及用户数据的持久化。
    
    Attributes:
        users (List[User]): 用户列表
        _next_id (int): 下一个用户ID
        
    Example:
        >>> manager = UserManager()
        >>> user = manager.create_user("alice", "alice@example.com", "password123")
        >>> found_user = manager.find_user_by_username("alice")
    """
    
    def __init__(self):
        """初始化用户管理器"""
        self.users: List[User] = []
        self._next_id = 1
    
    def create_user(self, username: str, email: str, password: str) -> User:
        """
        创建新用户
        
        Args:
            username (str): 用户名
            email (str): 邮箱地址
            password (str): 密码
            
        Returns:
            User: 创建的用户对象
            
        Raises:
            ValueError: 当用户名或邮箱已存在时
        """
        # 检查用户名是否已存在
        if self.find_user_by_username(username):
            raise ValueError(f"用户名 '{username}' 已存在")
        
        # 检查邮箱是否已存在
        if self.find_user_by_email(email):
            raise ValueError(f"邮箱 '{email}' 已存在")
        
        # 创建用户
        user = User(username, email)
        user.set_password(password)
        self.users.append(user)
        
        return user
    
    def find_user_by_username(self, username: str) -> Optional[User]:
        """
        根据用户名查找用户
        
        Args:
            username (str): 用户名
            
        Returns:
            Optional[User]: 找到的用户对象，如果不存在返回None
        """
        for user in self.users:
            if user.username == username:
                return user
        return None
    
    def find_user_by_email(self, email: str) -> Optional[User]:
        """
        根据邮箱查找用户
        
        Args:
            email (str): 邮箱地址
            
        Returns:
            Optional[User]: 找到的用户对象，如果不存在返回None
        """
        for user in self.users:
            if user.email == email:
                return user
        return None
    
    def authenticate_user(self, username: str, password: str) -> Tuple[bool, Optional[User]]:
        """
        用户认证
        
        Args:
            username (str): 用户名
            password (str): 密码
            
        Returns:
            Tuple[bool, Optional[User]]: (认证是否成功, 用户对象)
        """
        user = self.find_user_by_username(username)
        if user and user.verify_password(password):
            return True, user
        return False, None
    
    def get_all_users(self) -> List[Dict]:
        """
        获取所有用户信息
        
        Returns:
            List[Dict]: 所有用户的字典列表
        """
        return [user.to_dict() for user in self.users]
    
    def get_user_count(self) -> int:
        """
        获取用户总数
        
        Returns:
            int: 用户总数
        """
        return len(self.users)


# 使用示例
if __name__ == "__main__":
    # 创建用户管理器
    manager = UserManager()
    
    try:
        # 创建用户
        user1 = manager.create_user("alice", "alice@example.com", "password123")
        user2 = manager.create_user("bob", "bob@example.com", "password456")
        
        print(f"创建用户: {user1}")
        print(f"创建用户: {user2}")
        
        # 用户认证
        success, user = manager.authenticate_user("alice", "password123")
        if success:
            print(f"认证成功: {user}")
        else:
            print("认证失败")
        
        # 获取所有用户
        all_users = manager.get_all_users()
        print(f"所有用户: {all_users}")
        
        print(f"用户总数: {manager.get_user_count()}")
        
    except ValueError as e:
        print(f"错误: {e}")
```

### 🎯 最佳实践

1. **及时添加注释**：解释复杂的逻辑和算法
2. **使用有意义的变量名**：减少对注释的依赖
3. **编写详细的文档字符串**：特别是公共API
4. **遵循PEP 257**：文档字符串的编写规范
5. **使用类型提示**：提高代码可读性
6. **保持注释更新**：代码修改时同步更新注释

---

## 问题7：Python中的缩进规则是什么？

### 🤔 问题描述
为什么Python使用缩进来表示代码块？缩进有什么规则？如何处理缩进错误？不同缩进方式有什么区别？

### 💡 详细解答

#### 缩进的重要性

Python使用缩进来表示代码块的层次结构，这是Python语法的核心特征：

```python
# 缩进决定代码块
if True:
    print("这行有缩进")      # 属于if语句块
    print("这行也有缩进")    # 属于if语句块
print("这行没有缩进")        # 不属于if语句块
```

#### 缩进规则

=== "基本规则"
    ```python
    # 1. 使用4个空格作为标准缩进（推荐）
    def function():
        if condition:
            print("4个空格缩进")
            if nested_condition:
                print("8个空格缩进")
    
    # 2. 也可以使用Tab，但不推荐混用
    def function():
        if condition:
            print("Tab缩进")
    
    # 3. 缩进必须一致
    def function():
        if condition:
            print("4个空格")
          print("错误：缩进不一致")  # IndentationError
    ```

=== "常见缩进错误"
    ```python
    # 错误1：缺少缩进
    if True:
    print("错误：缺少缩进")
    
    # 错误2：缩进不一致
    if True:
        print("4个空格")
      print("2个空格")  # 错误
    
    # 错误3：意外的缩进
    print("正常")
        print("错误：不应该有缩进")
    
    # 错误4：混合使用空格和Tab
    if True:
        print("4个空格")
        print("Tab")  # 错误：混用
    ```

#### 缩进最佳实践

=== "使用4个空格"
    ```python
    # 推荐：使用4个空格
    class MyClass:
        def __init__(self):
            self.value = 0
        
        def method(self):
            if self.value > 0:
                return "正数"
            else:
                return "非正数"
    ```

=== "配置编辑器"
    ```python
    # VS Code配置 (.vscode/settings.json)
    {
        "python.defaultInterpreterPath": "python3",
        "editor.tabSize": 4,
        "editor.insertSpaces": true,
        "editor.detectIndentation": false,
        "python.linting.enabled": true,
        "python.linting.pylintEnabled": true
    }
    ```

=== "使用工具检查"
    ```python
    # 使用autopep8自动格式化
    # pip install autopep8
    # autopep8 --in-place --aggressive --aggressive script.py
    
    # 使用black格式化
    # pip install black
    # black script.py
    
    # 使用flake8检查
    # pip install flake8
    # flake8 script.py
    ```

### 📝 代码示例

**缩进示例程序：**

```python
"""
缩进规则演示程序

展示Python中缩进的各种用法和最佳实践。
"""

def demonstrate_indentation():
    """演示缩进规则"""
    
    # 1. 基本缩进
    print("=== 基本缩进演示 ===")
    
    if True:
        print("这是if语句块的内容")
        print("必须有相同的缩进")
    
    # 2. 嵌套缩进
    print("\n=== 嵌套缩进演示 ===")
    
    for i in range(3):
        print(f"外层循环: {i}")
        for j in range(2):
            print(f"  内层循环: {j}")
            if j == 1:
                print(f"    条件满足: j={j}")
    
    # 3. 函数缩进
    print("\n=== 函数缩进演示 ===")
    
    def nested_function(x):
        """嵌套函数示例"""
        if x > 0:
            return x * 2
        else:
            return 0
    
    result = nested_function(5)
    print(f"函数结果: {result}")
    
    # 4. 类缩进
    print("\n=== 类缩进演示 ===")
    
    class ExampleClass:
        """示例类"""
        
        def __init__(self, value):
            self.value = value
        
        def get_value(self):
            """获取值"""
            return self.value
        
        def set_value(self, new_value):
            """设置值"""
            if new_value >= 0:
                self.value = new_value
            else:
                raise ValueError("值不能为负数")
    
    obj = ExampleClass(10)
    print(f"对象值: {obj.get_value()}")


def handle_indentation_errors():
    """处理缩进错误"""
    print("\n=== 缩进错误处理 ===")
    
    try:
        # 故意制造缩进错误
        if True:
        print("这行缺少缩进")  # 这会导致IndentationError
    except IndentationError as e:
        print(f"捕获缩进错误: {e}")
        print("解决方案：确保代码块有正确的缩进")


def indentation_best_practices():
    """缩进最佳实践"""
    print("\n=== 缩进最佳实践 ===")
    
    # 1. 使用4个空格
    data = [1, 2, 3, 4, 5]
    
    # 2. 长行缩进
    result = some_function_with_long_name(
        argument1="value1",
        argument2="value2",
        argument3="value3"
    )
    
    # 3. 列表缩进
    items = [
        "item1",
        "item2",
        "item3",
        "item4"
    ]
    
    # 4. 字典缩进
    config = {
        "database": {
            "host": "localhost",
            "port": 5432,
            "name": "mydb"
        },
        "cache": {
            "enabled": True,
            "ttl": 3600
        }
    }
    
    print("缩进配置完成")


def some_function_with_long_name(argument1, argument2, argument3):
    """模拟长函数名"""
    return f"{argument1}-{argument2}-{argument3}"


def check_indentation_consistency():
    """检查缩进一致性"""
    print("\n=== 缩进一致性检查 ===")
    
    # 使用inspect模块检查缩进
    import inspect
    
    def sample_function():
        if True:
            return "缩进正确"
    
    source_lines = inspect.getsourcelines(sample_function)[0]
    print("函数源代码:")
    for i, line in enumerate(source_lines, 1):
        print(f"{i:2d}: {repr(line)}")


if __name__ == "__main__":
    # 运行所有演示
    demonstrate_indentation()
    handle_indentation_errors()
    indentation_best_practices()
    check_indentation_consistency()
    
    print("\n=== 缩进规则总结 ===")
    print("1. 使用4个空格作为标准缩进")
    print("2. 同一代码块内缩进必须一致")
    print("3. 不要混用空格和Tab")
    print("4. 使用编辑器自动格式化功能")
    print("5. 使用工具检查缩进错误")
```

### 🎯 最佳实践

1. **使用4个空格**：这是Python官方推荐的缩进方式
2. **保持一致性**：整个项目使用相同的缩进方式
3. **配置编辑器**：设置自动缩进和格式化
4. **使用工具**：autopep8、black、flake8等
5. **避免混用**：不要同时使用空格和Tab
6. **及时检查**：运行代码前检查缩进错误

---

## 问题8：Python中的标识符命名规则是什么？

### 🤔 问题描述
在Python中如何命名变量、函数、类等标识符？有哪些命名规则和约定？什么是PEP 8命名规范？

### 💡 详细解答

#### 基本命名规则

=== "合法字符"
    ```python
    # 1. 只能包含字母、数字、下划线
    valid_names = [
        "name",           # 纯字母
        "name123",        # 字母+数字
        "user_name",      # 字母+下划线
        "name_123",       # 字母+下划线+数字
        "_private",       # 下划线开头
        "__special__"     # 双下划线
    ]
    
    # 2. 不能以数字开头
    # 123name = "错误"    # SyntaxError
    # 2user = "错误"      # SyntaxError
    
    # 3. 不能使用关键字
    # class = "错误"      # SyntaxError
    # def = "错误"        # SyntaxError
    # if = "错误"         # SyntaxError
    ```

=== "关键字列表"
    ```python
    import keyword
    
    # 查看所有关键字
    print("Python关键字:")
    print(keyword.kwlist)
    
    # 检查是否为关键字
    print(keyword.iskeyword("class"))  # True
    print(keyword.iskeyword("name"))   # False
    ```

#### PEP 8命名约定

PEP 8是Python官方的代码风格指南，定义了命名约定：

=== "变量和函数"
    ```python
    # 使用小写字母和下划线（snake_case）
    user_name = "alice"
    user_age = 25
    is_active = True
    
    def calculate_total_price():
        return 100
    
    def get_user_info(user_id):
        return {"id": user_id, "name": "alice"}
    
    # 私有变量使用单下划线前缀
    _internal_variable = "内部使用"
    
    def _helper_function():
        return "辅助函数"
    ```

=== "常量"
    ```python
    # 使用大写字母和下划线
    MAX_CONNECTIONS = 100
    DEFAULT_TIMEOUT = 30
    API_BASE_URL = "https://api.example.com"
    
    # 在模块级别定义
    class Config:
        DATABASE_URL = "sqlite:///app.db"
        SECRET_KEY = "your-secret-key"
        DEBUG = False
    ```

=== "类名"
    ```python
    # 使用大驼峰命名（PascalCase）
    class UserManager:
        pass
    
    class DatabaseConnection:
        pass
    
    class HTTPRequestHandler:
        pass
    
    # 异常类以Error结尾
    class ValidationError(Exception):
        pass
    
    class DatabaseError(Exception):
        pass
    ```

=== "方法和属性"
    ```python
    class User:
        def __init__(self, name, email):
            self.name = name
            self.email = email
            self._password_hash = None  # 私有属性
        
        def get_full_name(self):  # 公共方法
            return self.name
        
        def _validate_email(self):  # 私有方法
            return "@" in self.email
        
        def __str__(self):  # 特殊方法
            return f"User({self.name})"
    ```

#### 特殊命名约定

=== "私有成员"
    ```python
    class Example:
        def __init__(self):
            self.public_attr = "公共属性"
            self._protected_attr = "受保护属性"  # 单下划线
            self.__private_attr = "私有属性"     # 双下划线
        
        def public_method(self):
            return "公共方法"
        
        def _protected_method(self):
            return "受保护方法"
        
        def __private_method(self):
            return "私有方法"
    
    # 使用示例
    obj = Example()
    print(obj.public_attr)        # 可以访问
    print(obj._protected_attr)    # 可以访问（约定上不应该）
    # print(obj.__private_attr)   # 不能直接访问
    ```

=== "特殊方法"
    ```python
    class Vector:
        def __init__(self, x, y):
            self.x = x
            self.y = y
        
        def __add__(self, other):  # 加法运算符
            return Vector(self.x + other.x, self.y + other.y)
        
        def __str__(self):  # 字符串表示
            return f"Vector({self.x}, {self.y})"
        
        def __len__(self):  # 长度
            return 2
        
        def __getitem__(self, index):  # 索引访问
            if index == 0:
                return self.x
            elif index == 1:
                return self.y
            else:
                raise IndexError("索引超出范围")
    
    # 使用示例
    v1 = Vector(1, 2)
    v2 = Vector(3, 4)
    v3 = v1 + v2
    print(v3)  # Vector(4, 6)
    print(len(v3))  # 2
    print(v3[0])  # 4
    ```

### 📝 代码示例

**完整的命名规范示例：**

```python
"""
Python命名规范演示

展示PEP 8命名约定的各种用法和最佳实践。
"""

# 模块级常量
MAX_RETRY_COUNT = 3
DEFAULT_TIMEOUT = 30
API_VERSION = "v1"

# 模块级变量
current_user = None
debug_mode = False


class UserService:
    """用户服务类"""
    
    # 类常量
    DEFAULT_PAGE_SIZE = 20
    MAX_USERNAME_LENGTH = 50
    
    def __init__(self, database_url):
        """初始化用户服务"""
        self.database_url = database_url
        self._connection = None  # 私有属性
        self._cache = {}  # 私有缓存
    
    def create_user(self, username, email, password):
        """
        创建用户
        
        Args:
            username (str): 用户名
            email (str): 邮箱
            password (str): 密码
            
        Returns:
            User: 创建的用户对象
        """
        # 验证输入
        self._validate_username(username)
        self._validate_email(email)
        self._validate_password(password)
        
        # 创建用户
        user = User(username, email)
        user.set_password(password)
        
        # 保存到数据库
        self._save_user(user)
        
        return user
    
    def get_user_by_id(self, user_id):
        """根据ID获取用户"""
        # 先检查缓存
        if user_id in self._cache:
            return self._cache[user_id]
        
        # 从数据库获取
        user = self._fetch_user_from_db(user_id)
        if user:
            self._cache[user_id] = user
        
        return user
    
    def _validate_username(self, username):
        """验证用户名（私有方法）"""
        if not username:
            raise ValueError("用户名不能为空")
        
        if len(username) > self.MAX_USERNAME_LENGTH:
            raise ValueError(f"用户名长度不能超过{self.MAX_USERNAME_LENGTH}个字符")
        
        if not username.replace("_", "").isalnum():
            raise ValueError("用户名只能包含字母、数字和下划线")
    
    def _validate_email(self, email):
        """验证邮箱（私有方法）"""
        import re
        pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
        if not re.match(pattern, email):
            raise ValueError("邮箱格式不正确")
    
    def _validate_password(self, password):
        """验证密码（私有方法）"""
        if len(password) < 8:
            raise ValueError("密码长度至少8位")
        
        if not any(c.isupper() for c in password):
            raise ValueError("密码必须包含大写字母")
        
        if not any(c.islower() for c in password):
            raise ValueError("密码必须包含小写字母")
        
        if not any(c.isdigit() for c in password):
            raise ValueError("密码必须包含数字")
    
    def _save_user(self, user):
        """保存用户到数据库（私有方法）"""
        # 模拟数据库保存
        print(f"保存用户: {user.username}")
    
    def _fetch_user_from_db(self, user_id):
        """从数据库获取用户（私有方法）"""
        # 模拟数据库查询
        return User(f"user_{user_id}", f"user{user_id}@example.com")


class User:
    """用户类"""
    
    def __init__(self, username, email):
        self.username = username
        self.email = email
        self._password_hash = None
        self.created_at = None
        self.is_active = True
    
    def set_password(self, password):
        """设置密码"""
        import hashlib
        self._password_hash = hashlib.sha256(password.encode()).hexdigest()
    
    def verify_password(self, password):
        """验证密码"""
        if not self._password_hash:
            return False
        
        import hashlib
        password_hash = hashlib.sha256(password.encode()).hexdigest()
        return password_hash == self._password_hash
    
    def __str__(self):
        """字符串表示"""
        return f"User(username='{self.username}', email='{self.email}')"
    
    def __repr__(self):
        """详细字符串表示"""
        return (f"User(username='{self.username}', email='{self.email}', "
                f"is_active={self.is_active})")


# 函数命名示例
def calculate_user_score(user, activity_data):
    """计算用户活跃度分数"""
    base_score = 100
    
    # 根据活动数据调整分数
    if activity_data.get('login_count', 0) > 10:
        base_score += 20
    
    if activity_data.get('post_count', 0) > 5:
        base_score += 30
    
    return min(base_score, 1000)  # 最高1000分


def format_user_display_name(user):
    """格式化用户显示名称"""
    return f"{user.username} ({user.email})"


# 异常类命名
class UserNotFoundError(Exception):
    """用户未找到异常"""
    pass


class InvalidUserDataError(Exception):
    """无效用户数据异常"""
    pass


class DatabaseConnectionError(Exception):
    """数据库连接异常"""
    pass


# 使用示例
def main():
    """主函数"""
    try:
        # 创建用户服务
        user_service = UserService("sqlite:///users.db")
        
        # 创建用户
        user = user_service.create_user(
            username="alice123",
            email="alice@example.com",
            password="SecurePass123"
        )
        
        print(f"创建用户成功: {user}")
        
        # 获取用户
        found_user = user_service.get_user_by_id(1)
        if found_user:
            print(f"找到用户: {found_user}")
        
        # 计算用户分数
        activity_data = {
            'login_count': 15,
            'post_count': 8
        }
        score = calculate_user_score(user, activity_data)
        print(f"用户分数: {score}")
        
        # 格式化显示名称
        display_name = format_user_display_name(user)
        print(f"显示名称: {display_name}")
        
    except ValueError as e:
        print(f"验证错误: {e}")
    except UserNotFoundError as e:
        print(f"用户错误: {e}")
    except Exception as e:
        print(f"未知错误: {e}")


if __name__ == "__main__":
    main()
```

### 🎯 最佳实践

1. **遵循PEP 8**：使用官方的命名约定
2. **使用有意义的名称**：变量名应该描述其用途
3. **保持一致性**：整个项目使用相同的命名风格
4. **避免缩写**：除非是广泛认知的缩写
5. **使用类型提示**：提高代码可读性
6. **定期检查**：使用工具检查命名规范

通过掌握Python的基础语法、注释、缩进和命名规则，你就为深入学习Python打下了坚实的基础！
