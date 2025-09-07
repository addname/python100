# 文件读写操作

## 问题124：如何打开和关闭文件？

```python
# 1. 基本文件操作
file = open("example.txt", "r", encoding="utf-8")
content = file.read()
file.close()

# 2. 使用with语句（推荐）
with open("example.txt", "r", encoding="utf-8") as file:
    content = file.read()
# 文件会自动关闭

# 3. 文件模式
# "r" - 读取模式（默认）
# "w" - 写入模式（覆盖）
# "a" - 追加模式
# "x" - 创建模式（文件不存在时创建）
# "b" - 二进制模式
# "t" - 文本模式（默认）
```

## 问题125：如何读取文件内容？

```python
# 1. 读取整个文件
with open("example.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)

# 2. 按行读取
with open("example.txt", "r", encoding="utf-8") as file:
    lines = file.readlines()
    for line in lines:
        print(line.strip())

# 3. 逐行读取
with open("example.txt", "r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())

# 4. 读取指定字符数
with open("example.txt", "r", encoding="utf-8") as file:
    chunk = file.read(100)  # 读取100个字符
    print(chunk)
```

## 问题126：如何写入文件内容？

```python
# 1. 写入文本
with open("output.txt", "w", encoding="utf-8") as file:
    file.write("Hello, World!")
    file.write("\n这是第二行")

# 2. 写入多行
lines = ["第一行", "第二行", "第三行"]
with open("output.txt", "w", encoding="utf-8") as file:
    file.writelines(line + "\n" for line in lines)

# 3. 追加内容
with open("output.txt", "a", encoding="utf-8") as file:
    file.write("\n这是追加的内容")

# 4. 使用print函数写入
with open("output.txt", "w", encoding="utf-8") as file:
    print("Hello, World!", file=file)
    print("这是第二行", file=file)
```

## 问题127：如何处理文件异常？

```python
import os

# 1. 检查文件是否存在
def read_file_safely(filename):
    if not os.path.exists(filename):
        print(f"文件 {filename} 不存在")
        return None
    
    try:
        with open(filename, "r", encoding="utf-8") as file:
            return file.read()
    except FileNotFoundError:
        print(f"文件 {filename} 未找到")
        return None
    except PermissionError:
        print(f"没有权限访问文件 {filename}")
        return None
    except UnicodeDecodeError:
        print(f"文件 {filename} 编码错误")
        return None
    except Exception as e:
        print(f"读取文件时出错: {e}")
        return None

# 2. 使用try-except处理文件操作
def copy_file(source, destination):
    try:
        with open(source, "r", encoding="utf-8") as src:
            content = src.read()
        
        with open(destination, "w", encoding="utf-8") as dst:
            dst.write(content)
        
        print(f"文件复制成功: {source} -> {destination}")
    except FileNotFoundError:
        print(f"源文件 {source} 不存在")
    except PermissionError:
        print(f"没有权限访问文件")
    except Exception as e:
        print(f"复制文件时出错: {e}")
```

## 问题128：如何处理二进制文件？

```python
# 1. 读取二进制文件
def read_binary_file(filename):
    try:
        with open(filename, "rb") as file:
            data = file.read()
            return data
    except FileNotFoundError:
        print(f"文件 {filename} 不存在")
        return None

# 2. 写入二进制文件
def write_binary_file(filename, data):
    try:
        with open(filename, "wb") as file:
            file.write(data)
        print(f"二进制文件写入成功: {filename}")
    except Exception as e:
        print(f"写入二进制文件时出错: {e}")

# 3. 复制二进制文件
def copy_binary_file(source, destination):
    try:
        with open(source, "rb") as src:
            with open(destination, "wb") as dst:
                while True:
                    chunk = src.read(1024)  # 每次读取1KB
                    if not chunk:
                        break
                    dst.write(chunk)
        print(f"二进制文件复制成功: {source} -> {destination}")
    except Exception as e:
        print(f"复制二进制文件时出错: {e}")
```

## 问题129：如何使用pathlib模块处理文件路径？

```python
from pathlib import Path

# 1. 创建Path对象
file_path = Path("example.txt")
directory_path = Path("documents")

# 2. 检查路径
print(file_path.exists())      # 检查文件是否存在
print(file_path.is_file())     # 检查是否为文件
print(directory_path.is_dir()) # 检查是否为目录

# 3. 获取路径信息
print(file_path.name)          # 文件名
print(file_path.stem)          # 文件名（不含扩展名）
print(file_path.suffix)        # 文件扩展名
print(file_path.parent)        # 父目录
print(file_path.absolute())    # 绝对路径

# 4. 使用pathlib读写文件
def read_file_with_pathlib(filename):
    file_path = Path(filename)
    if file_path.exists():
        return file_path.read_text(encoding="utf-8")
    return None

def write_file_with_pathlib(filename, content):
    file_path = Path(filename)
    file_path.write_text(content, encoding="utf-8")
    print(f"文件写入成功: {filename}")

# 5. 创建目录
def create_directory(dirname):
    dir_path = Path(dirname)
    dir_path.mkdir(exist_ok=True)
    print(f"目录创建成功: {dirname}")
```

## 问题130：如何处理CSV文件？

```python
import csv

# 1. 读取CSV文件
def read_csv_file(filename):
    data = []
    try:
        with open(filename, "r", encoding="utf-8") as file:
            reader = csv.reader(file)
            for row in reader:
                data.append(row)
        return data
    except FileNotFoundError:
        print(f"文件 {filename} 不存在")
        return []

# 2. 写入CSV文件
def write_csv_file(filename, data):
    try:
        with open(filename, "w", encoding="utf-8", newline="") as file:
            writer = csv.writer(file)
            writer.writerows(data)
        print(f"CSV文件写入成功: {filename}")
    except Exception as e:
        print(f"写入CSV文件时出错: {e}")

# 3. 使用字典读写CSV
def read_csv_as_dict(filename):
    data = []
    try:
        with open(filename, "r", encoding="utf-8") as file:
            reader = csv.DictReader(file)
            for row in reader:
                data.append(row)
        return data
    except FileNotFoundError:
        print(f"文件 {filename} 不存在")
        return []

def write_csv_from_dict(filename, data, fieldnames):
    try:
        with open(filename, "w", encoding="utf-8", newline="") as file:
            writer = csv.DictWriter(file, fieldnames=fieldnames)
            writer.writeheader()
            writer.writerows(data)
        print(f"CSV文件写入成功: {filename}")
    except Exception as e:
        print(f"写入CSV文件时出错: {e}")

# 使用示例
csv_data = [
    ["姓名", "年龄", "城市"],
    ["张三", "25", "北京"],
    ["李四", "30", "上海"]
]
write_csv_file("people.csv", csv_data)
```

## 问题131：如何处理JSON文件？

```python
import json

# 1. 读取JSON文件
def read_json_file(filename):
    try:
        with open(filename, "r", encoding="utf-8") as file:
            data = json.load(file)
        return data
    except FileNotFoundError:
        print(f"文件 {filename} 不存在")
        return None
    except json.JSONDecodeError:
        print(f"JSON格式错误")
        return None

# 2. 写入JSON文件
def write_json_file(filename, data):
    try:
        with open(filename, "w", encoding="utf-8") as file:
            json.dump(data, file, ensure_ascii=False, indent=2)
        print(f"JSON文件写入成功: {filename}")
    except Exception as e:
        print(f"写入JSON文件时出错: {e}")

# 3. 处理复杂JSON数据
def process_json_data():
    # 示例数据
    data = {
        "users": [
            {"name": "张三", "age": 25, "city": "北京"},
            {"name": "李四", "age": 30, "city": "上海"}
        ],
        "settings": {
            "theme": "dark",
            "language": "zh-CN"
        }
    }
    
    # 写入JSON文件
    write_json_file("data.json", data)
    
    # 读取JSON文件
    loaded_data = read_json_file("data.json")
    if loaded_data:
        print("JSON数据加载成功")
        print(f"用户数量: {len(loaded_data['users'])}")
```

## 问题132：文件操作的最佳实践

```python
import os
import shutil
from pathlib import Path

# 1. 安全的文件操作
def safe_file_operation(filename, operation):
    try:
        # 检查文件是否存在
        if not os.path.exists(filename):
            print(f"文件 {filename} 不存在")
            return False
        
        # 检查文件权限
        if not os.access(filename, os.R_OK):
            print(f"没有读取权限: {filename}")
            return False
        
        # 执行操作
        return operation(filename)
    except Exception as e:
        print(f"操作失败: {e}")
        return False

# 2. 文件备份
def backup_file(filename):
    if not os.path.exists(filename):
        print(f"文件 {filename} 不存在")
        return False
    
    backup_name = f"{filename}.backup"
    try:
        shutil.copy2(filename, backup_name)
        print(f"文件备份成功: {backup_name}")
        return True
    except Exception as e:
        print(f"备份失败: {e}")
        return False

# 3. 文件清理
def clean_old_files(directory, days=30):
    import time
    current_time = time.time()
    cutoff_time = current_time - (days * 24 * 60 * 60)
    
    try:
        for filename in os.listdir(directory):
            file_path = os.path.join(directory, filename)
            if os.path.isfile(file_path):
                file_time = os.path.getmtime(file_path)
                if file_time < cutoff_time:
                    os.remove(file_path)
                    print(f"删除旧文件: {filename}")
    except Exception as e:
        print(f"清理文件时出错: {e}")

# 4. 文件监控
def monitor_file_changes(filename):
    import time
    last_modified = 0
    
    while True:
        try:
            if os.path.exists(filename):
                current_modified = os.path.getmtime(filename)
                if current_modified > last_modified:
                    print(f"文件 {filename} 已修改")
                    last_modified = current_modified
            time.sleep(1)
        except KeyboardInterrupt:
            print("监控停止")
            break
```

## 问题133：文件操作的实际应用

```python
# 1. 日志文件处理
class Logger:
    def __init__(self, filename):
        self.filename = filename
    
    def log(self, message, level="INFO"):
        import datetime
        timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        log_entry = f"[{timestamp}] {level}: {message}\n"
        
        with open(self.filename, "a", encoding="utf-8") as file:
            file.write(log_entry)
    
    def read_logs(self, lines=10):
        try:
            with open(self.filename, "r", encoding="utf-8") as file:
                all_lines = file.readlines()
                return all_lines[-lines:]
        except FileNotFoundError:
            return []

# 2. 配置文件管理
class ConfigManager:
    def __init__(self, config_file):
        self.config_file = config_file
        self.config = {}
        self.load_config()
    
    def load_config(self):
        try:
            with open(self.config_file, "r", encoding="utf-8") as file:
                self.config = json.load(file)
        except FileNotFoundError:
            self.config = {}
        except json.JSONDecodeError:
            print("配置文件格式错误")
            self.config = {}
    
    def save_config(self):
        try:
            with open(self.config_file, "w", encoding="utf-8") as file:
                json.dump(self.config, file, ensure_ascii=False, indent=2)
        except Exception as e:
            print(f"保存配置失败: {e}")
    
    def get(self, key, default=None):
        return self.config.get(key, default)
    
    def set(self, key, value):
        self.config[key] = value
        self.save_config()

# 3. 文件同步
def sync_files(source_dir, target_dir):
    source_path = Path(source_dir)
    target_path = Path(target_dir)
    
    if not source_path.exists():
        print(f"源目录不存在: {source_dir}")
        return
    
    target_path.mkdir(exist_ok=True)
    
    for file_path in source_path.rglob("*"):
        if file_path.is_file():
            relative_path = file_path.relative_to(source_path)
            target_file = target_path / relative_path
            target_file.parent.mkdir(parents=True, exist_ok=True)
            shutil.copy2(file_path, target_file)
            print(f"同步文件: {relative_path}")
```

## 总结

文件操作是Python编程中的重要技能，要点包括：
- **文件打开和关闭**：使用with语句确保文件正确关闭
- **文件模式**：r、w、a、x等不同模式的使用
- **异常处理**：处理文件不存在、权限错误等异常
- **二进制文件**：处理图片、视频等二进制数据
- **pathlib模块**：现代化的路径处理方式
- **CSV和JSON**：处理结构化数据文件
- **最佳实践**：安全操作、备份、监控等
- **实际应用**：日志、配置、同步等场景
