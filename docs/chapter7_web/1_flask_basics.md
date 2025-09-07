# Flask基础

## 问题1：什么是Flask？如何安装Flask？

Flask是一个轻量级的Python Web框架，简单易学，适合快速开发Web应用：

```python
# 安装Flask
# pip install flask

# 基本Flask应用
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题2：如何创建Flask应用和路由？

```python
from flask import Flask

app = Flask(__name__)

# 基本路由
@app.route('/')
def index():
    return '欢迎来到首页'

# 带参数的路由
@app.route('/user/<name>')
def user(name):
    return f'你好, {name}!'

# 带类型转换的路由
@app.route('/post/<int:post_id>')
def show_post(post_id):
    return f'文章ID: {post_id}'

# 多个路由指向同一个函数
@app.route('/about')
@app.route('/info')
def about():
    return '关于我们'

# 指定HTTP方法
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        return '登录处理'
    return '登录页面'

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题3：如何处理请求和响应？

```python
from flask import Flask, request, jsonify, redirect, url_for

app = Flask(__name__)

# 处理GET请求参数
@app.route('/search')
def search():
    query = request.args.get('q', '')
    return f'搜索: {query}'

# 处理POST请求数据
@app.route('/submit', methods=['POST'])
def submit():
    name = request.form.get('name')
    email = request.form.get('email')
    return f'提交成功: {name}, {email}'

# 处理JSON数据
@app.route('/api/data', methods=['POST'])
def api_data():
    data = request.get_json()
    return jsonify({'status': 'success', 'data': data})

# 重定向
@app.route('/redirect')
def redirect_example():
    return redirect(url_for('index'))

# 自定义响应
@app.route('/custom')
def custom_response():
    from flask import make_response
    response = make_response('自定义响应')
    response.headers['Content-Type'] = 'text/plain'
    return response

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题4：如何使用Flask模板？

```python
from flask import Flask, render_template

app = Flask(__name__)

# 基本模板渲染
@app.route('/')
def index():
    return render_template('index.html')

# 传递变量到模板
@app.route('/user/<name>')
def user(name):
    return render_template('user.html', name=name)

# 传递多个变量
@app.route('/dashboard')
def dashboard():
    user_info = {
        'name': '张三',
        'age': 25,
        'city': '北京'
    }
    posts = [
        {'title': '文章1', 'content': '内容1'},
        {'title': '文章2', 'content': '内容2'}
    ]
    return render_template('dashboard.html', user=user_info, posts=posts)

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题5：如何使用Flask表单处理？

```python
from flask import Flask, render_template, request, flash, redirect, url_for
from flask_wtf import FlaskForm
from wtforms import StringField, TextAreaField, SubmitField
from wtforms.validators import DataRequired, Email

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your-secret-key'

# 定义表单类
class ContactForm(FlaskForm):
    name = StringField('姓名', validators=[DataRequired()])
    email = StringField('邮箱', validators=[DataRequired(), Email()])
    message = TextAreaField('消息', validators=[DataRequired()])
    submit = SubmitField('提交')

# 处理表单
@app.route('/contact', methods=['GET', 'POST'])
def contact():
    form = ContactForm()
    if form.validate_on_submit():
        flash('消息发送成功！')
        return redirect(url_for('contact'))
    return render_template('contact.html', form=form)

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题6：如何使用Flask会话和Cookie？

```python
from flask import Flask, session, request, make_response

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your-secret-key'

# 会话管理
@app.route('/login', methods=['POST'])
def login():
    username = request.form.get('username')
    password = request.form.get('password')
    
    if username == 'admin' and password == 'password':
        session['logged_in'] = True
        session['username'] = username
        return '登录成功'
    return '登录失败'

@app.route('/logout')
def logout():
    session.pop('logged_in', None)
    session.pop('username', None)
    return '已退出登录'

@app.route('/profile')
def profile():
    if session.get('logged_in'):
        return f'欢迎, {session["username"]}!'
    return '请先登录'

# Cookie管理
@app.route('/set_cookie')
def set_cookie():
    response = make_response('Cookie已设置')
    response.set_cookie('user_preference', 'dark_theme')
    return response

@app.route('/get_cookie')
def get_cookie():
    preference = request.cookies.get('user_preference')
    return f'用户偏好: {preference}'

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题7：如何使用Flask错误处理？

```python
from flask import Flask, render_template, abort

app = Flask(__name__)

# 自定义错误页面
@app.errorhandler(404)
def not_found(error):
    return render_template('404.html'), 404

@app.errorhandler(500)
def internal_error(error):
    return render_template('500.html'), 500

# 手动触发错误
@app.route('/error')
def error():
    abort(404)

# 处理特定异常
@app.errorhandler(ValueError)
def handle_value_error(error):
    return '值错误', 400

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题8：如何使用Flask蓝图？

```python
from flask import Flask, Blueprint

app = Flask(__name__)

# 创建蓝图
main_bp = Blueprint('main', __name__)
api_bp = Blueprint('api', __name__, url_prefix='/api')

# 在蓝图中定义路由
@main_bp.route('/')
def index():
    return '首页'

@main_bp.route('/about')
def about():
    return '关于我们'

@api_bp.route('/users')
def get_users():
    return {'users': ['张三', '李四', '王五']}

@api_bp.route('/users/<int:user_id>')
def get_user(user_id):
    return {'user_id': user_id, 'name': f'用户{user_id}'}

# 注册蓝图
app.register_blueprint(main_bp)
app.register_blueprint(api_bp)

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题9：如何使用Flask数据库？

```python
from flask import Flask, render_template, request, redirect, url_for
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///example.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)

# 定义模型
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)

    def __repr__(self):
        return f'<User {self.username}>'

# 创建表
with app.app_context():
    db.create_all()

# 路由
@app.route('/')
def index():
    users = User.query.all()
    return render_template('index.html', users=users)

@app.route('/add_user', methods=['POST'])
def add_user():
    username = request.form['username']
    email = request.form['email']
    user = User(username=username, email=email)
    db.session.add(user)
    db.session.commit()
    return redirect(url_for('index'))

if __name__ == '__main__':
    app.run(debug=True)
```

## 问题10：Flask应用的实际部署

```python
# 生产环境配置
class Config:
    SECRET_KEY = 'your-secret-key'
    SQLALCHEMY_DATABASE_URI = 'sqlite:///app.db'
    SQLALCHEMY_TRACK_MODIFICATIONS = False

class DevelopmentConfig(Config):
    DEBUG = True

class ProductionConfig(Config):
    DEBUG = False

# 应用工厂模式
def create_app(config_name='development'):
    app = Flask(__name__)
    
    if config_name == 'development':
        app.config.from_object(DevelopmentConfig)
    else:
        app.config.from_object(ProductionConfig)
    
    # 初始化扩展
    db.init_app(app)
    
    # 注册蓝图
    app.register_blueprint(main_bp)
    app.register_blueprint(api_bp)
    
    return app

# 创建应用
app = create_app()

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

## 总结

Flask是一个轻量级的Web框架，主要特点：
- **简单易学**：核心功能简单，易于理解
- **灵活扩展**：通过扩展添加功能
- **模板支持**：Jinja2模板引擎
- **路由系统**：灵活的路由定义
- **会话管理**：内置会话和Cookie支持
- **错误处理**：自定义错误页面
- **蓝图系统**：模块化应用结构
- **数据库支持**：SQLAlchemy集成
- **部署友好**：支持多种部署方式
