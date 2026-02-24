# 1 TypeError: unsupported operand type(s) for /: 'str' and 'str'
```shell
(venv) ai@pro:~/dev/xiaofu$ ls
manage.py  templates  venv  xiaofu
(venv) ai@pro:~/dev/xiaofu$ python manage.py makemigrations
Traceback (most recent call last):
  File "/home/ai/dev/xiaofu/manage.py", line 21, in <module>
    main()
  File "/home/ai/dev/xiaofu/manage.py", line 17, in main
    execute_from_command_line(sys.argv)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/__init__.py", line 381, in execute_from_command_line
    utility.execute()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/__init__.py", line 325, in execute
    settings.INSTALLED_APPS
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/conf/__init__.py", line 79, in __getattr__
    self._setup(name)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/conf/__init__.py", line 66, in _setup
    self._wrapped = Settings(settings_module)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/conf/__init__.py", line 157, in __init__
    mod = importlib.import_module(self.SETTINGS_MODULE)
  File "/usr/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 855, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/home/ai/dev/xiaofu/xiaofu/settings/dev.py", line 67, in <module>
    'DIRS': [BASE_DIR / 'templates']
TypeError: unsupported operand type(s) for /: 'str' and 'str'
```

解决方法：
```python
TEMPLATES = [  
    {  
        'BACKEND': 'django.template.backends.django.DjangoTemplates',  
        # 'DIRS': [BASE_DIR / 'templates'],  
        'DIRS': [BASE_DIR + 'templates'],  
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

# 2 ValueError: Unable to configure handler 'file'
```shell
(venv) ai@pro:~/dev/xiaofu$ python manage.py makemigrations
Traceback (most recent call last):
  File "/usr/lib/python3.9/logging/config.py", line 564, in configure
    handler = self.configure_handler(handlers[name])
  File "/usr/lib/python3.9/logging/config.py", line 745, in configure_handler
    result = factory(**kwargs)
  File "/usr/lib/python3.9/logging/handlers.py", line 153, in __init__
    BaseRotatingHandler.__init__(self, filename, mode, encoding=encoding,
  File "/usr/lib/python3.9/logging/handlers.py", line 58, in __init__
    logging.FileHandler.__init__(self, filename, mode=mode,
  File "/usr/lib/python3.9/logging/__init__.py", line 1146, in __init__
    StreamHandler.__init__(self, self._open())
  File "/usr/lib/python3.9/logging/__init__.py", line 1175, in _open
    return open(self.baseFilename, self.mode, encoding=self.encoding,
FileNotFoundError: [Errno 2] No such file or directory: '/home/ai/dev/xiaofu/logs/xiaofu.log'

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "/home/ai/dev/xiaofu/manage.py", line 21, in <module>
    main()
  File "/home/ai/dev/xiaofu/manage.py", line 17, in main
    execute_from_command_line(sys.argv)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/__init__.py", line 381, in execute_from_command_line
    utility.execute()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/__init__.py", line 357, in execute
    django.setup()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/__init__.py", line 19, in setup
    configure_logging(settings.LOGGING_CONFIG, settings.LOGGING)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/utils/log.py", line 76, in configure_logging
    logging_config_func(logging_settings)
  File "/usr/lib/python3.9/logging/config.py", line 809, in dictConfig
    dictConfigClass(config).configure()
  File "/usr/lib/python3.9/logging/config.py", line 571, in configure
    raise ValueError('Unable to configure handler '
ValueError: Unable to configure handler 'file'
```

解决方法：
```shel
(venv) ai@pro:~/dev/xiaofu$ mkdir logs scripts

(venv) ai@pro:~/dev/xiaofu$ ls
logs  manage.py  scripts  templates  venv  xiaofu
```

# 3 django.core.exceptions.ImproperlyConfigured: Error loading MySQLdb module. Did you install mysqlclient?

解决方法：
```python
#在xiaofu/\__init__.py下添加 

import pymysql

pymysql.install_as_MySQLdb()

```

# 4 RuntimeError: 'cryptography' package is required for sha256_password or caching_sha2_password auth methods
```shell
(venv) ai@pro:~/dev/xiaofu$ python manage.py makemigrations
Traceback (most recent call last):
  File "/home/ai/dev/xiaofu/manage.py", line 21, in <module>
    main()
  File "/home/ai/dev/xiaofu/manage.py", line 17, in main
    execute_from_command_line(sys.argv)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/__init__.py", line 381, in execute_from_command_line
    utility.execute()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/__init__.py", line 375, in execute
    self.fetch_command(subcommand).run_from_argv(self.argv)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/base.py", line 323, in run_from_argv
    self.execute(*args, **cmd_options)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/base.py", line 364, in execute
    output = self.handle(*args, **options)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/base.py", line 83, in wrapped
    res = handle_func(*args, **kwargs)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/core/management/commands/makemigrations.py", line 101, in handle
    loader.check_consistent_history(connection)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/db/migrations/loader.py", line 283, in check_consistent_history
    applied = recorder.applied_migrations()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/db/migrations/recorder.py", line 73, in applied_migrations
    if self.has_table():
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/db/migrations/recorder.py", line 56, in has_table
    return self.Migration._meta.db_table in self.connection.introspection.table_names(self.connection.cursor())
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/db/backends/base/base.py", line 256, in cursor
    return self._cursor()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/db/backends/base/base.py", line 233, in _cursor
    self.ensure_connection()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/db/backends/base/base.py", line 217, in ensure_connection
    self.connect()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/db/backends/base/base.py", line 195, in connect
    self.connection = self.get_new_connection(conn_params)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/django/db/backends/mysql/base.py", line 227, in get_new_connection
    return Database.connect(**conn_params)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/pymysql/connections.py", line 365, in __init__
    self.connect()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/pymysql/connections.py", line 681, in connect
    self._request_authentication()
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/pymysql/connections.py", line 980, in _request_authentication
    auth_packet = _auth.caching_sha2_password_auth(self, auth_packet)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/pymysql/_auth.py", line 271, in caching_sha2_password_auth
    data = sha2_rsa_encrypt(conn.password, conn.salt, conn.server_public_key)
  File "/home/ai/dev/xiaofu/venv/lib/python3.9/site-packages/pymysql/_auth.py", line 144, in sha2_rsa_encrypt
    raise RuntimeError(
RuntimeError: 'cryptography' package is required for sha256_password or caching_sha2_password auth methods
```

解决方法：
```shell
(venv) ai@pro:~/dev/xiaofu$ pip install cryptography -i http://pypi.tuna.tsinghua.edu.cn/simple/ --trusted-host pypi.tuna.tsinghua.edu.cn
```

# 5 AttributeError: 'str' object has no attribute 'decode'
```shell
# 再次运行python manage.py makemigrations报错
 File "/home/apps/py_virtual_environment/xiaofu/lib/python3.9/site-packages/django/db/backends/utils.py", line 103, in execute
    sql = self.db.ops.last_executed_query(self.cursor, sql, params)
  File "/home/apps/py_virtual_environment/xiaofu/lib/python3.9/site-packages/django/db/backends/mysql/operations.py", line 146, in last_executed_query
    query = query.decode(errors='replace')
AttributeError: 'str' object has no attribute 'decode'


# 找到文件/home/apps/py_virtual_environment/xiaofu/lib/python3.9/site-packages/django/db/backends/mysql/operations.py
146行修改为
query = query.encode(errors='replace')



# 再次运行python manage.py makemigrations成功
(xiaofu) [apps@centos1 xiaofu]$ python manage.py makemigrations
Migrations for 'users':
  xiaofu/apps/users/migrations/0001_initial.py
    - Create model User
(xiaofu) [apps@centos1 xiaofu]$ python manage.py migrate
```