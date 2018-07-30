### 1.相关链接

官方文档:[https://docs.python.org/3/library/urllib.request.html](https://docs.python.org/3/library/urllib.request.html)

测试网站:[http://httpbin.org/post](http://httpbin.org/post)

### 2. urlopen\(\) {#1-urlopen}

urllib.request 模块提供了最基本的构造 HTTP 请求的方法，利用它可以模拟浏览器的一个请求发起过程，同时它还带有处理authenticaton（授权验证），redirections（重定向\)，cookies（浏览器Cookies）以及其它内容。

例子:抓取百度首页

```
import urllib.request

response = urllib.request.urlopen("http://www.baidu.com")
print(response.read().decode('utf-8'))
print(type(response))
```

运行结果:

![](/assets/3.1.1-1.png)

输出的类型:

```
<class 'http.client.HTTPResponse'>
```

通过输出结果可以发现它是一个 HTTPResposne 类型的对象，主要包含的方法有 read\(\)、readinto\(\)、getheader\(name\)、getheaders\(\)、fileno\(\) 等方法和 msg、version、status、reason、debuglevel、closed 等属性。

可以利用response对象调用这些属性，例子:

```
import urllib.request

response = urllib.request.urlopen("http://www.baidu.com")
print(response.status) # 状态码
print(response.getheaders()) # 响应头信息
print(response.getheader('Server')) # headers中server的值
```

输出结果为:

```
200
[('Bdpagetype', '1'), ('Bdqid', '0xef591dd800056531'), ('Cache-Control', 'private'), ('Content-Type', 'text/html'), ('Cxy_all', 'baidu+16f7eb85af21b1161c1ef2120b208c5a'), ('Date', 'Mon, 30 Jul 2018 06:01:58 GMT'), ('Expires', 'Mon, 30 Jul 2018 06:01:28 GMT'), ('P3p', 'CP=" OTI DSP COR IVA OUR IND COM "'), ('Server', 'BWS/1.1'), ('Set-Cookie', 'BAIDUID=ADA3E646B4E0A6AE8F0BA17B395B76A3:FG=1; expires=Thu, 31-Dec-37 23:55:55 GMT; max-age=2147483647; path=/; domain=.baidu.com'), ('Set-Cookie', 'BIDUPSID=ADA3E646B4E0A6AE8F0BA17B395B76A3; expires=Thu, 31-Dec-37 23:55:55 GMT; max-age=2147483647; path=/; domain=.baidu.com'), ('Set-Cookie', 'PSTM=1532930518; expires=Thu, 31-Dec-37 23:55:55 GMT; max-age=2147483647; path=/; domain=.baidu.com'), ('Set-Cookie', 'delPer=0; expires=Wed, 22-Jul-2048 06:01:28 GMT'), ('Set-Cookie', 'BDSVRTM=0; path=/'), ('Set-Cookie', 'BD_HOME=0; path=/'), ('Set-Cookie', 'H_PS_PSSID=1441_25810_26458_21121_18559_26350_26920_22160; path=/; domain=.baidu.com'), ('Vary', 'Accept-Encoding'), ('X-Ua-Compatible', 'IE=Edge,chrome=1'), ('Connection', 'close'), ('Transfer-Encoding', 'chunked')]
BWS/1.1
```

urlopen\(\)函数的API:

`urllib.request.urlopen（url，data = None，[ timeout，] *，cafile = None，capath = None，cadefault = False，context = None ）`

### data参数

data 参数是可选的，如果要添加 data，它要是字节流编码格式的内容，即 bytes 类型，通过 bytes\(\) 方法可以进行转化，另外如果传递了这个 data 参数，它的请求方式就不再是 GET 方式请求，而是 POST。

模拟一个post请求:

```
import urllib.parse
import urllib.request

data = bytes(urllib.parse.urlencode({"name":"angle"}),encoding="utf-8")
response = urllib.request.urlopen("http://httpbin.org/post",data=data)
print(response.read().decode('utf-8'))
```

运行结果如下:

```
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "name": "angle"
  }, 
  "headers": {
    "Accept-Encoding": "identity", 
    "Connection": "close", 
    "Content-Length": "10", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "Python-urllib/3.6"
  }, 
  "json": null, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/post"
}
```

### timeout参数

timeout 参数可以设置超时时间，单位为秒，意思就是如果请求超出了设置的这个时间还没有得到响应，就会抛出异常，如果不指定，就会使用全局默认时间。它支持 HTTP、HTTPS、FTP 请求。

实例:

```
import urllib.request

response = urllib.request.urlopen("http://httpbin.org/get",timeout=0.1)
print(response.read().decode("utf-8"))
```

运行结果如下:

```
....

During handling of the above exception, another exception occurred:

....
  File "E:\Python36\lib\urllib\request.py", line 1320, in do_open
    raise URLError(err)
urllib.error.URLError: <urlopen error timed out>
```

设置超时时间为0.1秒，程序超过0.1秒没有响应，就会抛出URLError异常，属于urllib.error模块，错误的原因是超时

可以利用try/except语句来跳过长时间未响应的页面

```
import urllib.request
import urllib.error
import socket

try:
    response = urllib.request.urlopen("http://httpbin.org/get",timeout=0.1)
except urllib.error.URLError as e:
    if isinstance(e.reason,socket.timeout):
        print("TIME OUT")
```

运行结果:

```
TIME OUT
```

### 其他参数

还有 context 参数，它必须是 ssl.SSLContext 类型，用来指定 SSL 设置。

cafile 和 capath 两个参数是指定 CA 证书和它的路径，这个在请求 HTTPS 链接时会有用。

cadefault 参数现在已经弃用了，默认为 False。

### 2.Request

例子:

```
import urllib.request

request = urllib.request.Request("https://python.org")
response = urllib.request.urlopen(request)
print(response.read().decode('utf-8'))
```

urlopen\(\) 方法的参数不再是一个 URL，而是一个 Request 类型的对象，通过构造这个这个数据结构，一方面我们可以将请求独立成一个对象，另一方面可配置参数更加丰富和灵活

Request函数API:

```
class urllib.request.Request(url, data=None, headers={}, origin_req_host=None, unverifiable=False, method=None)
```

* url 参数是请求 URL，这个是必传参数，其他的都是可选参数。
* data 参数如果要传必须传 bytes（字节流）类型的，如果是一个字典，可以先用 urllib.parse 模块里的 urlencode\(\) 编码。
* headers 参数是一个字典，这个就是 Request Headers ，可以在构造 Request 时通过 headers 参数直接构造，也可以通过调用 Request 实例的 add\_header\(\) 方法来添加。

添加 Request Headers 最常用的用法就是通过修改 User-Agent 来伪装浏览器，默认的 User-Agent 是 Python-urllib，我们可以通过修改它来伪装浏览器，比如要伪装火狐浏览器，你可以把它设置为：

```
Mozilla/5.0 (X11; U; Linux i686) Gecko/20071127 Firefox/2.0.0.11
```

* origin\_req\_host 参数指的是请求方的 host 名称或者 IP 地址。
* unverifiable 参数指的是这个请求是否是无法验证的，默认是False。意思就是说用户没有足够权限来选择接收这个请求的结果。例如我们请求一个 HTML 文档中的图片，但是我们没有自动抓取图像的权限，这时 unverifiable 的值就是 True。
* method 参数是一个字符串，它用来指示请求使用的方法，比如GET，POST，PUT等等。

实例:

```
from urllib import request,parse

url = 'http://httpbin.org/post'
# 伪造请求头
headers = {
    'User-Agent': 'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)',
    'Host': 'httpbin.org'
}
# 构造参数
dict = {
    'name':"angle",
}
# 转换为字节流
data = bytes(parse.urlencode(dict),encoding='utf-8')
req = request.Request(url=url,data=data,headers=headers,method='POST')
response = request.urlopen(req)
print(response.read().decode('utf-8'))
```

运行结果:

```
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "name": "angle"
  }, 
  "headers": {
    "Accept-Encoding": "identity", 
    "Connection": "close", 
    "Content-Length": "10", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)"
  }, 
  "json": null, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/post"
}
```

通过四个参数构造了一个 Request，url 即请求 URL，在headers 中指定了 User-Agent 和 Host，传递的参数 data 用了 urlencode\(\) 和 bytes\(\) 方法来转成字节流，并指定了请求方式为 POST。

另外一种添加headers的方法：

利用add\_header\(\)方法来添加headers

```
req = request.Request(url=url,data=data,method='POST')
req.add_header('User-Agent','Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)')
```

注意add\_header\(\):add\_header\(key,value\)

### 3. 高级用法 {#3-高级用法}

 利用Handler 处理Cookies 处理，代理设置等操作

urllib.request 模块里的 BaseHandler类，是所有其他 Handler 的父类，提供了最基本的 Handler 的方法，例如 default\_open\(\)、protocol\_request\(\) 方法等。

接下来就有各种 Handler 子类继承这个 BaseHandler 类，举例几个如下：

* HTTPDefaultErrorHandler 用于处理 HTTP 响应错误，错误都会抛出 HTTPError 类型的异常。
* HTTPRedirectHandler 用于处理重定向。
* HTTPCookieProcessor 用于处理 Cookies。
* ProxyHandler 用于设置代理，默认代理为空。
* HTTPPasswordMgr 用于管理密码，它维护了用户名密码的表。
* HTTPBasicAuthHandler 用于管理认证，如果一个链接打开时需要认证，那么可以用它来解决认证问题。
* 另外还有其他的 Handler 类，在这不一一列举了，详情可以参考官方文档：
  [https://docs.python.org/3/library/urllib.request.html\#urllib.request.BaseHandler](https://docs.python.org/3/library/urllib.request.html#urllib.request.BaseHandler)

另外一个比较重要的类就是 OpenerDirector，我们可以称之为 Opener，我们之前用过 urlopen\(\) 这个方法，实际上它就是 Urllib为我们提供的一个 Opener。

那么为什么要引入 Opener ？因为需要实现更高级的功能，之前使用的 Request、urlopen\(\) 相当于类库封装好了极其常用的请求方法，利用它们两个就可以完成基本的请求，但是现在不一样了，需要实现更高级的功能，所以需要深入一层进行配置，使用更底层的实例来完成我们的操作。

所以，在这里就用到了比调用 urlopen\(\) 的对象的更普遍的对象，也就是 Opener。

Opener 可以使用 open\(\) 方法，返回的类型和 urlopen\(\) 如出一辙。那么它和 Handler 有什么关系？简而言之，就是利用 Handler 来构建 Opener。

