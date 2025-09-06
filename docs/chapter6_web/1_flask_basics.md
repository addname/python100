# 第六章：Web开发

!!! info "Web开发基础"
    Web开发是Python的重要应用领域。本章将学习如何使用Flask和Django等框架开发Web应用，以及API开发和部署的相关知识。

## 问题81：什么是Flask？如何创建第一个Flask应用？

### 🤔 问题描述
Flask是什么？它有什么特点？如何安装和配置Flask？如何创建第一个Flask应用？

### 💡 详细解答

#### Flask简介

Flask是一个轻量级的Python Web框架，被称为"微框架"，具有以下特点：
- 简单易学
- 灵活可扩展
- 文档完善
- 社区活跃

#### 安装Flask

```bash
# 安装Flask
pip install Flask

# 创建虚拟环境（推荐）
python -m venv flask_env
source flask_env/bin/activate  # Linux/macOS
# flask_env\Scripts\activate   # Windows
pip install Flask
```

#### 第一个Flask应用

```python
from flask import Flask

# 创建Flask应用实例
app = Flask(__name__)

# 定义路由
@app.route('/')
def home():
    return '<h1>欢迎来到Flask世界！</h1>'

@app.route('/about')
def about():
    return '<h1>关于我们</h1><p>这是一个Flask应用</p>'

@app.route('/user/<name>')
def user(name):
    return f'<h1>你好, {name}!</h1>'

# 运行应用
if __name__ == '__main__':
    app.run(debug=True)
```

### 📝 代码示例

```python
# Flask应用综合示例
from flask import Flask, render_template, request, redirect, url_for, flash, jsonify
from datetime import datetime
import os

app = Flask(__name__)
app.secret_key = 'your-secret-key-here'

# 模拟数据存储
posts = [
    {
        'id': 1,
        'title': 'Flask入门教程',
        'content': 'Flask是一个轻量级的Python Web框架...',
        'author': '张三',
        'date': datetime(2024, 1, 1)
    },
    {
        'id': 2,
        'title': 'Python Web开发',
        'content': 'Python在Web开发领域有着广泛的应用...',
        'author': '李四',
        'date': datetime(2024, 1, 2)
    }
]

@app.route('/')
def index():
    """首页"""
    return render_template('index.html', posts=posts)

@app.route('/post/<int:post_id>')
def post(post_id):
    """文章详情页"""
    post = next((p for p in posts if p['id'] == post_id), None)
    if post is None:
        flash('文章不存在', 'error')
        return redirect(url_for('index'))
    return render_template('post.html', post=post)

@app.route('/create', methods=['GET', 'POST'])
def create_post():
    """创建文章"""
    if request.method == 'POST':
        title = request.form['title']
        content = request.form['content']
        author = request.form['author']
        
        new_post = {
            'id': len(posts) + 1,
            'title': title,
            'content': content,
            'author': author,
            'date': datetime.now()
        }
        posts.append(new_post)
        flash('文章创建成功！', 'success')
        return redirect(url_for('index'))
    
    return render_template('create.html')

@app.route('/api/posts')
def api_posts():
    """API接口：获取所有文章"""
    return jsonify(posts)

@app.route('/api/posts/<int:post_id>')
def api_post(post_id):
    """API接口：获取指定文章"""
    post = next((p for p in posts if p['id'] == post_id), None)
    if post is None:
        return jsonify({'error': '文章不存在'}), 404
    return jsonify(post)

@app.errorhandler(404)
def not_found(error):
    """404错误处理"""
    return render_template('404.html'), 404

@app.errorhandler(500)
def internal_error(error):
    """500错误处理"""
    return render_template('500.html'), 500

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)
```

---

## 问题82：如何使用Flask模板系统？

### 🤔 问题描述
Flask的模板系统是什么？如何使用Jinja2模板引擎？模板继承和包含有什么作用？

### 💡 详细解答

#### 模板系统基础

Flask使用Jinja2作为模板引擎，支持：
- 变量替换
- 控制结构
- 模板继承
- 过滤器
- 宏定义

#### 基本用法

```python
# 在Flask应用中使用模板
from flask import render_template

@app.route('/')
def index():
    return render_template('index.html', 
                         title='首页', 
                         users=['张三', '李四', '王五'])
```

#### 模板语法

```html
<!-- base.html -->
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}默认标题{% endblock %}</title>
</head>
<body>
    <header>
        <h1>{% block header %}网站标题{% endblock %}</h1>
    </header>
    
    <main>
        {% block content %}{% endblock %}
    </main>
    
    <footer>
        <p>&copy; 2024 我的网站</p>
    </footer>
</body>
</html>

<!-- index.html -->
{% extends "base.html" %}

{% block title %}{{ title }}{% endblock %}

{% block content %}
<h2>用户列表</h2>
<ul>
    {% for user in users %}
        <li>{{ user }}</li>
    {% endfor %}
</ul>

{% if users %}
    <p>共有 {{ users|length }} 个用户</p>
{% else %}
    <p>暂无用户</p>
{% endif %}
{% endblock %}
```

### 📝 代码示例

```python
# Flask模板系统示例
from flask import Flask, render_template, request, flash, redirect, url_for
from datetime import datetime

app = Flask(__name__)
app.secret_key = 'template-demo-key'

# 模拟数据
users = [
    {'id': 1, 'name': '张三', 'email': 'zhangsan@example.com', 'age': 25},
    {'id': 2, 'name': '李四', 'email': 'lisi@example.com', 'age': 30},
    {'id': 3, 'name': '王五', 'email': 'wangwu@example.com', 'age': 28}
]

@app.route('/')
def index():
    """首页"""
    return render_template('index.html', 
                         title='用户管理系统',
                         users=users,
                         current_time=datetime.now())

@app.route('/user/<int:user_id>')
def user_detail(user_id):
    """用户详情页"""
    user = next((u for u in users if u['id'] == user_id), None)
    if user is None:
        flash('用户不存在', 'error')
        return redirect(url_for('index'))
    
    return render_template('user_detail.html', user=user)

@app.route('/search')
def search():
    """搜索页面"""
    query = request.args.get('q', '')
    results = []
    
    if query:
        results = [u for u in users if query.lower() in u['name'].lower()]
    
    return render_template('search.html', 
                         query=query, 
                         results=results)

if __name__ == '__main__':
    app.run(debug=True)
```

```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}用户管理系统{% endblock %}</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 20px; }
        .header { background: #f0f0f0; padding: 20px; margin-bottom: 20px; }
        .nav { margin-bottom: 20px; }
        .nav a { margin-right: 20px; text-decoration: none; color: #333; }
        .nav a:hover { color: #007bff; }
        .content { max-width: 800px; margin: 0 auto; }
        .user-card { border: 1px solid #ddd; padding: 15px; margin: 10px 0; border-radius: 5px; }
        .flash-message { padding: 10px; margin: 10px 0; border-radius: 5px; }
        .flash-success { background: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
        .flash-error { background: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }
    </style>
</head>
<body>
    <div class="header">
        <h1>{% block header %}用户管理系统{% endblock %}</h1>
        <div class="nav">
            <a href="{{ url_for('index') }}">首页</a>
            <a href="{{ url_for('search') }}">搜索</a>
        </div>
    </div>
    
    <div class="content">
        {% with messages = get_flashed_messages(with_categories=true) %}
            {% if messages %}
                {% for category, message in messages %}
                    <div class="flash-message flash-{{ category }}">{{ message }}</div>
                {% endfor %}
            {% endif %}
        {% endwith %}
        
        {% block content %}{% endblock %}
    </div>
    
    <footer style="text-align: center; margin-top: 50px; color: #666;">
        <p>&copy; 2024 用户管理系统. 当前时间: {{ current_time.strftime('%Y-%m-%d %H:%M:%S') if current_time else '' }}</p>
    </footer>
</body>
</html>

<!-- templates/index.html -->
{% extends "base.html" %}

{% block title %}{{ title }}{% endblock %}

{% block content %}
<h2>用户列表</h2>

{% if users %}
    <p>共有 {{ users|length }} 个用户</p>
    
    {% for user in users %}
        <div class="user-card">
            <h3><a href="{{ url_for('user_detail', user_id=user.id) }}">{{ user.name }}</a></h3>
            <p><strong>邮箱:</strong> {{ user.email }}</p>
            <p><strong>年龄:</strong> {{ user.age }} 岁</p>
            <p><strong>ID:</strong> {{ user.id }}</p>
        </div>
    {% endfor %}
{% else %}
    <p>暂无用户数据</p>
{% endif %}

<div style="margin-top: 30px;">
    <h3>统计信息</h3>
    <ul>
        <li>总用户数: {{ users|length }}</li>
        <li>平均年龄: {{ (users|sum(attribute='age') / users|length)|round(1) if users else 0 }} 岁</li>
        <li>最年长用户: {{ users|max(attribute='age').name if users else '无' }}</li>
        <li>最年轻用户: {{ users|min(attribute='age').name if users else '无' }}</li>
    </ul>
</div>
{% endblock %}

<!-- templates/user_detail.html -->
{% extends "base.html" %}

{% block title %}{{ user.name }} - 用户详情{% endblock %}

{% block content %}
<div class="user-card">
    <h2>{{ user.name }} 的详细信息</h2>
    
    <table style="width: 100%; border-collapse: collapse;">
        <tr>
            <td style="padding: 10px; border: 1px solid #ddd;"><strong>姓名</strong></td>
            <td style="padding: 10px; border: 1px solid #ddd;">{{ user.name }}</td>
        </tr>
        <tr>
            <td style="padding: 10px; border: 1px solid #ddd;"><strong>邮箱</strong></td>
            <td style="padding: 10px; border: 1px solid #ddd;">{{ user.email }}</td>
        </tr>
        <tr>
            <td style="padding: 10px; border: 1px solid #ddd;"><strong>年龄</strong></td>
            <td style="padding: 10px; border: 1px solid #ddd;">{{ user.age }} 岁</td>
        </tr>
        <tr>
            <td style="padding: 10px; border: 1px solid #ddd;"><strong>用户ID</strong></td>
            <td style="padding: 10px; border: 1px solid #ddd;">{{ user.id }}</td>
        </tr>
    </table>
    
    <div style="margin-top: 20px;">
        <a href="{{ url_for('index') }}" style="background: #007bff; color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px;">返回首页</a>
    </div>
</div>
{% endblock %}

<!-- templates/search.html -->
{% extends "base.html" %}

{% block title %}搜索用户{% endblock %}

{% block content %}
<h2>搜索用户</h2>

<form method="GET" style="margin-bottom: 20px;">
    <input type="text" name="q" value="{{ query }}" placeholder="输入用户名..." style="padding: 10px; width: 300px;">
    <button type="submit" style="padding: 10px 20px; background: #007bff; color: white; border: none; border-radius: 5px;">搜索</button>
</form>

{% if query %}
    <h3>搜索结果: "{{ query }}"</h3>
    
    {% if results %}
        <p>找到 {{ results|length }} 个匹配的用户:</p>
        
        {% for user in results %}
            <div class="user-card">
                <h4><a href="{{ url_for('user_detail', user_id=user.id) }}">{{ user.name }}</a></h4>
                <p><strong>邮箱:</strong> {{ user.email }}</p>
                <p><strong>年龄:</strong> {{ user.age }} 岁</p>
            </div>
        {% endfor %}
    {% else %}
        <p>没有找到匹配的用户。</p>
    {% endif %}
{% else %}
    <p>请输入搜索关键词。</p>
{% endif %}
{% endblock %}
```

### 🎯 最佳实践

1. **使用模板继承**：减少重复代码
2. **合理使用过滤器**：格式化数据
3. **注意安全性**：避免XSS攻击
4. **优化性能**：合理使用缓存
5. **保持简洁**：避免复杂的模板逻辑

通过掌握Flask的模板系统，你就能创建出美观、功能完整的Web应用！
