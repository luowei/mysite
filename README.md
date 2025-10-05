# mysite

基于 Django 框架的投票系统示例项目

## 项目简介

mysite 是一个使用 Django 框架开发的 Web 应用示例，实现了一个简单的在线投票系统。这是一个典型的 Django 入门项目，展示了 Django 的基本特性和 MVC（MTV）架构模式的应用。

## 技术栈

- **开发语言**: Python
- **Web 框架**: Django (dev 版本)
- **数据库**: SQLite3 (开发环境)
- **模板引擎**: Django Template
- **管理后台**: Django Admin

## 功能特性

- 投票问题管理（Poll）
- 投票选项管理（Choice）
- 用户投票功能
- 投票结果展示
- Django Admin 后台管理
- 自动化的 URL 路由
- ORM 数据库操作

## 项目结构

```
mysite/
├── manage.py              # Django 项目管理脚本
├── db.sqlite3            # SQLite 数据库文件
├── README.md             # 项目说明文档
├── mysite/               # 项目配置目录
│   ├── __init__.py
│   ├── settings.py       # Django 配置文件
│   ├── urls.py          # 根 URL 配置
│   └── wsgi.py          # WSGI 部署配置
└── polls/               # 投票应用
    ├── __init__.py
    ├── models.py        # 数据模型定义
    ├── views.py         # 视图函数
    ├── urls.py          # URL 路由配置
    ├── admin.py         # Admin 后台配置
    ├── tests.py         # 单元测试
    ├── templates/       # 模板文件
    │   └── polls/
    │       ├── index.html    # 投票列表页
    │       ├── detail.html   # 投票详情页
    │       └── results.html  # 结果展示页
    └── migrations/      # 数据库迁移文件
```

## 数据模型

### Poll (投票问题)
- `question`: CharField - 问题文本（最大 20 字符）
- `pub_date`: DateTimeField - 发布日期

### Choice (投票选项)
- `poll`: ForeignKey - 关联的投票问题
- `choice_text`: CharField - 选项文本（最大 200 字符）
- `votes`: IntegerField - 票数（默认为 0）

## 核心功能模块

### 视图函数 (polls/views.py)

1. **index(request)** - 投票列表
   - 显示最新的 5 个投票问题
   - 按发布日期倒序排列

2. **detail(request, poll_id)** - 投票详情
   - 展示指定投票的详细信息
   - 显示所有可选项

3. **vote(request, poll_id)** - 投票处理
   - 处理用户的投票提交
   - 更新选项的票数
   - 重定向到结果页面

4. **results(request, poll_id)** - 结果展示
   - 显示投票结果统计

### URL 路由 (polls/urls.py)

- `/polls/` - 投票列表页
- `/polls/<poll_id>/` - 投票详情页
- `/polls/<poll_id>/results/` - 结果展示页
- `/polls/<poll_id>/vote/` - 投票提交处理

## 依赖要求

- **Python**: 2.7 或 3.x
- **Django**: 使用 dev 版本（建议使用稳定版本如 1.11 或 2.x）
- **SQLite**: 无需额外安装（Python 内置）

## 安装和运行

### 1. 克隆项目

```bash
cd /Users/luowei/projects/My_Github/apps/mysite
```

### 2. 安装 Django

```bash
# 使用 pip 安装 Django
pip install django
```

### 3. 数据库迁移

```bash
# 创建数据库表
python manage.py migrate

# 创建超级用户（用于 Admin 后台）
python manage.py createsuperuser
```

### 4. 运行开发服务器

```bash
# 启动 Django 开发服务器
python manage.py runserver

# 或指定端口
python manage.py runserver 8000
```

### 5. 访问应用

- **投票系统首页**: http://127.0.0.1:8000/polls/
- **管理后台**: http://127.0.0.1:8000/admin/

## 使用说明

### 创建投票

1. 访问管理后台：http://127.0.0.1:8000/admin/
2. 使用超级用户账号登录
3. 在 Polls 模块中添加投票问题
4. 为每个问题添加多个选项

### 进行投票

1. 访问投票首页：http://127.0.0.1:8000/polls/
2. 选择一个投票问题
3. 选择一个选项并提交
4. 查看投票结果

## 开发要点

### Django 配置 (mysite/settings.py)

```python
# 已安装的应用
INSTALLED_APPS = (
    'django.contrib.admin',      # 管理后台
    'django.contrib.auth',       # 认证系统
    'django.contrib.contenttypes',
    'django.contrib.sessions',   # 会话管理
    'django.contrib.messages',   # 消息框架
    'django.contrib.staticfiles', # 静态文件
    'polls',                     # 投票应用
)

# 数据库配置
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

### 常用 Django 命令

```bash
# 创建新的迁移文件
python manage.py makemigrations

# 执行数据库迁移
python manage.py migrate

# 创建超级用户
python manage.py createsuperuser

# 启动开发服务器
python manage.py runserver

# 进入 Django Shell
python manage.py shell

# 收集静态文件（生产环境）
python manage.py collectstatic
```

## 学习要点

本项目展示了以下 Django 核心概念：

1. **MTV 架构模式**
   - Model: 数据模型定义（models.py）
   - Template: 模板文件（templates/）
   - View: 视图逻辑（views.py）

2. **ORM 操作**
   - 模型定义和关系
   - 数据查询（objects.all(), get(), filter()）
   - 数据排序（order_by()）

3. **URL 路由**
   - URL 模式配置
   - 命名空间的使用
   - reverse() 反向解析

4. **模板系统**
   - 模板继承
   - 变量渲染
   - 模板标签和过滤器

5. **表单处理**
   - POST 数据处理
   - 表单验证
   - 重定向（HttpResponseRedirect）

6. **错误处理**
   - get_object_or_404() 快捷函数
   - 自定义错误消息

## 扩展建议

- 添加用户认证功能
- 实现投票权限控制（一人一票）
- 添加投票时间限制
- 优化前端界面（Bootstrap/Tailwind CSS）
- 添加数据可视化（图表展示）
- 迁移到 PostgreSQL/MySQL 数据库
- 添加 API 接口（Django REST framework）

## 注意事项

- 当前使用的是 Django 开发版本，生产环境建议使用稳定版本
- SECRET_KEY 已暴露，生产环境需要重新生成
- DEBUG 模式已开启，生产环境需要关闭
- 使用 SQLite 数据库，生产环境建议使用 PostgreSQL 或 MySQL

## 许可证

本项目仅供学习和参考使用。
