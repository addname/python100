# 集合(Set)的特点与使用

## 问题1：什么是集合？集合有什么特点？

集合(set)是Python中的一种无序、不重复的数据结构，用花括号 `{}` 表示：

```python
# 创建集合
fruits = {"苹果", "香蕉", "橙子", "苹果"}  # 重复元素会被自动去除
print(fruits)  # {'橙子', '苹果', '香蕉'}
print(type(fruits))  # <class 'set'>

# 空集合
empty_set = set()  # 注意：{} 是空字典，不是空集合
print(type(empty_set))  # <class 'set'>
```

### 集合的特点：
1. **唯一性**：集合中的元素必须唯一
2. **无序性**：元素没有固定顺序
3. **可变性**：可以添加、删除元素
4. **可哈希性**：元素必须是不可变类型
5. **高效性**：查找、添加、删除操作都是O(1)时间复杂度

## 问题2：如何创建和操作集合？

```python
# 1. 直接创建
colors = {"red", "green", "blue"}
numbers = {1, 2, 3, 4, 5}

# 2. 使用set()函数
text_set = set("hello")  # 从字符串创建
print(text_set)  # {'h', 'e', 'l', 'o'} (注意'l'只出现一次)

list_set = set([1, 2, 2, 3, 3, 4])  # 从列表创建
print(list_set)  # {1, 2, 3, 4}

# 3. 集合推导式
squares = {x**2 for x in range(1, 6)}
print(squares)  # {1, 4, 9, 16, 25}

# 4. 添加元素
fruits.add("葡萄")
fruits.update(["西瓜", "草莓"])  # 添加多个元素
print(fruits)

# 5. 删除元素
fruits.remove("苹果")  # 如果元素不存在会报错
fruits.discard("香蕉")  # 如果元素不存在不会报错
removed = fruits.pop()  # 随机删除一个元素并返回
print(f"删除的元素: {removed}")

# 6. 清空集合
fruits.clear()
print(fruits)  # set()
```

## 问题3：集合的数学运算有哪些？

```python
# 创建两个集合
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

# 1. 并集 (union)
union = set1 | set2  # 或 set1.union(set2)
print(f"并集: {union}")  # {1, 2, 3, 4, 5, 6, 7, 8}

# 2. 交集 (intersection)
intersection = set1 & set2  # 或 set1.intersection(set2)
print(f"交集: {intersection}")  # {4, 5}

# 3. 差集 (difference)
diff1 = set1 - set2  # 或 set1.difference(set2)
diff2 = set2 - set1  # 或 set2.difference(set1)
print(f"set1 - set2: {diff1}")  # {1, 2, 3}
print(f"set2 - set1: {diff2}")  # {6, 7, 8}

# 4. 对称差集 (symmetric_difference)
symmetric_diff = set1 ^ set2  # 或 set1.symmetric_difference(set2)
print(f"对称差集: {symmetric_diff}")  # {1, 2, 3, 6, 7, 8}

# 5. 子集和超集
set_a = {1, 2, 3}
set_b = {1, 2, 3, 4, 5}

print(set_a.issubset(set_b))    # True (set_a是set_b的子集)
print(set_b.issuperset(set_a))  # True (set_b是set_a的超集)
print(set_a < set_b)           # True (真子集)
print(set_b > set_a)           # True (真超集)
```

## 问题4：集合的常用方法有哪些？

```python
# 创建示例集合
numbers = {1, 2, 3, 4, 5}

# 1. 检查元素是否存在
print(3 in numbers)      # True
print(6 not in numbers)  # True

# 2. 获取集合长度
print(len(numbers))  # 5

# 3. 复制集合
numbers_copy = numbers.copy()
print(numbers_copy)

# 4. 检查集合关系
set1 = {1, 2, 3}
set2 = {1, 2, 3, 4, 5}
set3 = {6, 7, 8}

print(set1.isdisjoint(set3))  # True (没有共同元素)
print(set1.issubset(set2))    # True (是子集)
print(set2.issuperset(set1))  # True (是超集)

# 5. 更新集合
set1.update([4, 5, 6])  # 添加多个元素
print(set1)  # {1, 2, 3, 4, 5, 6}

# 6. 交集更新
set1.intersection_update({3, 4, 5, 6, 7})
print(set1)  # {3, 4, 5, 6}

# 7. 差集更新
set1.difference_update({5, 6})
print(set1)  # {3, 4}

# 8. 对称差集更新
set1.symmetric_difference_update({4, 5, 6})
print(set1)  # {3, 5, 6}
```

## 问题5：集合在实际应用中有哪些用途？

```python
# 1. 去重
def remove_duplicates(lst):
    return list(set(lst))

numbers = [1, 2, 2, 3, 3, 4, 5, 5]
unique_numbers = remove_duplicates(numbers)
print(unique_numbers)  # [1, 2, 3, 4, 5]

# 2. 查找共同元素
def find_common_elements(list1, list2):
    return list(set(list1) & set(list2))

list1 = [1, 2, 3, 4, 5]
list2 = [4, 5, 6, 7, 8]
common = find_common_elements(list1, list2)
print(common)  # [4, 5]

# 3. 查找不同元素
def find_different_elements(list1, list2):
    return list(set(list1) ^ set(list2))

different = find_different_elements(list1, list2)
print(different)  # [1, 2, 3, 6, 7, 8]

# 4. 权限管理
def check_permissions(user_permissions, required_permissions):
    return set(required_permissions).issubset(set(user_permissions))

user_perms = ["read", "write", "execute"]
required_perms = ["read", "write"]
print(check_permissions(user_perms, required_perms))  # True

# 5. 标签系统
def get_common_tags(articles):
    if not articles:
        return set()
    
    common_tags = set(articles[0]["tags"])
    for article in articles[1:]:
        common_tags &= set(article["tags"])
    
    return common_tags

articles = [
    {"title": "文章1", "tags": ["Python", "编程", "教程"]},
    {"title": "文章2", "tags": ["Python", "数据科学", "教程"]},
    {"title": "文章3", "tags": ["Python", "Web开发", "教程"]}
]

common_tags = get_common_tags(articles)
print(common_tags)  # {'Python', '教程'}
```

## 问题6：集合推导式如何使用？

```python
# 基本集合推导式
squares = {x**2 for x in range(1, 6)}
print(squares)  # {1, 4, 9, 16, 25}

# 带条件的集合推导式
even_squares = {x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)  # {64, 4, 36, 16, 100}

# 字符串处理
words = ["hello", "world", "python", "programming"]
unique_chars = {char for word in words for char in word}
print(unique_chars)  # {'h', 'e', 'l', 'o', 'w', 'r', 'd', 'p', 'y', 't', 'n', 'g', 'a', 'm', 'i'}

# 从字典创建集合
person = {"name": "张三", "age": 25, "city": "北京"}
keys_set = {key for key in person.keys()}
values_set = {value for value in person.values()}
print(keys_set)    # {'name', 'age', 'city'}
print(values_set)  # {'张三', 25, '北京'}
```

## 问题7：集合与列表、元组的区别是什么？

```python
# 创建相同内容的列表、元组和集合
my_list = [1, 2, 2, 3, 3, 4]
my_tuple = (1, 2, 2, 3, 3, 4)
my_set = {1, 2, 2, 3, 3, 4}

print("列表:", my_list)    # [1, 2, 2, 3, 3, 4]
print("元组:", my_tuple)   # (1, 2, 2, 3, 3, 4)
print("集合:", my_set)     # {1, 2, 3, 4}

# 性能比较
import time

# 测试查找性能
large_list = list(range(100000))
large_set = set(range(100000))

# 列表查找
start_time = time.time()
for i in range(1000):
    _ = 50000 in large_list
list_time = time.time() - start_time

# 集合查找
start_time = time.time()
for i in range(1000):
    _ = 50000 in large_set
set_time = time.time() - start_time

print(f"列表查找耗时: {list_time:.6f}秒")
print(f"集合查找耗时: {set_time:.6f}秒")
print(f"集合比列表快 {list_time/set_time:.1f} 倍")
```

## 问题8：集合的不可变版本是什么？

```python
# frozenset - 不可变集合
frozen = frozenset([1, 2, 3, 4, 5])
print(frozen)  # frozenset({1, 2, 3, 4, 5})
print(type(frozen))  # <class 'frozenset'>

# frozenset可以作为字典的键
frozen_dict = {
    frozenset([1, 2, 3]): "集合1",
    frozenset([4, 5, 6]): "集合2"
}
print(frozen_dict)

# frozenset支持集合运算
frozen1 = frozenset([1, 2, 3, 4])
frozen2 = frozenset([3, 4, 5, 6])
print(frozen1 | frozen2)  # frozenset({1, 2, 3, 4, 5, 6})
print(frozen1 & frozen2)  # frozenset({3, 4})
```

## 问题9：集合在数据处理中的应用

```python
# 1. 数据清洗
def clean_data(data):
    # 去除重复数据
    unique_data = list(set(data))
    return unique_data

# 2. 数据对比
def compare_datasets(old_data, new_data):
    old_set = set(old_data)
    new_set = set(new_data)
    
    added = new_set - old_set      # 新增数据
    removed = old_set - new_set    # 删除数据
    unchanged = old_set & new_set  # 未变化数据
    
    return {
        "added": list(added),
        "removed": list(removed),
        "unchanged": list(unchanged)
    }

# 3. 用户行为分析
def analyze_user_behavior(user_actions):
    action_sets = {}
    for user, actions in user_actions.items():
        action_sets[user] = set(actions)
    
    # 找出所有用户都执行过的动作
    common_actions = set.intersection(*action_sets.values())
    
    # 找出只有部分用户执行的动作
    all_actions = set.union(*action_sets.values())
    unique_actions = all_actions - common_actions
    
    return {
        "common_actions": list(common_actions),
        "unique_actions": list(unique_actions)
    }

# 使用示例
user_actions = {
    "user1": ["login", "view", "purchase", "logout"],
    "user2": ["login", "view", "search", "logout"],
    "user3": ["login", "view", "purchase", "review"]
}

analysis = analyze_user_behavior(user_actions)
print("共同行为:", analysis["common_actions"])  # ['login', 'view', 'logout']
print("独特行为:", analysis["unique_actions"])  # ['purchase', 'search', 'review']
```

## 问题10：集合的最佳实践

```python
# 1. 使用集合进行快速成员检查
def is_valid_email(email):
    valid_domains = {"gmail.com", "yahoo.com", "hotmail.com", "outlook.com"}
    domain = email.split("@")[-1]
    return domain in valid_domains

# 2. 使用集合进行数据验证
def validate_tags(tags, allowed_tags):
    return set(tags).issubset(set(allowed_tags))

# 3. 使用集合进行权限检查
def has_permission(user_permissions, required_permission):
    return required_permission in set(user_permissions)

# 4. 使用集合进行数据去重和统计
def analyze_text(text):
    words = text.lower().split()
    unique_words = set(words)
    word_count = len(words)
    unique_count = len(unique_words)
    
    return {
        "total_words": word_count,
        "unique_words": unique_count,
        "duplicate_rate": (word_count - unique_count) / word_count
    }

# 5. 使用集合进行数据合并
def merge_user_data(users):
    all_skills = set()
    all_interests = set()
    
    for user in users:
        all_skills.update(user.get("skills", []))
        all_interests.update(user.get("interests", []))
    
    return {
        "all_skills": list(all_skills),
        "all_interests": list(all_interests)
    }

# 6. 使用集合进行数据过滤
def filter_common_items(list1, list2, threshold=0.5):
    set1 = set(list1)
    set2 = set(list2)
    
    common = set1 & set2
    total = set1 | set2
    
    if len(total) == 0:
        return []
    
    similarity = len(common) / len(total)
    if similarity >= threshold:
        return list(common)
    else:
        return []
```

## 总结

集合是Python中重要的数据结构，主要特点：
- **唯一性**：自动去除重复元素
- **无序性**：元素没有固定顺序
- **高效性**：O(1)的查找、添加、删除操作
- **数学运算**：支持并集、交集、差集等运算

适用场景：
- 数据去重
- 快速成员检查
- 集合运算
- 权限管理
- 数据对比和分析
- 标签系统
