# json模块

## 问题64：什么是JSON？

**答：**
JSON（JavaScript Object Notation）是一种轻量级的数据交换格式：

```python
import json

# JSON字符串示例
json_string = '''
{
    "name": "Alice",
    "age": 25,
    "city": "Beijing",
    "hobbies": ["reading", "swimming"],
    "is_student": true
}
'''

# JSON的特点：
# 1. 易于阅读和编写
# 2. 轻量级
# 3. 语言无关
# 4. 支持多种数据类型
```

---

## 问题65：如何解析JSON？

**答：**
使用json.loads()解析JSON字符串：

```python
import json

# JSON字符串
json_string = '{"name": "Alice", "age": 25, "city": "Beijing"}'

# 解析JSON
data = json.loads(json_string)
print(f"Name: {data['name']}")
print(f"Age: {data['age']}")
print(f"City: {data['city']}")

# 从文件读取JSON
with open('data.json', 'r') as file:
    data = json.load(file)
    print(data)
```

---

## 问题66：如何生成JSON？

**答：**
使用json.dumps()将Python对象转换为JSON字符串：

```python
import json

# Python字典
data = {
    "name": "Alice",
    "age": 25,
    "city": "Beijing",
    "hobbies": ["reading", "swimming"],
    "is_student": True
}

# 转换为JSON字符串
json_string = json.dumps(data)
print(json_string)

# 格式化输出
formatted_json = json.dumps(data, indent=2, ensure_ascii=False)
print(formatted_json)

# 保存到文件
with open('output.json', 'w', encoding='utf-8') as file:
    json.dump(data, file, indent=2, ensure_ascii=False)
```
