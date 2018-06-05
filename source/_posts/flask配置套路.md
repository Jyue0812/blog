

flask



应用内：

三个文件夹 + 5个python文件

```
static

templates

views



config.py

forms.py

models.py

extensions.py

__init__.py
```

配置文件 config.py 配置 开发 测试 生产环境

```
import os
basedir = os.path.abspath(os.path.dirname(__file__))

class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'hard to guess string'
    SQLALCHEMY_COMMIT_ON_TEARDOWN = True
    SQLALCHEMY_TRACK_MODIFICATIONS = False
    FLASKY_POSTS_PER_PAGE = 10

    FLASK_MAIL_SERVER = 'smtp.qq.com'
    FLASK_MAIL_PORT= 465
    FLASK_MAIL_USE_SSL = True
    FLASK_MAIL_USE_TLS = False
    FLASK_MAIL_USERNAME = '1678033705@qq.com'
    FLASK_MAIL_PASSWORD = 'coohdgjzpxsnebab'

    TEMPLATES_AUTO_RELOAD = True

class DevelopConfig(Config):
    DEBUG = True
    SQLALCHEMY_DATABASE_URI = "sqlite:///" + os.path.join(basedir, "blog-dev.sqlite")


class TestingConfig(Config):
    TESTING = True
    SQLALCHEMY_DATABASE_URI = "sqlite:///" + os.path.join(basedir, "blog-test.sqlite")


class ProductConfig(Config):
    SQLALCHEMY_DATABASE_URI = "sqlite:///" + os.path.join(basedir, "blog.sqlite")

config = {
    'develop': DevelopConfig,
    'testing': TestingConfig,
    'products': ProductConfig,
    'default': DevelopConfig,
}
```

init.py

```
from flask import Flask
from app.config import config
from extensions import config_extensions
from app.views import register_blueprint

def create_app(config_name):
    app = Flask(__name__)
    app.config.from_object(config.get(config_name or 'default'))
    config_extensions(app)
    register_blueprint(app)
    register_blueprint(app)
    return app
```

extensions.py

```
from flask_bootstrap import Bootstrap
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
from flask_mail import Mail
from flask_moment import Moment
from flask_login import LoginManager


db = SQLAlchemy()
boot = Bootstrap()
migrate = Migrate(db=db)
mail = Mail()
moment = Moment()
login_manager = LoginManager()
login_manager.session_protection = 'strong'
login_manager.login_view = 'auth.login'


def config_extensions(app):
    db.init_app(app)
    boot.init_app(app)
    migrate.init_app(app)
    mail.init_app(app)
    moment.init_app(app)
    login_manager.init_app(app)
    login_manager.login_view = 'user.login'
    login_manager.login_message = '请登录后再访问'
```

