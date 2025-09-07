# os与sys模块

## 问题58：os模块的常用功能？

**答：**
os模块提供了与操作系统交互的功能：

```python
import os

# 获取当前工作目录
current_dir = os.getcwd()
print(f"Current directory: {current_dir}")

# 改变工作目录
os.chdir('/path/to/directory')

# 列出目录内容
files = os.listdir('.')
print(f"Files: {files}")

# 创建目录
os.makedirs('new_directory', exist_ok=True)

# 删除文件
if os.path.exists('file.txt'):
    os.remove('file.txt')

# 检查路径是否存在
exists = os.path.exists('/path/to/file')
```

---

## 问题59：sys模块的作用？

**答：**
sys模块提供了与Python解释器交互的功能：

```python
import sys

# 获取命令行参数
print(f"Script name: {sys.argv[0]}")
print(f"Arguments: {sys.argv[1:]}")

# 获取Python版本
print(f"Python version: {sys.version}")

# 获取模块搜索路径
print(f"Module search paths: {sys.path}")

# 退出程序
# sys.exit(0)  # 正常退出
# sys.exit(1)  # 错误退出

# 获取系统信息
print(f"Platform: {sys.platform}")
```

---

## 问题60：路径操作的方法？

**答：**
os.path模块提供了路径操作的功能：

```python
import os.path

# 路径拼接
full_path = os.path.join('folder', 'subfolder', 'file.txt')

# 获取文件名
filename = os.path.basename('/path/to/file.txt')  # file.txt

# 获取目录名
dirname = os.path.dirname('/path/to/file.txt')    # /path/to

# 分离文件名和扩展名
name, ext = os.path.splitext('file.txt')  # ('file', '.txt')

# 检查路径类型
is_file = os.path.isfile('/path/to/file.txt')
is_dir = os.path.isdir('/path/to/directory')
is_abs = os.path.isabs('/absolute/path')

# 获取文件大小
size = os.path.getsize('/path/to/file.txt')
```
