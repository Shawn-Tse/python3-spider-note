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

### 安装requests

```
pip install requests
```

### GET请求

```
>>> import requests
>>> result = requests.get("https://httpbin.org/ip")
>>> result
<Response [200]> # 响应对象
>>> result.status_code # 响应状态码
200
>>> result.content # 响应内容
b'{"origin":"221.13.7.74"}\n'
```

### POST请求

```
>>> r = requests.post('http://httpbin.org/post', data = {'key':'value'})
>>> r
<Response [200]>
```

### 自定义请求头

服务器反爬虫机制会判断客户端请求头的User-Agent是否源于真实浏览器，所以，使用requests指定UA伪装成浏览器发起请求

```
>>> url = "https://httpbin.org/headers"
>>> headers = {"user-agent":"Mozilla/5.0"}
>>> r = requests.get(url,headers=headers)
>>> r.content
b'{"headers":{"Accept":"*/*","Accept-Encoding":"gzip, deflate","Connection":"close","Host":"httpbin.org","User-Agent":"Mozilla/5.0"}}\n'
```

### 参数传递

```
>>> url = "http://httpbin.org/get"
>>> r = requests.get(url,params={"key":"val"})
>>> r.url
'http://httpbin.org/get?key=val'
```

### 指定cookie

```
>>> c = requests.get("http://httpbin.org/cookies",cookies={"from-my":"browser"})
>>> c.text
'{"cookies":{"from-my":"browser"}}\n'
```

### 设置超时

```
r = requests.get('https://google.com', timeout=5)
```

### 设置代理

```
import requests

proxies = {
    'http': 'http://127.0.0.1:1080',
    'https': 'http://127.0.0.1:1080',
}

r = requests.get('http://www.kuaidaili.com/free/', proxies=proxies, timeout=2)
```

### session

```
import requests

s = requests.Session()
s.cookies = requests.utils.cookiejar_from_dict({"a": "c"})
r = s.get('http://httpbin.org/cookies')
print(r.text)
# '{"cookies": {"a": "c"}}'

r = s.get('http://httpbin.org/cookies')
print(r.text)
# '{"cookies": {"a": "c"}}'
```


