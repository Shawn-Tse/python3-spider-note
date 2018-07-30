### 1.说明

Urllib 的 error 模块定义了由 request 模块产生的异常。如果出现了问题，request 模块便会抛出 error 模块中定义的异常

### 2.URLError

URLError 类来自 Urllib 库的 error 模块，它继承自 OSError 类，是 error 异常模块的基类，由 request 模块生的异常都可以通过捕获这个类来处理。

* 具有一个属性 reason，即返回错误的原因

实例:

```
from urllib import request,error

try:
    response = request.urlopen('http://www.runoob.com/python1.html')
except error.URLError as e:
    print(e.reason)
```

访问一个不存在的网页，会报错，但是利用try/except捕获到了URLError这个异常

运行结果:

```
Not Found
```

可以利用try/except抛出URLError异常从而避免程序异常终止，并同时得到有效的处理

### 3.HTTPError

专门用来处理 HTTP 请求错误，比如认证请求失败等等

有三个属性:

* code，返回 HTTP Status Code，即状态码，比如 404 网页不存在，500 服务器内部错误等等。
* reason，同父类一样，返回错误的原因。
* headers，返回 Request Headers。
* 
