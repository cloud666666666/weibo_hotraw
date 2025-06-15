# 微博热搜数据采集与分析系统

## 项目简介

这是一个基于 Python 开发的微博热搜数据采集与分析系统，集成了数据爬取、存储、分析和可视化等功能。系统采用 Django + Flask 双框架架构，提供完整的 Web 界面进行数据展示和分析。

## 功能特性

### 🕷️ 数据采集功能
- **实时热搜爬取**：定时获取微博热搜榜数据
- **数据存储**：支持 MySQL 数据库和 JSON 文件存储
- **智能去重**：自动处理重复数据
- **定时任务**：支持定时自动采集

### 📊 数据分析功能
- **分类统计**：按类别统计热搜话题分布
- **热度分析**：统计搜索量和话题热度
- **词频分析**：基于 jieba 分词的文本分析
- **趋势分析**：热搜话题变化趋势

### 🎨 可视化展示
- **实时热搜榜**：展示当前热搜排行
- **数据图表**：echarts 图表展示分析结果
- **词云图**：热门词汇可视化
- **历史数据**：热搜历史记录查看

### 🔧 管理功能
- **用户管理**：支持用户注册登录
- **数据管理**：Django Admin 后台管理
- **密码修改**：用户密码修改功能
- **数据导出**：支持数据导入导出

## 技术栈

### 后端技术
- **Python 3.x**：主要开发语言
- **Django 5.0.6**：Web 框架（管理后台）
- **Flask 3.0.3**：Web 框架（API 服务）
- **MySQL**：数据库存储
- **Selenium 4.21.0**：Web 自动化工具

### 数据处理
- **requests 2.31.0**：HTTP 请求库
- **BeautifulSoup4**：HTML 解析
- **pandas 2.2.2**：数据处理
- **numpy 1.26.4**：数值计算
- **jieba 0.42.1**：中文分词

### 可视化组件
- **pyecharts 2.0.5**：Python 图表库
- **Bootstrap 5**：前端 UI 框架
- **ECharts**：JavaScript 图表库

### 其他工具
- **schedule 1.2.1**：任务调度
- **pymysql 1.1.0**：MySQL 连接器
- **scikit-learn 1.4.2**：机器学习库

## 项目结构

```
weibo_hotraw/
├── get_weibo.py          # 微博数据爬取主程序
├── app.py               # Flask Web 应用
├── demo.py              # 数据分析演示脚本
├── fc.py                # 文本分词处理工具
├── try.py               # 哈希工具函数
├── manage.py            # Django 管理脚本
├── requirements.txt     # 项目依赖
├── data.json           # JSON 数据文件
├── data.csv            # CSV 数据文件
├── chromedriver.exe    # Chrome 驱动程序
├── testdjango/         # Django 项目目录
│   ├── settings.py     # Django 配置文件
│   ├── urls.py         # URL 路由配置
│   └── wsgi.py         # WSGI 配置
├── user/               # 用户管理应用
│   ├── models.py       # 数据模型
│   ├── views.py        # 视图函数
│   └── resource.py     # 资源配置
├── utils/              # 工具模块
│   ├── spider.py       # 爬虫工具
│   └── *.log          # 日志文件
├── templates/          # HTML 模板文件
│   ├── index.html      # 主页模板
│   ├── ana.html        # 分析页面
│   ├── cloud.html      # 词云页面
│   ├── history.html    # 历史数据页面
│   └── login.html      # 登录页面
└── static/            # 静态资源文件
```

## 安装部署

### 环境要求
- Python 3.7+
- MySQL 5.7+
- Chrome 浏览器

### 安装步骤

1. **克隆项目**
```bash
git clone <repository-url>
cd weibo_hotraw
```

2. **安装依赖**
```bash
pip install -r requirements.txt
```

3. **数据库配置**
```bash
# 创建 MySQL 数据库
CREATE DATABASE testdjango;

# 执行数据库迁移
python manage.py makemigrations
python manage.py migrate
```

4. **修改配置**
编辑 `testdjango/settings.py` 中的数据库配置：
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'testdjango',
        'HOST': '127.0.0.1',
        'PORT': 3306,
        'USER': 'root',
        'PASSWORD': 'your_password'  # 修改为你的密码
    }
}
```

同时修改 `get_weibo.py` 中的数据库连接配置。

5. **创建超级用户**
```bash
python manage.py createsuperuser
```

## 使用方法

### 启动 Django 服务
```bash
python manage.py runserver
```
访问：http://127.0.0.1:8000/admin （管理后台）

### 启动 Flask 服务
```bash
python app.py
```
访问：http://127.0.0.1:5000 （Web 界面）

### 数据采集
```bash
# 单次采集
python get_weibo.py

# 或使用爬虫工具
python utils/spider.py
```

### 数据分析
```bash
# 运行分析脚本
python demo.py
```

## 主要功能说明

### 数据采集模块
- `get_weibo.py`：核心爬虫程序，获取微博热搜数据并存储到 MySQL
- `utils/spider.py`：定时爬虫工具，支持定时任务调度

### Web 应用模块
- `app.py`：Flask 应用，提供数据展示和 API 接口
- Django 项目：提供管理后台和用户管理功能

### 数据分析模块
- `demo.py`：数据统计分析，包括分类统计、热度分析等
- `fc.py`：文本分词和词频统计工具

## API 接口

### Flask 接口
- `GET /` - 主页
- `GET /data` - 获取表格数据
- `GET /start` - 启动爬虫

### Django 接口
- `/admin/` - 管理后台
- `/index/` - 热搜数据查看
- `/ana/` - 数据分析页面
- `/ciyun/` - 词云图页面
- `/history/` - 历史数据页面

## 注意事项

1. **Chrome 驱动**：确保 chromedriver.exe 版本与 Chrome 浏览器版本匹配
2. **数据库权限**：确保 MySQL 用户有足够的权限
3. **网络环境**：爬虫功能需要稳定的网络连接
4. **反爬策略**：注意微博反爬机制，建议设置合理的请求间隔
5. **数据量控制**：系统设置了 10 万条数据上限，会自动清理旧数据

