# 第五章：标准库应用

!!! info "Python标准库"
    Python标准库是Python安装包的一部分，包含了大量实用的模块和函数。本章将学习如何使用这些标准库来提高开发效率。

## 问题66：如何使用os模块进行系统操作？

### 🤔 问题描述
os模块是Python中用于与操作系统交互的重要模块，它提供了哪些功能？如何使用os模块进行文件和目录操作？

### 💡 详细解答

#### os模块的主要功能

os模块提供了与操作系统交互的接口，包括：
- 文件和目录操作
- 环境变量访问
- 进程管理
- 路径操作

#### 基本用法

```python
import os

# 1. 获取当前工作目录
current_dir = os.getcwd()
print(f"当前目录: {current_dir}")

# 2. 改变工作目录
os.chdir('/path/to/directory')

# 3. 列出目录内容
files = os.listdir('.')
print(f"当前目录文件: {files}")

# 4. 创建目录
os.mkdir('new_directory')
os.makedirs('path/to/nested/directory')  # 创建多级目录

# 5. 删除目录
os.rmdir('empty_directory')
os.removedirs('path/to/nested/directory')  # 删除多级目录

# 6. 重命名文件或目录
os.rename('old_name.txt', 'new_name.txt')

# 7. 删除文件
os.remove('file_to_delete.txt')

# 8. 检查路径是否存在
if os.path.exists('some_file.txt'):
    print("文件存在")

# 9. 检查是否为文件或目录
if os.path.isfile('some_file.txt'):
    print("这是一个文件")
if os.path.isdir('some_directory'):
    print("这是一个目录")
```

### 📝 代码示例

```python
# os模块综合示例
import os
import shutil
from datetime import datetime

def demonstrate_os_operations():
    """演示os模块的各种操作"""
    
    print("=== os模块操作演示 ===")
    
    # 1. 目录操作
    print(f"当前工作目录: {os.getcwd()}")
    
    # 创建测试目录
    test_dir = "test_directory"
    if not os.path.exists(test_dir):
        os.mkdir(test_dir)
        print(f"创建目录: {test_dir}")
    
    # 2. 文件操作
    test_file = os.path.join(test_dir, "test.txt")
    with open(test_file, 'w') as f:
        f.write("这是一个测试文件")
    print(f"创建文件: {test_file}")
    
    # 3. 路径操作
    print(f"文件绝对路径: {os.path.abspath(test_file)}")
    print(f"文件目录: {os.path.dirname(test_file)}")
    print(f"文件名: {os.path.basename(test_file)}")
    print(f"文件扩展名: {os.path.splitext(test_file)}")
    
    # 4. 文件信息
    stat_info = os.stat(test_file)
    print(f"文件大小: {stat_info.st_size} 字节")
    print(f"修改时间: {datetime.fromtimestamp(stat_info.st_mtime)}")
    
    # 5. 环境变量
    print(f"PATH环境变量: {os.environ.get('PATH', '未设置')}")
    print(f"HOME目录: {os.environ.get('HOME', os.environ.get('USERPROFILE', '未设置'))}")
    
    # 6. 清理
    os.remove(test_file)
    os.rmdir(test_dir)
    print("清理完成")

def file_operations_demo():
    """文件操作演示"""
    
    print("\n=== 文件操作演示 ===")
    
    # 创建测试文件
    test_files = ['file1.txt', 'file2.txt', 'file3.txt']
    for filename in test_files:
        with open(filename, 'w') as f:
            f.write(f"这是{filename}的内容")
        print(f"创建文件: {filename}")
    
    # 列出当前目录文件
    files = os.listdir('.')
    txt_files = [f for f in files if f.endswith('.txt')]
    print(f"文本文件: {txt_files}")
    
    # 批量重命名
    for i, filename in enumerate(txt_files, 1):
        new_name = f"renamed_file_{i}.txt"
        os.rename(filename, new_name)
        print(f"重命名: {filename} -> {new_name}")
    
    # 清理文件
    for filename in os.listdir('.'):
        if filename.startswith('renamed_file_') and filename.endswith('.txt'):
            os.remove(filename)
            print(f"删除文件: {filename}")

def directory_traversal():
    """目录遍历演示"""
    
    print("\n=== 目录遍历演示 ===")
    
    def walk_directory(path, max_depth=2, current_depth=0):
        """递归遍历目录"""
        if current_depth > max_depth:
            return
        
        try:
            for item in os.listdir(path):
                item_path = os.path.join(path, item)
                indent = "  " * current_depth
                
                if os.path.isfile(item_path):
                    size = os.path.getsize(item_path)
                    print(f"{indent}📄 {item} ({size} bytes)")
                elif os.path.isdir(item_path):
                    print(f"{indent}📁 {item}/")
                    walk_directory(item_path, max_depth, current_depth + 1)
        except PermissionError:
            print(f"{indent}❌ 权限不足: {path}")
    
    # 遍历当前目录
    walk_directory('.')

def main():
    """主函数"""
    demonstrate_os_operations()
    file_operations_demo()
    directory_traversal()

if __name__ == "__main__":
    main()
```

---

## 问题67：如何使用pathlib模块进行路径操作？

### 🤔 问题描述
pathlib是Python 3.4+引入的现代路径操作模块，它比os.path有什么优势？如何使用pathlib进行路径操作？

### 💡 详细解答

#### pathlib的优势

pathlib提供了面向对象的路径操作接口，具有以下优势：
- 更直观的API
- 跨平台兼容性
- 链式操作
- 类型安全

#### 基本用法

```python
from pathlib import Path

# 1. 创建Path对象
p = Path('/path/to/file.txt')
p = Path('relative/path')
p = Path.cwd()  # 当前目录

# 2. 路径操作
p = Path('/home/user') / 'documents' / 'file.txt'
print(p)  # /home/user/documents/file.txt

# 3. 路径属性
print(p.name)        # file.txt
print(p.stem)        # file
print(p.suffix)      # .txt
print(p.parent)      # /home/user/documents
print(p.parts)       # ('/', 'home', 'user', 'documents', 'file.txt')

# 4. 路径检查
print(p.exists())    # 检查是否存在
print(p.is_file())   # 检查是否为文件
print(p.is_dir())    # 检查是否为目录

# 5. 文件操作
p.write_text('Hello, World!')  # 写入文本
content = p.read_text()        # 读取文本
p.unlink()                     # 删除文件

# 6. 目录操作
p.mkdir()           # 创建目录
p.mkdir(parents=True, exist_ok=True)  # 创建多级目录
```

### 📝 代码示例

```python
# pathlib综合示例
from pathlib import Path
import json

def demonstrate_pathlib():
    """演示pathlib的各种操作"""
    
    print("=== pathlib操作演示 ===")
    
    # 1. 创建Path对象
    current_dir = Path.cwd()
    print(f"当前目录: {current_dir}")
    
    # 2. 路径拼接
    config_file = current_dir / 'config' / 'settings.json'
    print(f"配置文件路径: {config_file}")
    
    # 3. 创建目录结构
    config_file.parent.mkdir(parents=True, exist_ok=True)
    print(f"创建目录: {config_file.parent}")
    
    # 4. 写入配置文件
    config_data = {
        'database': {
            'host': 'localhost',
            'port': 5432,
            'name': 'myapp'
        },
        'debug': True,
        'version': '1.0.0'
    }
    
    config_file.write_text(json.dumps(config_data, indent=2))
    print(f"写入配置文件: {config_file}")
    
    # 5. 读取配置文件
    loaded_config = json.loads(config_file.read_text())
    print(f"读取配置: {loaded_config}")
    
    # 6. 文件信息
    print(f"文件大小: {config_file.stat().st_size} 字节")
    print(f"文件修改时间: {config_file.stat().st_mtime}")
    
    # 7. 路径操作
    print(f"文件名: {config_file.name}")
    print(f"文件扩展名: {config_file.suffix}")
    print(f"文件主名: {config_file.stem}")
    print(f"父目录: {config_file.parent}")
    print(f"绝对路径: {config_file.absolute()}")
    
    # 8. 清理
    config_file.unlink()
    config_file.parent.rmdir()
    print("清理完成")

def file_management_system():
    """文件管理系统示例"""
    
    print("\n=== 文件管理系统 ===")
    
    # 创建项目目录结构
    project_root = Path('my_project')
    project_root.mkdir(exist_ok=True)
    
    # 创建子目录
    directories = [
        'src',
        'tests',
        'docs',
        'data',
        'logs'
    ]
    
    for directory in directories:
        (project_root / directory).mkdir(exist_ok=True)
        print(f"创建目录: {project_root / directory}")
    
    # 创建文件
    files_to_create = {
        'src/main.py': 'print("Hello, World!")',
        'src/utils.py': 'def helper(): pass',
        'tests/test_main.py': 'import unittest\nclass TestMain(unittest.TestCase): pass',
        'docs/README.md': '# My Project\n\n这是一个示例项目。',
        'data/sample.json': '{"name": "sample", "value": 42}'
    }
    
    for file_path, content in files_to_create.items():
        file_obj = project_root / file_path
        file_obj.write_text(content)
        print(f"创建文件: {file_obj}")
    
    # 遍历项目结构
    print("\n项目结构:")
    for item in project_root.rglob('*'):
        if item.is_file():
            size = item.stat().st_size
            print(f"  📄 {item.relative_to(project_root)} ({size} bytes)")
        elif item.is_dir():
            print(f"  📁 {item.relative_to(project_root)}/")
    
    # 查找特定文件
    print("\n查找Python文件:")
    for py_file in project_root.rglob('*.py'):
        print(f"  🐍 {py_file.relative_to(project_root)}")
    
    # 清理项目
    import shutil
    shutil.rmtree(project_root)
    print(f"\n清理项目目录: {project_root}")

def backup_system():
    """备份系统示例"""
    
    print("\n=== 备份系统 ===")
    
    # 创建源目录和文件
    source_dir = Path('source')
    source_dir.mkdir(exist_ok=True)
    
    # 创建一些测试文件
    for i in range(3):
        file_path = source_dir / f'file_{i}.txt'
        file_path.write_text(f'这是文件 {i} 的内容')
    
    # 创建备份目录
    backup_dir = Path('backup')
    backup_dir.mkdir(exist_ok=True)
    
    # 备份文件
    for source_file in source_dir.iterdir():
        if source_file.is_file():
            backup_file = backup_dir / f"{source_file.stem}_backup{source_file.suffix}"
            backup_file.write_text(source_file.read_text())
            print(f"备份: {source_file.name} -> {backup_file.name}")
    
    # 验证备份
    print("\n备份验证:")
    for backup_file in backup_dir.iterdir():
        if backup_file.is_file():
            print(f"  ✅ {backup_file.name}")
    
    # 清理
    import shutil
    shutil.rmtree(source_dir)
    shutil.rmtree(backup_dir)
    print("清理完成")

def main():
    """主函数"""
    demonstrate_pathlib()
    file_management_system()
    backup_system()

if __name__ == "__main__":
    main()
```

### 🎯 最佳实践

1. **优先使用pathlib**：比os.path更现代和直观
2. **使用链式操作**：提高代码可读性
3. **注意跨平台兼容性**：pathlib自动处理路径分隔符
4. **合理使用glob模式**：快速查找文件
5. **异常处理**：文件操作可能失败

通过掌握标准库的使用，你就能编写出更高效、更可靠的Python程序！
