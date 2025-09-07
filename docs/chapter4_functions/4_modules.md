# 模块的导入与使用

## 问题43：如何导入模块？

**答：**
Python有多种导入模块的方式：

### 导入整个模块
```python
import math
result = math.sqrt(16)  # 4.0
```

### 导入特定函数
```python
from math import sqrt, pi
result = sqrt(16)  # 4.0
print(pi)  # 3.141592653589793
```

### 导入所有内容
```python
from math import *
result = sqrt(16)  # 4.0
```

---

## 问题44：from...import的用法？

**答：**
from...import语句用于从模块中导入特定的函数、类或变量：

```python
# 导入特定函数
from datetime import datetime, timedelta

now = datetime.now()
tomorrow = now + timedelta(days=1)

# 导入并重命名
from math import sqrt as square_root
result = square_root(16)

# 导入多个项目
from os import path, listdir, getcwd
```

---

## 问题45：如何创建自定义模块？

**答：**
创建自定义模块很简单，只需要创建.py文件：

### 创建模块文件（my_module.py）
```python
# my_module.py
def greet(name):
    return f"Hello, {name}!"

def add(a, b):
    return a + b

PI = 3.14159
```

### 使用自定义模块
```python
# 导入自定义模块
import my_module

# 使用模块中的函数
result = my_module.greet("Alice")
sum_result = my_module.add(5, 3)
print(my_module.PI)
```
