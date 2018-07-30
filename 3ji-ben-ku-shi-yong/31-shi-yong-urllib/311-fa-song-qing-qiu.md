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

```
import urllib.parse
import urllib.request

data = bytes(urllib.parse.urlencode({"name":"angle"}),encoding="utf-8")
response = urllib.request.urlopen("http://httpbin.org/post",data=data)
print(response.read())
```

### timeout参数

### 其他参数



