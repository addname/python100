# 路由与视图函数

## 问题70：什么是路由？

**答：**
路由是Web应用中URL与处理函数之间的映射关系：

```python
from flask import Flask

app = Flask(__name__)

# 基本路由
@app.route('/')
def home():
    return 'Welcome to my website!'

@app.route('/about')
def about():
    return 'This is the about page'

@app.route('/user/<username>')
def user_profile(username):
    return f'Hello, {username}!'

if __name__ == '__main__':
    app.run()
```

---

## 问题71：如何定义路由？

**答：**
Flask提供了多种定义路由的方式：

```python
from flask import Flask

app = Flask(__name__)

# 基本路由
@app.route('/')
def index():
    return 'Home page'

# 带参数的路由
@app.route('/user/<int:user_id>')
def user(user_id):
    return f'User ID: {user_id}'

# 多种HTTP方法
@app.route('/api/data', methods=['GET', 'POST'])
def api_data():
    return 'API endpoint'

# 路由装饰器
def admin_required(f):
    def decorated_function(*args, **kwargs):
        # 检查管理员权限
        return f(*args, **kwargs)
    return decorated_function

@app.route('/admin')
@admin_required
def admin():
    return 'Admin panel'
```

---

## 问题72：什么是视图函数？

**答：**
视图函数是处理HTTP请求并返回响应的函数：

```python
from flask import Flask, request, jsonify

app = Flask(__name__)

# 简单视图函数
@app.route('/hello')
def hello():
    return 'Hello, World!'

# 带参数的视图函数
@app.route('/greet/<name>')
def greet(name):
    return f'Hello, {name}!'

# 处理不同HTTP方法的视图函数
@app.route('/api/users', methods=['GET', 'POST'])
def users():
    if request.method == 'GET':
        return jsonify({'users': ['Alice', 'Bob']})
    elif request.method == 'POST':
        data = request.get_json()
        return jsonify({'message': 'User created', 'data': data})

# 返回不同响应类型的视图函数
@app.route('/data')
def get_data():
    return jsonify({'status': 'success', 'data': [1, 2, 3]})

@app.route('/html')
def html_response():
    return '<h1>HTML Response</h1>'
```
