Django1.0版本后为Admin注册模型与之前有了很大变化：

需要在对应应用程序目录下，创建admin.py:
```
from django.contrib import admin
from django_test.books.models import Book, Author, Publisher

admin.site.register(Book)
admin.site.register(Author)
admin.site.register(Publisher)
```

参考资料：http://code.djangoproject.com/wiki/BackwardsIncompatibleChanges#Mergednewforms-adminintotrunk


---


## 定制管理模板 ##