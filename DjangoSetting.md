项目当前工作路径：
```
PROJECT_PATH = os.path.abspath(os.path.dirname(__file__))
```

可以在数据库文件路径中使用：
```
DATABASE_ENGINE = 'sqlite3'
DATABASE_NAME = '%s/db/test.db' % PROJECT_PATH
```