# 请求与响应

## 问题156：如何处理HTTP请求？

**答：**
Flask提供了request对象来处理HTTP请求：

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/api/data', methods=['GET', 'POST', 'PUT', 'DELETE'])
def handle_request():
    # 获取请求方法
    method = request.method
    
    # 获取URL参数
    if request.method == 'GET':
        name = request.args.get('name', 'World')
        return f'Hello, {name}!'
    
    # 获取POST数据
    elif request.method == 'POST':
        data = request.get_json()
        return f'Received data: {data}'
    
    # 获取表单数据
    elif request.method == 'PUT':
        username = request.form.get('username')
        email = request.form.get('email')
        return f'User: {username}, Email: {email}'
    
    return 'Method not supported'
```

---

## 问题157：如何返回响应？

**答：**
Flask支持多种响应类型：

```python
from flask import Flask, jsonify, render_template, redirect, url_for

app = Flask(__name__)

@app.route('/')
def home():
    # 返回字符串
    return 'Hello, World!'

@app.route('/json')
def json_response():
    # 返回JSON
    return jsonify({'status': 'success', 'message': 'Hello'})

@app.route('/html')
def html_response():
    # 返回HTML
    return '<h1>Hello, World!</h1>'

@app.route('/template')
def template_response():
    # 返回模板
    return render_template('index.html', name='Alice')

@app.route('/redirect')
def redirect_response():
    # 重定向
    return redirect(url_for('home'))

@app.route('/custom')
def custom_response():
    # 自定义响应
    from flask import Response
    return Response('Custom response', status=201, mimetype='text/plain')
```

---

## 问题158：如何处理表单数据？

**答：**
Flask提供了多种处理表单数据的方式：

```python
from flask import Flask, request, render_template

app = Flask(__name__)

@app.route('/form', methods=['GET', 'POST'])
def handle_form():
    if request.method == 'POST':
        # 获取表单数据
        username = request.form['username']
        email = request.form['email']
        age = request.form.get('age', 0, type=int)
        
        # 处理数据
        return f'User: {username}, Email: {email}, Age: {age}'
    
    # 显示表单
    return '''
    <form method="POST">
        <input type="text" name="username" placeholder="Username" required>
        <input type="email" name="email" placeholder="Email" required>
        <input type="number" name="age" placeholder="Age">
        <button type="submit">Submit</button>
    </form>
    '''

# 处理文件上传
@app.route('/upload', methods=['POST'])
def upload_file():
    if 'file' in request.files:
        file = request.files['file']
        if file.filename != '':
            file.save(f'uploads/{file.filename}')
            return 'File uploaded successfully'
    return 'No file selected'
```
