# Django框架

# 1.安装python环境和开发软件

## 1.1 windows下安装python环境

安装包下载：[https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled.png)

## 1.2 Pycharm 安装

安装包下载：[https://www.jetbrains.com/pycharm/download/#section=windows](https://www.jetbrains.com/pycharm/download/#section=windows)

Pycharm 分为专业版，和教育版

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%201.png)

# 2.新建项目和应用

## 2.1 使用 Pycharm 新建Django 项目

点击 New Project

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%202.png)

新建项目时 可以使用python虚拟环境

python 的虚拟环境可以为一个 python 项目提供独立的解释环境、依赖包等资源，既能够很好的隔离不同项目使用不同 python 版本带来的冲突

![Untitled.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%203.png)

其中 inherit global site-packges 可以继承全局python的包

make available to all projects 就是将python虚拟环境 添加到列表便于下次使用相同环境时使用

![批注 2021-11-22 101004.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/%E6%89%B9%E6%B3%A8_2021-11-22_101004.png)

新建项目完成

1. 项目目录里会有一个跟项目同名的，文件夹
2. 在同名问价夹中，settings.py 是用来配置项目基本信息的，urls.py 是用来配置网址url映射的

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%204.png)

## 2.2 修改 [settings.py](http://settings.py) 的配置信息

```python
# 自身的绝对路径 用于动态计算当前项目文件位置
BASE_DIR = Path(__file__).resolve().parent.parent
```

![批注 2021-11-22 103226.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/%E6%89%B9%E6%B3%A8_2021-11-22_103226.png)

```python
# DEBUG 项目 启动模式 true 就是以调试模式启动 false 就是上线模式
# debug模式 检测代码改变后 立即重启项目 一旦有错误会有详细报错页面信息 但是 上线模式没有
DEBUG = True

# 请求头 指定 请求头 比如 127.0.0.0 只有请求头是127.0.0.0 才处理可以用于过滤请求 ALLOWED_HOSTS = ['127.0.0.1']
# 如果是内网访问 ALLOWED_HOSTS = ['0.0.0.0']就是同一个内网的所有都可以访问
# 该信息一旦不为空 就需要全部配置
ALLOWED_HOSTS = []
```

![批注 2021-11-22 103420.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/%E6%89%B9%E6%B3%A8_2021-11-22_103420.png)

```python
# INSTALLED_APPS  就是当你使用 “python manage.py startapp 文件名”  新建app时就需要到 settings.py 里面注册
# 比如 python manage.py startapp app01 就需要在 INSTALLED_APPS 添加
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app01',
]
```

![批注 2021-11-22 103635.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/%E6%89%B9%E6%B3%A8_2021-11-22_103635.png)

```python
# 表明django主路由文件
ROOT_URLCONF = 'newone.urls'
#TEMPLATES  是模板配置项
TEMPLATES = [
    {
        # 模板引擎
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # dirs 模板目录
        'DIRS': [BASE_DIR / 'templates']
        ,
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

![批注 2021-11-22 104346.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/%E6%89%B9%E6%B3%A8_2021-11-22_104346.png)

DATABASES  是数据库配置项 用来连接数据库，但是默认使用的是 sqlite 数据库 这里我们使用Mysql数据作为演示

```python
# 数据库
DATABASES = {
    # 'default': {
    #     'ENGINE': 'django.db.backends.sqlite3',
    #     'NAME': BASE_DIR / 'db.sqlite3',
    # }
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'test',
        'HOST': '127.0.0.1',
        'POST': 3306,
        'USER': 'root',
        'PASSWORD': 'root',
    }
}
```

![批注 2021-11-22 104701.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/%E6%89%B9%E6%B3%A8_2021-11-22_104701.png)

最后我们把项目修改成中文，时区修改为 东八区

```python
# 语言信息配置 比如 需要中文 LANGUAGE_CODE = 'zh-Hans'
LANGUAGE_CODE = 'zh-Hans'
# 格林尼治时间   TIME_ZONE = 'Asia/Shanghai'  改成东八区
TIME_ZONE = 'Asia/Shanghai'
```

![批注 2021-11-22 105040.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/%E6%89%B9%E6%B3%A8_2021-11-22_105040.png)

# 3. 新建Django 应用

Django应用指的是 django 完整项目下的 一个模块，比如一个商品管理系统下可分为商品列表模块，管理人员模块，订单管理模块等

## 3.1 新建app

在terminal 里输入以下命令

```bash
python manage.py startapp textApi
```

应用新建完成可以看到在左侧新建了一个 textApi 文件夹 这个就是 app 文件夹

文件夹中的 [models.py](http://models.py) 是应用的数据模型文件

文件夹中的 views[.py](http://urls.py) 是试图文件

文件夹中的 [apps.py](http://apps.py) 是应用配置文件

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%205.png)

## 3.2 把新建应用添加到django项目中

只需要 在 项目同名文件夹中的，settings.py 中`INSTALLED_APPS` 进行注册即可

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'testApi'
]
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%206.png)

# 4. Django和mysql

## 4.1 Django 设计模式

## django配置mysql

安装 mysqlclient  pip install mysqlclient

（需要配置好 mysql 环境变量）创建数据库 create databse 数据库名 default charset utf8

数据库名通常和项目名一样

然后 [在setting.py](http://在setting.py) 里面配置   django 支持四种数据库除了mysql和sqlite 还有 oracle和postgresql

模型就是一个python类，他是由diango.db.models.Model 派生出来的子类

一个模型类就是代表数据库中的一张数据表

模型类中的每个类属性都代表数据库中的一个字段

模型是数据交互的接口，是表示和操作数据库的方法和方式  就不需要直接操作 mysql了

怎么实现这个模型呢？

ORM框架

ORM 就是对象关系映射，它允许你使用类和对象对数据库进行操作，从而避免通过sql语句操作数据库

ORM作用：

1. 简历模型类和表之间的对应关系，允许我们通过面向对象的方式操作数据库。
2. 根据设计的模型类生成数据库中的表格
3. 通过简单的配置就可以进行数据库切换

## orm优点

1. 显而易见 只需要面向对象编程，不需要面向数据库编写代码
2. 失信了数据模型和数据库的解耦，频闭了不停数据库操作上的差异（无所谓 mysql 还是 oracle）

## orm缺点

1. 对于复杂业务，使用成本很高
2. 根据对象的操作转换成sql语句，根据查询的结果转化成对象，在映射过程中有性能损失

### 映射关系

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%207.png)

## 4.2 新建数据库

mysql 常用命令行 

mysql  连接服务器-h主机地址 -u用户名 -p用户密码      ：     mysql -uroot -proot

mysql 修改密码  mysqladmin -u用户名 -u旧密码 password 新密码  ： 

mysqladmin -uroot -proot password 123456（改密码）

mysqladmin -uroot -password 123456（添加一个密码）

mysql 创建数据库  create database <数据库名>  ： mysql create test

**创建数据库并分配用户**

①CREATE DATABASE 数据库名;

②GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON 数据库名.* TO 数据库名@localhost IDENTIFIED BY '密码';

③SET PASSWORD FOR '数据库名'@'localhost' = OLD_PASSWORD('密码');

显示数据库 mysql> show databases;

删除数据库 mysql> drop database <数据库名> ：  drop database test;

连接数据库 use <数据库名>   ：  use test

创建数据库  create table <表名> （<字段1><类型1>[,..<字段名n> <类型n>]）

删除表 drop table <表名>  ：  drop table name

表中插入数据 insert  into <表名> [(<字段名1>)[[,..<字段名n >]] value (值1)[,(值n)]

查询表中数据  select <字段1，字段2，...> from <表名> where <表达式> 

查询前两行数据  mysql> select * from MyClass order by id limit 0,2;

查询表myclass中的所有数据 mysql> select * from MyClass;

删除表myclass中编号为1的记录 mysql> delete from myclass where id = 1;

修改表中数据 update 表名 set 字段=新值，...  where 条件

mysql> update myclass set name='mary' where id='1';

增加字段 alter table 表名 add 字段 类型 其他；：  

mysql> alter table myclass add passtest int(4) default '0';

修改表名 ： rename table 原表名 to 新表名；： 

mysql> rename tsble myclass to youclass

导出 数据库 mysqldump -u 用户名 -p数据库名 > 导出的文件名

导出 表  mysqldump -u 用户名  -p 数据库名 表名 > 导出的文件名

导出的文件放在 mysql\bin下

## 4.3 ORM新建表

## 4.4 数据库迁移

### 迁移时diango同步您对模型所做的修改（添加字段，删除模型等）到您的数据库模式的方式

1. 生成迁移文件—命令 python [manage.py](http://manage.py) makemigrations  将应用下的models.py文件生成一个中间文件，并保存在migrations文件夹中
2. 执行迁移脚本—python [manage.py](http://manage.py) migrate  执行迁移程序，将每个应用下的migrations目录中的中间文件同步到数据库

在迁移过程中有很多不是自己创建的文件 这是因为 django 是非常重度的框架 他已经写好了很多表，需要我们手动同步，所以我们一开始就可以先同步一次 避免影响使用

迁移完成的 数据库 默认django 添加 id字段 并附加属性primary_key 

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%208.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%209.png)

 BooleanField（）  对应   mysql  tinyint（1） 

编程语言中使用 true 和 false mysql里面使用 1和0；

charfield （） 对应数据库  varchar  必须指定 max_length参数值

DateField（）  数据库类型 date  作用表示日期  

参数  

1. auto_now:每次保存对象时，自动设置该字段为当前时间（取值true/false）
2. auto_now_add：当对象第一次被创建时取当前时间（取值true/false）
3. default : 设置当前时间（取值：字符串格式时间如“2019-6-1”）自己给值

以上参数只能多选一

DateTimeField()  对应数据库类型 datetime（6） 作用表示日期和时间 参数同DateField()

FloatField()  对应数据库类型 ： double 编程语言和数据库中都使用小数表示值

DecimalField()  跟钱相关 

1. 对应数据库类型 decimal（x,y）
2. 编程语言：使用小数表示该列的值
3. 在数据库中：使用小数

参数

1. max_digits:位数总数，包括小数点后面的位数。该值必须大于等于
decima_places
2. decimal_places:小数点后面的数字数量

EmailField()：对应数据库类型 varchar 编程语言和数据库中使用字符串

很明显用于存放 邮箱   应该是是使用了  类似正则验证

IntegerField()

数据库类型：int   编程语言和数据库中使用整数

ImageField()

数据库类型：varchar(100)

作用：在数据库中为了保存图片的路径（我觉的没啥用）

编程语言和数据库中使用字符串

TextField()

数据库类型：longtext（用于论坛文档之类）

作用 表示不定长的字符数据

## 4.5模型类 字段选项

1. primary_key  如果设置为true，则表示该列为主键，如果指定一个字段为主键则，数据表不会自动生成，id列
2. blank 设置为true时，字段可以为空，设置为false时，字段必须填写
3. null 设置为true时，字段必须可以为空，设置为false时，字段必须填写 默认值false   如果设置为false 为避免出错建议加入 defult选项来设置默认值 （不建议使用）
4. defult 设置所在列的默认值，如果该字段选项null=false ，建议添加此项 在使用过程中会发现即使你设置了default 表中1也不会呈现出你设置的数据 因为 django 为了避免出现问题 尽量避免操作数据库表 ， 但是设置default 等你往里面放值的时候会体现出来，在插入新字段时如果没有，设置default 就会报错提醒你添加新值
5. db_index 如果设置为true，表示该列增加索引
6. unique 如果设置为true，表示该字段在数据库中的值必须是唯一的（不能重复出现）
7. db_column 指定列的名称，如果不指定的话则采用属性名作为列的名称
8. verbose_name 设置在admin界面上显示名称（后台）

任何修改过字段信息的操作，均要执行 

makemigrations和migrate

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2010.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2011.png)

## 模型类-Meta类

控制表信息  在模型类内部定义

```python
class Book(models.Model):
    title = models.CharField("书名", max_length=50)
    price = models.DecimalField("价格", max_digits=7, decimal_places=2)
    # charfield必须有 maxlength
    info = models.CharField(max_length=100, default='')

    class Meta:
        db_table = 'book'
```

 

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2012.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2013.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2014.png)

修改过后

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2015.png)

## 4.6ORM - 操作

对于数据的操作 基本的当然就是 增删改查操作了 即 CRUD

CURD 就是指在做计算处理时的增加（Create）读取查询（Read）

更新（Update） 和  删除（Delete）

Django ORM CRUD 核心 →  模型类.管理器对象  每一个模型类都会继承来自models.Model 的 object对象  这个对象就叫管理器对象

```python
#新建类
class MyModel(models.Model):
    title = models.CharField("书名", max_length=50, default='', unique=True)
    pub = models.CharField("出版社", max_length=100, default='')
    price = models.DecimalField("价格", max_digits=7, decimal_places=2)
    # charfield必须有 maxlength
    market_price = models.DecimalField("零售价", max_digits=7, decimal_places=2, default=0.0)
    info = models.CharField(max_length=100, default='')

    class Meta:
        db_table = 'book'

#方案1
eg:   mymodel.object.create(属性=值，属性=值，属性=值，.....)   #创建数据

#方案2  必须先实例化一个对象出来
eg:   obj = MyModel(属性=值，属性=值，.....)   #实例化一个对象
			obj.属性 = 值   #用于单个添加 或者临时添加
			obj.save()

```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2016.png)

## Django shell

python [manage.py](http://manage.py) shell

 

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2017.png)

# 5 数据库查询

1. all()方法
- 用法：mymodel.object.all()
- 作用：查询mymodel实体中所有的数据
- 等同于select * from table
- 返回值：QuerySet容器对象，内部存放mymodel实例

 

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2018.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2019.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2020.png)

1. values('列1'，’列2‘,.....)
- 用法：mymodel.objects.values(...)
- 作用：查询部分列的数据并返回 等同于select  列1，列2 from table
- 返回值：QuerySet  返回查询结果容器，容器内存字典，每个字典代表一条数据，格式为：{’列1‘：值1，'列2'：值2}

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2021.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2022.png)

3.values.list('列1'，'列2'，.....)

- 用法：mymodel.objects.values_list(...)
- 作用：返回元组形式的查询结果，等同于select 列1，列2 from xxx
- 返回值 QuerySet容器对象，内部存放元组
- 会将查询出来的数据封装到元组中，再封装到查询集合QuerySet中

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2023.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2024.png)

4.order_by()

- 用法：mymodel.objects.order_by('-列'，’列‘)    加负号就是降序不加默认就是升序
- 作用：与all（）方法不同，他会使用sql语句的ORDER BY子句对查询结果进行根据某个字段选择性的进行排序
- 说明：默认是按照升序排序，降序排序则需要在列前增加“-”表示
- order_by可以配合别的命令使用 ， 位置不影响

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2025.png)

可以通过  a1.query 取得对应的MySQL语句(结果必须是queryset)

我可太爱了吧 😼

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2026.png)

## 条件查询

1.filter(条件)

- 语法：mymodel.objects.filter(属性1=值1，属性2=值2)
- 作用：返回包含此条件的全部数据集
- 返回值：QuerySet容器对象，内部存放mymodel实例
- 说明：当多个属性在一起时为“与”关系，即当

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2027.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2028.png)

2.exclude(条件)

- 语法：mymodel.objects.exclude(条件)
- 作用：返回不包含此条件的全部数据集
- 实例：查询清华大学出版社，并且定价等于50以外的全部图书

```bash
books = models.Book.objects.exclude(pub="清华大学出版社"，price="50")
for book in books:
		print(book)
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2029.png)

3.get(条件)

- 语法：mymodel.objects.get(条件)
- 作用：返回满足条件的唯一一条数据
- 说明：该方法只能返回一条数据，查询结果多余一条数据则抛出Model.MultipleObjectsReturned异常，查询结果如果没有数据则抛出Model.DoesNotExist异常

查询结果 返回多条数据 报错 it turned 2

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2030.png)

查询条件不存在报错

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2031.png)

正确的查询一条数据

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2032.png)

## 怎么做非等值查询

where id>10

Book.objects.filter(id>10)  #  很显然不行会报错

方法：查询谓词    "  类属性+’__‘+谓词"

定义：做更灵活的条件查询时需要使用查询谓词

说明：每一个查询谓词是一个独立的查询功能

1._exact:等值查询

Book.objects.filter(id_excat=1)  相当于 select * from Book where id = 1

2._contains:包含指定值

Author.objects.filter(name_contains='w')  相当于 

select * from book where name like '%w%'

3._startswith:以....开始

4._endswith:以.....结束

5._gt:大于指定值  Book.objects.filter(age_gt=50)相当于

select * from Book where age > 50

6.__gte  ：大于等于

7.__lt :  小于

8.__lte:  小于等于(全部是双下划线)

9.__in : 查询数据是否在指定的范围内   Book.objects.filter(country_in=['中国','日本','韩国'])

10.__range: 查找数据是否在指定的区间范围内 Author.objects.filter(age__range=(35,50))  相当于 select  ...  where Author between 35 and 50;

## ORM 更新操作

### 修改单个实体的某些字段值

1. 查  通过 get() 得到某些字段的步骤
2. 改  通过对象.属性的方式修改数据
3. 保存 通过对象.save()保存数据

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2033.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2034.png)

在python shell 面板修改 数据时 如果数据表已经发生了改变一定注意 

先 exit()  然后 重新导入 实列   from testapi.models  import  Book

### 批量更改数据

1. 直接调用QuerySet的update（属性=值）实现批量修改

```bash
# 将id大于3的所有图书的价格定为0元
books = Book.objects.filter(id__gt=3)
books = update(price=0)

# 将所有书的零售价定位100元
books = Book.objects.all()
books.update(market_price=100)
```

## 删除数据

### 单个数据删除

1. 查找查询结果对应的一个数据对象
2. 调用这个数据对象的delete()方法

```python
try:
	author = Author.objects.get(id=1)
	author.delete()

except:
	print("删除错误")
```

## 批量删除

通常不会轻易在业务里把数据真正的删除，取而代之的是伪删除，即在表中添加一个布尔型的字段  is_active  ,默认是True；执行删除时，将欲删的数据的  is_active  字段置为False

注意： 用伪删除时，确保显示数据的地方，均加入了  is_active=True 的过滤查询

1. 查找查询结果集中满足条件的全部QuerySet查询集合对象
2. 调用查询集合对象的delete()方法实现删除

```python
author = Author.objects.filter(age__gt=65)
author.delete()
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2035.png)

   

## F对象

1. 一个F对象代表数据库中某条记录的字段的信息（上锁）
2. 作用 通常是对数据库中的字段值在不获取的情况下进行操作，用于类属性（字段）之间的比较
3. 语法

```python
from django.db.models import F
f('列名')
```

查找 market_price大于 price 的数据

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2036.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2037.png)

## Q对象

1. 当在获取查询结果集 使用复杂的逻辑或  |  逻辑 非  ~   等操作时可以借助Q对象 进行操作
2. 语法

```python
from django.db.models import Q
	Q(条件1)|Q(条件2)   #条件一或条件2
	Q(条件1)&Q(条件2)   #条件一且条件2
	Q(条件1)&~Q(条件2)  #条件一成立且条件2不成立
```

```python
from django.db.models import Q
	Q(条件1)|Q(条件2)
	
```

1. 如  想找出定价低于20元  或者 清华大学出版社的全部书籍，可以这么写

```python
Book.objects.filter(Q(price__lt=20)|Q(pub="清华大学出版社"))
```

F，Q对象在数据包 django.db.models 中 需要先导入 才可以使用

  

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2038.png)

## 聚合查询和原生数据库操作

### 聚合查询

1. 聚合查询指的是对一个数据表中的一个字段的数据进行部分或全部进行统计查询，查bookstore_book数据表中的全部书的平均价格，查询所有书的总个数等，都要使用聚合查询
2. 聚合查询分为 整表查询和分组查询

不带分组的聚合查询是指将全部数据进行集中统计查询

聚合函数导入  

```python
from django.db.models import *  （Sum , Avg , Count , Max ,Min）
#聚合函数   Sum , Avg , Count , Max ,Min
#语法
#mymodels.objects.aggregate(结果变量名=聚合函数（‘列’）)
# 返回结果：结果变量名和值组成的字典
# 格式：{“结果变量名”：值}
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2039.png)

### 分组聚合（先选出来一部分再聚合）

分组聚合是指通过计算查询结果中的每一个对象所关联的对象的集合，从而得出总价值（也可以是平均值或总和），即为查询集的每一项生成聚合

```python
#语法
QuerySet.annotate(结果变量名=聚合函数(‘列’))
#返回值
QuerySet
```

先按照 pub 查出数据  然后 对查询结果 分组查询 然后再查看聚合结果大于一的

触发 having

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2040.png)

## 原生数据库操作（你觉得自己MySQL比较好，可以用）

- 查询 ： 使用mymodels.objects.raw()进行数据库查询操作
- 语法 ： mymodels.objects.raw(sql语句，拼接参数)
- 返回值 : RawQuerySet 集合队形（RawQuerySet 只支持基础操作，比如循环）

```python
books = models.Book.objects.raw('select * from book')

for i in books:
	print(i)
```

## django 不推荐使用原生SQL语句操作

使用原生语句时校新sql注入 （所谓sql注入 就是指用户通过数据上传，将恶意的sql语句提价给服务器，从而达到攻击的效果）

案例1：用户在搜索好友的表单框里 输入 ‘1 or 1 = 1’

```python
s1 = Book.objects.raw('select * from book where id=%s'%('1 or 1=1'))
# 攻击结果 ： 可以查询出所有的用户数据
```

 

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2041.png)

 

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2042.png)

## sql注入防范

```python
#错误
#相当于 id = 1 or 1=1(or生效 or 1=1) 
s1 = Book.objects.raw('select * from book where id=%s' %('1 or 1=1'))
#相当于 id = '1 or 1=1'(or不会执行)mysql 找到第一个 int值 就不在往下看
#正确
s2 = Book.objects.raw('select * from book where id=%s',['1 or 1=1'])
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2043.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2044.png)

## 完全跨过模型类操作数据库—（查询，更新，删除）

1. 导入cursor所在的包（使用游标）
    1. from django.db import connection
2. 用创建的 cursor 类的构造函数创建cursor对象，在使用cursor 对象，为保证再出现异常情况时能释放cursor资源，通常使用with语句进行创建操作

```python
from django.db import connection
with connection.cursor() as cur:
		cur.execute('执行sql语句','拼接参数')
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2045.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2046.png)

## Django自带的admin后台管理

- diango提供了比较完善的后台管理数据库的接口，可控开发过程中调用和测试使用
- diango会搜集所有已注册的模型类，为这些模型类提供数据管理界面，供开发者使用
- 创建后台管理账号—该账号是管理后台最高权限账号  (超级账号可以创建多个)
    - 
    
    ```python
    python manage.py createsuperuser
    ```
    

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2047.png)

### 如何将自定义的模型类添加到/admin后台中显示和管理

需要将自己的类注册到后台管理界面

注册步骤：

1. 在应用app中的admin.py中导入注册要管理的模型models类,比如：from.models import Book
2. 调用 admin.site.regester 方法进行注册，比如：admin.site.regester(自定义模型类)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2048.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2049.png)

admin后台很明显跟我们定义的  __str__   类是一样的（这样显示很粗糙）

所以我们需要引入 模型管理器类

### 模型管理器类

- 作用：为后台管理界面添加便于操作的新功能
- 说明： 后台管理器类必须继承自 django.contrib.admin里的ModelAdmin
- 使用方法
    - 在<应用app>/admin.py里定义模型类管理器类
    - 
    
    ```python
    # 必须继承于 ModelAdmin
    Class XXXmanager(admin.ModelAdmin):
    		....................（可以写一些类属性）
    ```
    
    - 绑定注册模型管理器和模型类
    - 
    
    ```python
    from django.contrib import admin
    from .models import YYYY
    #   绑定  YYYY 模型类与管理器类XXXmanager
    admin.site.regester(YYYY,XXXmanager) 
    ```
    

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2050.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2051.png)

### 过滤器

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2052.png)

### 设置 admin 后台表名

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2053.png)

## MySQL关系映射

### 什么是关系映射

- 在关系型数据库中，通常不会把所有数据放在同一张表中，不易于拓展，常见的关系映射有：
1. 一对一映射
    1. 如一个身份证号对应一个人，一个人一个指纹信息，一个家庭一个户主
    2. 一对一是表示现实事物间存在的一对一的对应关系
    3. 语法：OneToOneField（类名，on_delete = xxx）on_delete 是级联删除的规则   级联删除就是 表与表之间建立关系之后 如果一个表中的信息删除 另一个表如何操作（django 2 才加入级联删除）
        1. 级联删除 的值
            1. models.CASCADE  级联删除。（共生死）django模拟SQL约束on delete CASCADE的行为，并删除ForeignKey的对象（删除与之关联的外键的对象）这种是django模拟出来的 并不是直接设置的mysql 。
            2. models.PROTECT抛出ProtectedError 以阻止被引用对象的删除；（等同于mysql默认的PESTRICT）
            3. SET_NULL  设置ForeignKey null；需要指定null=True（就是我让你删但是我的外键指向null）
            4. SET_DEFAULT 将ForeginKey设置为ForeignKey的默认值。（就是我让你删，我的外键指向默认值）
            5. 
    4. 
    
    ```python
    class A(model.Model):
    		...........
    class B(model.Model):
    		属性 = models.OneToOneField(A,on_delete=xxx)
    ```
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2054.png)
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2055.png)
    
    e. 一对一 创建数据
    
    - 无外键的模型1类[Author]：
        
        author1= Author.objects.create(name='王老师')
        
    - 有外键的模型类[Wife]
        
        wife1 = Wife.objects.create(name='王夫人'，author=author1) # 关联王老师obj
        
        wife1 = Wife.objects.create(name='王夫人'，author_id=1)#关联王老师对应的主键值
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2056.png)
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2057.png)
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2058.png)
        
    
    ### 一对一 查询数据
    
    1. 正向查询：直接通过外键属性查询，则称为正向查询
        
        ```python
        # 通过wife找author
        from .models import Wife
        wife = Wife.models.get(name='王夫人')
        print(wife.name,'的老公是',wife.author.name)
        ```
        
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2059.png)
    
    1. 反向查询 ：没有外键属性的一方，可以调用反向属性查询到关联的另一方，反向关联的属性为‘实例对象.引用类名（小写）’，如作家的反向引用为‘作家对象.wife’;   当反向引用不存在时，则会触发异常
    
    ```python
    author1 = Author.obbjects.get(name='王老师')
    # 实际上我没并没有给 是  djang  送的
    author1.wife.name  
    ```
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2060.png)
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2061.png)
    
2. 一对多
    1. 如一个班级对应全班学生（开发中很常见）
    2. 一对多要区分出具体的角色，在多表上设置外键
    3. 语法：当A类对象可以关联多个B类对象时（先创建一在创建多）
        
        ```python
        class A(model.Model):
        		.........
        # ForeignKey必须指定on_delete模式
        class B(model.Model):
        		属性 = models.ForeginKey("一"的模型类,on_delete=xx)
        ```
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2062.png)
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2063.png)
        
    4. 正向查询[通过book查询出版社publisher]
        
        ```python
        abook = Book.objects.get(id=1)
        print(abook.name,'的出版社：',abook.publisher.publisher)
        ```
        
    5. 反向查询  [ 通过publisher查询 对应的所有 book]  需要用到 反向属性
        
        ```python
        # 通过出版社1查询对应的书
        pub1 = publisher.objects.get(name='清华大学出版社')
        # 通过book_set获取pub1对应的多个book数据对象
        	# 不仅可以.all()  还可以  .filter 那些因为都是多个queryset查询
        books = pub1.book_set.all()
        # 也可以这样获取
        #books = Book.objects.filter(publisher=pub1)
        print("清华大学出版社的书有：")
        for i in books:
        		print(book.name)
        ```
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2064.png)
        
3. 多对多
    1. 如一个学生可以报多个课程，一个课程可以有多个学生学习
    2. 多对多表达的对象之间多对多复杂关系，如每个人都有不同的学校（小学，初中，高中，.....）,每个学校都有不同的学生.....
        1. mysql中创建多对多需要依赖第三张表来实现
        2. django中无需创建第三张表，django自动完成
    3. 语法：在关联的两个类中任意一个类中，增加：
        
        ```python
        属性 = models.ManyToManyField(MyModel)
        ```
        
    4. 多对多模型创建 
        1. 方案1 先创建 author 再关联 book
            
            ```python
            author1 = Author.objects.create(name='吕老师')
            author2 = Author.objects.create(name='李老师')
            #  李老师和吕老师同时写了一本 python
            book11 = author1.book_set.create(title='python')
            author2.book_set.add(book11)
            ```
            
        2. 方案2 先创建 book 再关联 author
            
            ```python
            book = Book.objects.create(title='python基础')
            # 郭小闹和吕老师 都参与了 python基础  的操作
            author3 = book.authros.create(name='郭小闹')
            book.authors.add(author1)
            ```
            
            ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2065.png)
            
            ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2066.png)
            

## Cookie和Session

1. http 的请求过程就是会话，我希望浏览器和服务器能够互相记住，就是会话保持。
2. 从打开浏览器访问一个网站，到关闭浏览器结束此次访问，称为一次会话
3. http协议是无状态的，导致会话难以保持，Cookies和Session 就是为了保持会话状态而诞生的两个储存技术
4. Cookies是保存在客户端浏览器上的存储空间  
    
    Chrome：Application→Storage→Cookies  查看和操作浏览器端所有的Cookie
    
    Firefox：存储→Cookies
    
5. Cookies 在浏览器上是以键值对的形式进行存储的，键和值都是以ASII字符的形式存储（不能是中文字符串）
6. 存储的数据带有生命周期 Expires/Max-Age :2022-11-23T10:41:13.036Z(一年过期)
7. cookies中的数据是按域（域名）存储隔离的，不同的域之间无法访问
8. cookies的内部的数据会在每次访问此网址时都会携带到服务器端，如果cookies过大会降低响应速度。
9. cookies的使用
    
    ```python
    HttpResopnse.set_cookie(key,value='',max_age=None,expires=None)
    -key:cookie的名字
    -value:cookie的值
    -max_age:cookie存活的时间，单位为秒
    -expires:具体的过期时间
    -当不指定max_age和expires时，关闭浏览器时此数据失效
    
    # 添加cookie
    responds = HttpResopnse('添加 cookie1，值为123')
    responds.set_cookie('cookie1', 123, 3600)
    return resopnds
    
    #修改cookie
    responds = HttpResopnse('已修改 cookie1，值为456')
    responds.set_cookie('cookie1', 456, 3600)
    return resopnds
    
    # 删除session  注意区分 删除 cookie 和  session
        if 'username' in request.session:
            del request.session['username']
        if 'uid' in request.session:
            del request.session['uid']
    
    #删除cookies
    HttpResopnse.delete_cookie(key)
    # 删除指定的key的cookie 如果key不存在则什么也不发生
    # 获取cookies通过request.COOKIES绑定的字典dict获取客户端的COOKIES数据
    value = request.COOKIES.get('cookies名'，'默认值')
    #删除cookie
    		if 'username' in request.COOKIES:
            res.delete_cookie('username')
        if 'uid' in request.COOKIES:
            res.delete_cookie('uid')
        return res
    ```
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2067.png)
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2068.png)
    

## session

1. 类似于超市存包（浏览器把sessionID存在cookie里）
2. session是在服务器上开辟一段空间用于保留浏览器和服务器交互时的重要数据
3. 实现方式
    1. 使用session需要在浏览器客户端启动cookie，且在cookie中存储sessionid
    2. 每个客户端都可以在服务器端有一个独立的session（注意：不同的请求者之间不会共享这个数据，与请求者一一对应）
4. session 初始配置
    1. 在setting.py中配置session，向INSTALLED_APPS列表中添加：
        
        ```python
        INSTALLED_APPS = [
        			#启用 session 应用
        			'django.contrib.session',
        ]
        ```
        
    2. 向MIDDLEWARE列表中添加
        
        ```python
        MIDDLEWARE = [
        		#  启用session中间件
        		'django.contrib.session.middleware.SessionMiddleware'
        ]
        ```
        
5. session对于对象是一个类似于字典的SessionStore类型的对象，可以用类似于字典的方式进行操作，session  能够存储诸如字符串，整型，字典，列表等。
    1. 保存session的值到服务器  request.session['KEY'] = VALUE
    2. 获取session的值  
        1. value = request.session['KEY']
        2. value = request.session.get('KEY',默认值)
    3. 删除session del request.session['KEY']
    4. 因为  服务器返回的sessionid 是保存在cookie里面的因为cookie是有时效性的所以session也可以认为是有时效性的
    5. SESSION_COOKIE_AGE
        1. 作用：指定session在cookies中的保存时常（默认是2周），如下：例如SESSION_COOKIE_AGE=60*60*24*7*2
        2. SESSION_EXPIRE_AT_BROWSER_CLOSE=True
            
            设置只要浏览器关闭时，session就失效（默认是False）
            
        
        注意：Django中的sesion数据存储在数据库中，所以使用session前需要确保已经执行过migrate（数据库中django默认给出的django_session）
        
    6. django session的问题
        1. django_session表是单表设计；且该表数据量持续增持[浏览器故意删掉sessionid&过期数据未删除]
        2. 可以每晚执行python [manage.py](http://manage.py) clearsessions [该命令可以删除已过期的session数据]
    7. cookie 和  session对比  相对来说 cookie不安全 session更安全（除非可以进入数据库） 

## 阶段性项目 云笔记

       基本功能，用户可以在该系统中记录自己的日常学习/旅游/笔记,用户的数据将被安全的存储在云笔记平台，用户与用户之间数据为隔离存储（用户只有在登陆后才能使用相关笔记功能，且自己只能查询自己的笔记内容）

一般，项目组成员角色

- 产品/运营经理：负责产品功能细节的把控
- 开发
    - 前端—负责显示部分内容的开发
    - 后端—负责服务器部分的功能开发
- 运维：管理linux服务器，组件化配置，安全问题
- 测试：负责找出产品的问题（BUG）
- 美术：负责产品素材方面的绘制

### 功能拆解

- 用户模块
    - 注册 — 成为平台用户
    - 登录 — 校验用户身份
    - 退出登录 — 退出登陆状态
- 笔记模块
    - 查看笔记列表 — 查
    - 创建新笔记 — 增
    - 修改笔记 — 改
    - 删除笔记 — 删

## 用户模型类设计

 用户模型类包含参数：用户名  密码  用户创建时间   更新时间  

```python
class User(models.Model):
    # unique  保证用户名独一无二
    username = models.CharField('用户名', max_length=30, unique=True)
    password = models.CharField('密码', max_length=32)
    # auto_now无论是你添加还是修改对象，时间为你添加或者修改的时间。
    # auto_now_add为添加时的时间，更新对象时不会有变动。
    create_time = models.DateTimeField('创建时间', auto_now_add=True)
    update_time = models.DateTimeField('更新时间', auto_now=True)

    def __str__(self): 
        return '用户名' % self.username
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2069.png)

### 用户注册

- url:/user/reg
- 视图函数：reg_view
- 模板位置：template/user/register.html

这里注意下两个经典报错

[1.post](http://1.post) url 需要以 /   结尾

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2070.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2071.png)

还有就是 post 获取信息 是字典的形式 用[]

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2072.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2073.png)

注册部分

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2074.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2075.png)

### 密码处理？

  哈希加密 给定明文，计算出一段定长的不可逆的值，md5，sha-256

1. 定长输出，不管明文长度是多长，哈希值都是定长的，md5 - 32位16进制
2. 不可逆 无法反向计算出对应的明文
3. 雪崩效应，输入改变，输出必然变

哈希算法应用场景：1.密码处理  2.文件完整性校验

### python如何使用哈希

```python
# 常规算法都有
import hashlib
m = hashlib.md5()
m.update(b'123456')# 参数必须是字节串
# 获取16进制结果
m.hexdigest()
# 如果你想再计算一个123 不能 使用m.update(b'123')
# 这样计算的结果是 123456123 因为 是update
h = hashlib.md5()
h.update(b'123456123')
# 获取16进制带有不可视字符摘要
h.digest()
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2076.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2077.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2078.png)

### 插入问题

creatuser有问题：核心问题就是 username 是有unique 唯一 假设多台服务器，有多个人同一时间设置同一个用户名，哪一个用户的语句最快到达sql语句，谁可以设置成功，否则唯一索引报错

解决办法 try 以下（唯一索引的地方都要 try）

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2079.png)

### 产品经理要求 注册 则免登录 一天，这个功能怎么做

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2080.png)

## 用户登录

1. url:/user/login
2. 视图函数：login_view
3. 模板位置：templates/user/login.html

![QQ图片20211125210102.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/QQ%E5%9B%BE%E7%89%8720211125210102.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2081.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2082.png)

搞一个首页 如果已经登陆过就跳转到首页，不然就跳转到登陆界面

1. 优先检查session 如果session有效跳转到 首页，
2. 如果session没有数据 ，再检查cookie cookie有数据就再次存储cookie，ruguocookie没有数据就跳转到login

### 网站首页

- url: /index
- 视图函数：index_view
- 模板位置：template/index/index.html
- 界面样式：没有登陆就显示登录和注册  登陆后就显示 欢迎进入我的笔记
    
    变量相关的用`{{}}`，逻辑相关的用`{%%}`
    

## 笔记内容 模型类

### 查看笔记

- urls : /note/all
- 视图函数 ： list_all
- 模板位置：template/note/list_note.html

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2083.png)

注意 严格来说在笔记模块的任何一个地方 都应该校验登陆状态。

orm操作保存的时间 是 utc 的 不是 设置的 Asia/Shanghai,在模板上调用时间是你seetting设置的，但是在MySQL里面看还是 utc

### 添加笔记

- url: /note/add
- 视图函数 ： add_view
- 模板位置： template/note/add_note.html

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2084.png)

 用[python装饰器](https://www.notion.so/Python-0686d38c3398427e9fb46365d7489d70)来解决登陆验证问题

核心在于如何灵活校验登陆状态

note_view code

```python
from django.shortcuts import render
from django.http import HttpResponse, HttpResponseRedirect
from .models import Note
# Create your views here.

# fun就是视图函数
def check_login(fun):
    # * 用于传入的多个参数将按照元组形式存储，是一个元组。
    # ** 用于参数前则表示传入的（多个）参数将按照字典的形式存储，是一个字典。
    def wrap(request, *args, **kwargs):
        # 检查登录状态
        if 'username' not in request.session or 'uid' not in request.session:
            # 检查完session 检查 cookie
            c_username = request.COOKIES.get('username')
            c_uid = request.COOKIES.get('uid')
            if not c_username or not c_uid:
                # 这里必须是相对地址
                return HttpResponseRedirect('/user/login')
            else:
                # 回写 cookie
                request.COOKIES['username'] = c_username
                request.COOKIES['uid'] = c_uid
        return fun(request, *args, **kwargs)
    return wrap

@check_login
def add_note(request):
    if request.method == 'GET':
        return render(request, 'note/add_note.html')
    elif request.method == 'POST':
        # 处理数据
        uid = request.session['uid']
        title = request.POST['title']
        content = request.POST['content']
        # 记得指定外键
        Note.objects.create(title=title, content=content, user_id=uid)

        return HttpResponse("<script>alert('记录成功')</script>")
```

note_models 模型文件

```python
from django.db import models
from user.models import User

# Create your models here.

class Note(models.Model):
    title = models.CharField('标题', max_length=100)
    content = models.TextField('内容')
    create_time = models.DateTimeField('创建时间', auto_now_add=True)
    update_time = models.DateTimeField('修改时间', auto_now=True)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```

note_urls

```python
from django.urls import path
from .views import add_note

urlpatterns = [
    path('add_note/', add_note),
]
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2085.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2086.png)

## 缓存：（缓存是服务器优化的重要方式）

- 定义：缓存是一类可以更快的读取数据的介质 统称，也指其他可以加快数据读取的存储方式，一般用来存储临时数据，常用介质是读取速度很快的内存
- 意义：视图渲染有一定成本，数据库的频繁查询过高，所以对于低频变动的页面可以考虑使用缓存技术，减少实际渲染次数，用户拿到的响应时间成本会更低
- 案例分析

```python
from diango.shoortcuts import render
def index(request):
		#时间复杂度极高的渲染
		book_list = Book.objects.all()  #->假设此处耗时2s(浏览器卡住两秒)
		return render(request, 'index.html', locals())
```

- 优化思想 - 官网(查询的页面首先从缓存里面查找，看缓存里有没有，如果没有，保存一份到缓存留到下一次用，具有时效性)
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2087.png)
    
- 缓存场景  场景特点：缓存的地方，数据变动频率小
    - 博客列表页（首页著名文章放缓村里）
    - 电商商品详情页（关于某一商品的信息）

## Django中设置缓存 - 数据库缓存

1. 将缓存的数据存储在您的数据库中
    
    说明：尽管储存介质没有更换，但是当把一次负责查询的结果直接存储在表里，比如多个条件的过滤查询结果，可以避免重复进行复杂的查询，提升效率；
    
    ```python
    CACHES = {
        'default': {
            'BACKEND': 'django.core.cache.backends.db.DatabaseCache',
            'LOCATION': 'my_cache_table',
            # 缓存保存的时间单位是秒，默认值为300
            'TIMEOUT': 300,
            'OPTIONS': {
                # 缓存最大的条数
                'MAX_ENTRIES': 300,
                # 缓存条数达到最大值时，删除1/x 的缓存数据
                'CULL_FREQUENCY': 2,
            }
        }
    }
    ```
    
2. Django中设置缓存 - 本地内存缓存（放到内存中,一般都是存到内存性的数据库里面  redis）
    
    ```python
    CASHES={
    			'defalut':{
    					'BACKEND':'django.core.cache.backends.locmem.LocMemCache',
    					'LOCATION':'unique-snowflake',  # 缓存地址  使用的雪花算法
    								}
    				}
    ```
    
3. Django中设置缓存 - 文件系统缓存 (将缓存的数据存储到本地文件,不推荐使用)
    
    ```python
    CASHES={
    			'defalut':{
    					'BACKEND':'django.core.cache.backends.filedbased.FileBasedCache',
    					'LOCATION':'/var/tmp/django_cache',  # 这个是文件夹的路径
    					#'LOCATION':'c:\test\cache',  # 这个是windows下的文件夹的路径
    								}
    				}
    ```
    

以第一种缓存的数据存储在您的数据库中为例

完成setting设置以后，记得通过 python [manage.py](http://manage.py/) createcachetable 将缓存表新建

### 整体缓存

整体缓存，把响应一股脑的放到缓存里，比如一个大页面，把整个页面全部存进缓存里，下次查询直接返回整个页面，

- django中使用缓存 — 视图函数中
    
    ```python
    from diango.view.decorators.cache import cache_page
    
    @cache_page(30)  #->  单位秒缓存保存时间
    #现在装饰器里面查看是不是存在缓存 如果存在就直接返回就行了，如果没有就
    #正常执行视图函数 并且保存缓存进入 数据库
    def my_view(request):
    .........
    ```
    
- django中使用缓存 — 路由里面
    
    ```python
    from django.views.decorators.cache import cache_page
    
    urlpatterns = [
    		# 在路由里面很方便 
    		path('foo/', cache_page(60)(my_view)),
    
    ]
    ```
    

```python
# 整体缓存
import time
from django.http import HttpResponse
from django.views.decorators.cache import cache_page

# 缓存15秒
@cache_page(15)
def test_cache(request):
    t = time.time()
    print('时间是：%s' % t)
    return HttpResponse('时间是：%s' % t)
```

在设置的15秒内，走的都是，缓存，时间过了才会重新获取

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2088.png)

## 局部缓存

相对于整体缓存策略，局部缓存可复用性更高，更加灵活，像缓存哪一部分就缓存哪一部分

比如下面这个案例

- 整体缓存的时候，会先通过装饰器的逻辑，只有通过了装饰器的逻辑，才会执行视图函数，这就对导致整体缓存最后的结果是return部分，而且对于视图函数创造的缓存无法干预，没有办法操作，使用起来简单除暴，但是可操作性不高
- 比如 假设我们只需要缓存  book_list  部分 整体缓存就无可奈何，而且其他视图函数调用book_list 也可以使用缓存，就会很nice

```python
from django.shortcuts import render

def index (request)
		#  时间复杂度极高的渲染
		book_list = Book.objects.all()   # -> 此处假设耗时2s
		return render (request, 'index.html', locals())
```

### 局部缓存的使用

1. 缓存api的使用
    
    先引入cache对象
    
    1. 方式一：使用caches['CASHE配置key']导入具体对象
        
        ```python
        # 假设setting 设置里面的 CACHE 不止 dafault 一项
        from django.core.cache import cache
        cache1 = cache['default']    # 跟下面的效果一样
        cache2 = cache['myalias_2']
        ```
        
    2. 方式二：
        
        ```python
        
        # 相当于直接导入 CACHE配置项中的default
        from django.core.cache import cache 
        ```
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2089.png)
        
2. 缓存api的使用
    1. cache.set(key,value,timeout) - 存储缓存 、
        
        key ： 缓存的key，字符串类型
        
        value ：Python对象
        
        timeout : 缓存存储的时间，默认为CACHE中的TIMEOUT值
        
        返回值 ：NONE
        
    2. cache.get(key) - 获取缓存
        
        key ： 之前缓存的key
        
        返回值：为key的具体值，如果没有数据，则返回None
        
    3. cache.add(key,value) - 存储缓存，只在key不存在时生效
        
        返回值：True[存储成功] or False[存储失败]
        
    4. cache.get_or_set(key,value,timeout) - 如果未获取到数据，则执行set操作，返回值value
    5. cache.set_many(dict,timeout)  -  批量存储缓存
        
        dict:key和value的字典
        
        timeout：存贮时间（s）
        
        返回值：插入不成功的key的数组
        
    6. cache.get_many(key_list)  -  批量获取缓存数据
        
        key_list：包含key的数组
        
        返回值：取到key和value的字典
        
    7. cache.delets(key)  -  删除key的缓存数据
        
        返回值：NONE
        
    8. cache.delete_many(key_list) - 批量删除
        
        返回值：NONE
        
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2090.png)
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2091.png)
    

## 浏览器缓存策略

浏览器也具备缓存技术，对于浏览器来说，每次向服务器发出请求都是耗时的操作，如果本身浏览器内部就具备当前url的内容，则一定时间内可以不必给服务器发送请求，从而提升用户体验，降低服务器请求的压力。

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2092.png)

### 浏览器缓存 —— 强缓存

不会像服务器发送请求，直接在缓存中读取资源

1. 响应头 - Expires（绝对时间）http1.0
    
    定义：缓存过期时间，用来指定缓存资源的到期时间，是服务器的具体的时间点
    
    样例：Expires ：Thu，02 Apr 2030 05：14：08 GMT
    
2. 响应头 - Cache - Control（相对时间）http1.1
    
    在HTTP/1.1中，Cache-Control 主要用于控制网页缓存，比如当‘Cache-Contrl：max-age=120’ 代表请求创建时间后120秒，缓存失效
    
    说明：目前浏览器都会带着这两个头同时相应给浏览器，浏览器优先使用Cache-Control
    

以上这两个响应头 都是 Django 装饰器 `@cache_page`  自动添加的

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2093.png)

### 浏览器缓存 —— 协商缓存

强缓存中的数据一旦过期，还需要跟服务器进行通信，从而更新数据；

思考：如果强缓存缓存的数据是一些静态文件，大图片等；

解答：考虑到大图片这类比较耗费贷款且不易变化的数据，强缓存时间到期后，浏览器会跟服务器协商，当前缓存是否可用，如果可用，服务器不必返回数据，浏览器继续使用原来的缓存的数据，如果文件不可用，则返回最新的数据

### 协商缓存 - 响应头

1. Last-Modified响应头和  if-Modified-Since请求头 
    
    说明：Last-Modified 为文件的最近修改时间，浏览器第一次请求静态文件时，服务器如果返回Last-Modified 响应头，则代表该资源为需协商的缓存。
    
    当缓存到期后，浏览器将取到的Lat-Modified值作为请求头if-Modified-Since的值，与服务器请求协商，服务器返回304响应码[响应体为空]，代表缓存继续使用，200响应码代表缓存不可用[响应体为最新资源
    
    注：Last-Modified 并不是最优解，http协议新加了 ETag响应头和if-None-Match 请求头（因为Last-Modified 依靠时间判断是否过期 不太严谨；，比如一秒内代码发生了变化就不能识别出来，最准确的就是 利用hash算法，hash校验看一下文件是否发生变化]）
    
2. ETag响应头和if-None-Match请求头（缺点：浪费计算资源 每次都要计算hash）
    
    说明：ETag是服务器请求时，返回当前资源文件的一个唯一标识（由服务器生成），只要资源有变化，ETag就会重新生成
    
    缓存到期后，浏览器将ETag响应头的值，作为if-None-Match请求头的值，给服务器发送请求协商；服务器接到请求头后，对比文件表示，不一致则认为资源不可用，返回200响应码[响应体为最新资源]；可用则返回304响应码
    

PS：如果同时存在 Last-Modified 和 ETag  浏览器认准 ETag， 浏览器永远只认最新的东西。

## 中间件 （可用于反扒）

- 中间件是Django请求/响应处理的钩子框架。他是一个轻量级的，低级的插件系统，用于全局改变Django的输入或输出
- 中间件以类的形式体现
- 每个中间件组件负责做一些特定的功能，例如Django包含一个中间件组件AuthenticationMiddleware，它使用会话将用户与请求关联起来
- 中间件类需继承来自 django.utils.deprecation.MiddlewareMixin类
- 中间件类须实现下列五个方法中的一个或多个：
    - process_request(self，request)
        
        执行路由之前被调用，在每个请求上调用，返回None或HttpResponse对象，返回none代表继续往下执行.
        
    - process_view(self,request,callback,callback_args,callback_kwargs)
        
        调用试图之前被调用，在每个请求上的调用，返回None或HttpResponse对象
        
    - process_response(self,request,resopnse)
        
        所有响应返回浏览器被调用，在每个请求上调用，返回HttpResponse对象
        
    - process_exception(self,request,exception)（抓异常 返回邮件）
        
        当处理过程中抛出异常时调用，返回一个HttpResponse对象
        
    - process_template_response(self,request,resopnse)（不经常用比较高级）
        
        在视图函数执行完毕且试图返回的对象中包含render方法时被调用；该方法需要返回实现了render方法的响应对象
        
        Ps: 中间件中的大多数方法在返回None时表示忽略当前操作进入下一项事件，当返回HttpResponse对象时表示请求结束，直接返回给客户端。
        

## 中间件的使用（参照生命周期函数）

要想使用中间件首先，我们需要在 [setting.py](http://setting.py) 里面注册，MIDDLEWARE

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
    # 注册中间件
    'middleware.mymiddleware.MyMW',
]
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2094.png)

```python
from django.utils.deprecation import MiddlewareMixin

class MyMW(MiddlewareMixin):

    def process_request(self, request):

        print('MyMW process_request do ---')

    def process_view(self, request, callback, callback_agrs, callback_kwargs):

        print('MyMW process_view do ---')

    def process_response(self, request, response):

        print('MyMW process_view do ---')
        return response
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2095.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2096.png)

可以在下图看到，中间件执行的过程，类似于vue生命周期函数

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2097.png)

### 中间件的执行顺序

类似与栈先进后出，在进入视图函数之前先执行注册在上方的，中间件，在退出视图函数时，后注册的中间件先执行

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2098.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%2099.png)

以下是比较简单的解决办法，最好是使用数据库存储，访问次数

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20100.png)

![1426850-20181015213224012-1563676825.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/1426850-20181015213224012-1563676825.png)

![1426850-20181015213614470-941854817.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/1426850-20181015213614470-941854817.png)

![1426850-20181015214134505-2039072515.png](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/1426850-20181015214134505-2039072515.png)

上图是非常经典的django流程细节

## CSRF 攻击(跨站请求伪造攻击)

某些恶意网站上包含连接i，表单按钮或者javascript，他们会利用登陆过的用户在浏览器中的认证信息试图在你的网站上完成某些操作，这就是跨站请求伪造（csrf 即 cross-site Request Forgey）。

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20101.png)

- django采用‘对比暗号’机制防范攻击
- cookies中储存暗号1，模板中表单里藏着暗号2，用户只有在本网站下提交数据，暗号2才会随着表单提交给服务器，django对比两个暗号，对比成功，则认为是合法请求，否则是违法请求，403响应码
    
    ### 配置步骤：
    
    1. seeting.py中确认MIDDLEWARE中  django.middleware.csrf.CsrfViewMiddleware 是否打开
    2. 模板中，form标签下添加标签  {  % csrf_token% }
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20102.png)
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20103.png)
        
        在模板加上 {%csrf_token%}
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20104.png)
        
        ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20105.png)
        
    
    ps：如果某个页面不需要django进行csrf保护，可以用装饰器关闭对此视图的检查
    
    ```python
    from django.views.decorators.csrf import csrf_exempt
    
    @csrf_exempt
    def my_view(request)
    		return HttpResponse('hello')
    ```
    

## 分页

- 分页是指在web页面有大量数据需要显示，为了阅读方便在每个页面只显示部分数据
- 优点：
    - 方便阅读
    - 减少数据提取量，减轻服务器压力。
    - django提供了Paginator类可以方便的实现分页功能
    - Paginator类位于‘django.core.paginator’
    
    （暂时没搞）
    

## 生成CSV文件

逗号分隔值（comma-separated Vlues，CSV，有时也称为符号分隔值，因为分隔字符也可以不是逗号），其文件以纯文本形式储存表格数据（数字和文本）

说明：可被常见制表工具，如excel等直接进行读取

python提供了内建库 - csv 可直接通过该库操作csv文件

```python
import csv
# open生成csv文件 需要添加newline = ''  newline='' 意思是不会转义字符
with open('eggs.csv','w',newline='') as csvfile:
			writer = csv.write(csvfile)
			writer.writerow(['a','b','c'])
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20106.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20107.png)

在网站中，实现下载csv，注意以下

- 响应content-type类型需修改为test/csv。这告诉浏览器该文档是csv文件，而不是html文件
- 相应会获得一个额外的Conten-Disposition标头，其中包含csv文件的名称，他将被浏览器用于开启‘另存为。。。。’对话框

### csv文件下载

```python
def test_csv(request):
    response = HttpResponse(content_type='text/csv')
    response['Content-Disposition'] = 'attachment;filename="test_csv.csv"'
    all_data = ['1',  '2', '3', '4', '5']
    writer = csv.writer(response)
    writer.writerow(all_data)
    return response
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20108.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20109.png)

## 内建用户系统 admin后台

- django带有一个用户认证系统，他处理用户账号，组，权限以及基于cookie的用户会话
- 用户可以直接使用django自带的用户表

模型类位置 from django.contrib.auth.models import User

username  用户名

password  密码

email    邮箱

first_name  名

lact_name   姓

is_superuser 是否是管理员账号（/admin）

is_staff 是否可以访问admin管理界面（区分外部和内部用户）

is_active 是否是活跃用户，默认是True，一般不删除用户，而是将用户的is_active设为False

last_login 上次登录时间

date_joined 用户创建的时间

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20110.png)

创建普通用户create_user  django会帮你加密

```python
from django.contrib.auth.models import User
user = User.objects.create_user(username='用户名')
password = '密码'，email='邮箱',.......
```

创建超级用户create_superuser

```python
from django.contrib.auth.models import User
user = User.objects.create_superuser(username='用户名',password='密码'
，email='邮箱', .....)
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20111.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20112.png)

删除用户 建议伪删除

```python
from django.contrib.auth.models import User
try:
	user = User.objects.get(username='用户名')
	user.isactive = False
	user.save()
	print('删除成功')
expect:
	print('删除失败')
```

因为这种方式 密码加密是django完成的，所以我们不知道django的加密方式，没办法校验密码；django给我们了一个方法可以校验密码

```python
# 密码校验
from django.contrib.auth import authenticate
user = authenticate(username='用户名',password='password')
说明： 如果用户名密码校验成功则返回对应的user对象，否则返回None
```

修改密码同理

```python
# 修改密码
from django.contrib.auth.models import User
try:
	user =User.objects.get(username='用户名')
	user.set_password('123456')
	user.save()
	return HttpResponse('修改密码成功')
	return HttpResponse('修改密码失败')
```

登陆状态保持

```python
from django.contrib.auth import login
def login_view(request):
	user = authenticate(username='用户名',password='password')
	login(request,user)
```

登陆状态校验

```python
from django.contrib.auth.decorators import login_required

@login_required
def index_view(request):
	#该视图必须为用户登录状态下才可以访问
	#当前登录用户可通过request.user获取

	login_user =  request.user
```

但是当用户表字段不够怎么办？比如想添加手机号字段？

1. 方案一 ：通过建立新表，跟内建表做一对一
2. 方案二 ：继承内建表抽象user模型类(新建一个表，并且必须是在没有执行migrate 迁移之前，否则不行，保证当前数据库内没有表)
    
    步骤：
    
    1. 添加新的应用
    2. 定义模型类 继承AbstractUser
    3. settings.py中指明 AUTH_USER_MODEL='应用名.类名'
    
    ```python
    from django.db oimport models
    from django.contrib.auth.models import AbstractUser
    
    class UserInfo(AbstractUser):
    		# 其余的内容不用新建 会继承过来
    		phone = model.CharFiled(max_length=11, default='')
    ```
    
    seetings.py添加配置
    
    AUTH_USER_MODEL = 'user.UserInfo'(实际新建模型类名)
    
    接着就可以做数据库迁移 migrate
    
    生成的就是一个新表，使用给之前内嵌表一样
    

## 文件上传功能

用户通过浏览器将图片等文件上传至网站

场景

- 用户上传头像
- 上传流程性的文档[pdf,txt等]

文件上传时必须带有enctype = ”multipart/form-data“时才会包含文件内容数据；表单中用<input type='file' name='xxxx'>标签上传

后端，视图函数中，用request.FILES取文件筐的内容

file = request.FILES['XXX']

说明：

1. FILES的key对应页面中file框的name值
2. file绑定文件流对象
3. file.name文件名
4. file.file 文件的字节流数据

配置 文件的访问路径和存储路径

[在settings.py](http://在settings.py) 中设置MEDIA相关配置；Django把用户上传的文件统称为media资源

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

想让上面的配置生效，还需要在主路由里面配置

```python
from django.conf import settings
from django.conf.urls.static import static
urlpatterns += static(setting.MEDIA_URL,document_root=setting.MEDIA_ROOT)

说明：等价于做了MEDIA_URL开头的路由，django接到该特征请求后去MEDIA_ROOT路径查找资源

```

文件写入方案 ：传统的open方式

```python
@csrf_exempt  #csrf
def upload_view(request):
		if request.method == 'GET':
					return render(request, 'test_upload.html')
		elif request,method == 'POST':
					a_file = request.FILES['myfile']
					print('上传文件名是：', a_file.name)
					filename = os.path.join(settings.MEDIA_ROOT, a_file.name)
					with open(filename, 'wb') as f:
								data = a_file.file.read()
								f.write(data)
					return HttpResponse('接收文件',+a_fileename+'success')
```

文件写入方案2 ： 借助ORM

字段：FileFiled(upload='子目录名')

```python
@csrf_exempt
def upload_view_dj(request):
		if request.method == 'GET'
				return render(request, 'test_upload.html')
		elif request.method == 'POST':
				title = request.POST['title']
				a_file = request.FILES['myfile']
				Content.objects.create(desc=title,myfile=a_file)
				return HttpResponse('-----upload is ok------')
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20113.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20114.png)

Django会自动解决同名问题，自动重命名（加上一个随机的后缀）

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20115.png)

而且还可以通过浏览器地址，访问到上传的文件（没找到返回404）

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20116.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20117.png)

## Django发送邮件

### 业务场景

1. 业务警告（服务器出故障，自动发送错误信息）
2. 邮件验证
3. 密码找回

邮件相关协议 - SMTP

- SMTP全称是”Simple Mail Transfer Protocol“，即简单邮件传输协议（25端口）
- 他是一组用于从源地址到目的地址传输邮件的规范，通过他来控制邮件的中转（属于’推送‘协议，发邮件）

邮件相关协议 - IMAP

- IMAP全称是Internet Mail Access Protocol，即交互式邮件访问协议，他是一个应用层协议（端口是143）
- 用来从本地邮件客户端（Outlook Express，Foxmail， Mozilla Thunderbird等）访问远程服务器上的邮件
- 属于拉取协议（把服务器上的邮件拉取下来，clone）

邮件相关协议 - POP3

- POP3是Post Office Protocol 3 的简称，即邮局协议的第三个版本，是TCP/IPX协议族中的一种（默认端口是110）
- 本协议主要用于支持使用客户端远程管理在服务器上的电子邮件
- 同样也属于拉取协议

IMAP 与 POP3的区别

两者都是’拉取‘协议，负责人1从邮件服务器中下载邮件

- IMAP 具备摘要浏览功能，可预览部分摘要，再下载整个邮件
- IMAP为双向协议，客户端操作可以反馈给服务器（比如移动邮件，给邮件添加星标）
- POP3必须下载全部邮件，无摘要功能
- POP3为单项协议，客户端操作无法同步给服务器

邮件服务运作模式

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20118.png)

Django中配置邮件功能，主要为SMTP协议，负责发邮件

步骤：

- 给djano授权一个邮箱（以qq为例）
    - 拿到右相对应协议的授权码即可，即不需要登录就可以发送邮件
    - 
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20119.png)
    
    至于 EMAIL_USE_TLS 默认就是False 免费用户一般没有这个选项
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20120.png)
    
- django用该邮箱给对应收件人发送邮件
- django.core.mail 封装了电子邮件的自动发送SMTP协议

## 项目部署-uwsgi

1. 在安装机器上安装和配置同版本的环境[python，数据库等]
2. django项目迁移（放到服务器即可，各显神通，WinSCP）
3. 用uWSGI替代 python [manage.py](http://manage.py) runserver 方法启动服务器（runserver 性能不行只能测试使用，上线肯定不能用，所以用uWSGI）
    
    WSGI（web server gateway interface）web服务器网关接口，是python应用程序或框架和web服务器之间的一种接口，被广泛使用（python [manage.py](http://manage.py) runserver 通常只用于开发和测试环境中使用，当开发结束后，完善的代码需要在一个高效稳定的环境中运行，这时可以使用WSGI）
    
    django根本就不认识 http 协议，但是django认识wsgi，参见中间件图，但是runserver即认识http又认识wsgi 在http和django中起到翻译的作用。
    
    uWSGI是WSGI的一种，它实现了http协议WSGI协议以及uwsgi（小写）协议uWSGI功能完善，支持众多协议，在python web 圈热度极高，uWSGI以学习配置为主。
    
    uWSGI安装 pip install uWSGI == 2.0.18 -i
    
    检查是否安装  pip freeze | grep -i 'uwsgi'
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20121.png)
    
    ![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20122.png)
    
4. 配置nginx反向代理服务器（用于平衡请求）
5. 用nginx配置静态文件路径，解决静态路径问题

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20123.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20124.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20125.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20126.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20127.png)

不要重复启动uesgi ，在已启动状态下再次启动，会修改pid的值，就会报错

如下

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20128.png)

## 项目部署-Nginx

Nginx是轻量级的高性能web服务器，提供了诸如HTTP代理和反向代理，负载均衡等一系列重要特性，可以转发http或者uwsgi

C语言编写，执行效率高

Nginx作用：

- 负载均衡，多台服务器轮流处理请求
- 反向代理

原理：

客户端请求Nginx，再由Nginx将请求转发uWSGI运行的django

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20129.png)

配置完之后重启

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20130.png)

Nginx重启完成，需要修改uWSGI配置，

```python
[uwsgi]
# 去掉如下
# http=127.0.0.2:8000
# 改为
socket=127.0.0.1:8000
#
```

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20131.png)

同样 配置修改完成，uwsgi也需要重启，注意：访问的是80端口。

有问题，看日志。

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20132.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20133.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20134.png)

 

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20135.png)

### 自定义报错页面

返回自定义报错页面，在模板文件夹中添加404.html模板，当视图触发http404异常时将会被显示，404.html仅在发布版中即（settings.py中的DEBUG=false）时才起作用。

### 邮箱警告

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20136.png)

![Untitled](Django%E6%A1%86%E6%9E%B6%2056eccb4957ac44d5b6957df441ae6f23/Untitled%20137.png)