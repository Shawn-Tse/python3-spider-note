### 使用python内建模块urllib请求一个url

```
import ssl
from urllib.request import Request
from urllib.request import urlopen

context = ssl._create_unverified_context()

# http 请求
request = Request(url="https://foofish.net/pip.html",
                  method="GET",
                  headers={"Host":"foofish.net"},
                  data=None)

# http 响应
response = urlopen(request,context=context)
headers = response.info() # 响应头
content = response.read() # 响应体
code = response.getcode() # 状态码
print(headers)
print(content)
print(code)
```



