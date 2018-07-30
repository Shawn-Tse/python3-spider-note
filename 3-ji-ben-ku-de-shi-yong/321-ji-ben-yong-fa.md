### 1.准备工作

[安装requests](/1.kaifahuanjing/12-qing-qiu-ku-de-an-zhuang/121-requestsde-an-zhuang.md)

### 2.实例演示

get请求实例:

```
import requests

response = requests.get("https://www.baidu.com/")

# Response类型
print(type(response))
# 状态码
print(response.status_code)
# 文本类型
print(type(response.text))
# 文本内容
print(response.text)
# cookies
print(response.cookies)
```

运行结果:

```
<class 'requests.models.Response'>
200
<class 'str'>
<!DOCTYPE html>
<!--STATUS OK--><html> <head><meta http-equiv=content-type content=text/html;charset=utf-8><meta http-equiv=X-UA-Compatible content=IE=Edge><meta content=always name=referrer><link rel=stylesheet type=text/css href=https://ss1.bdstatic.com/5eN1bjq8AAUYm2zgoY3K/r/www/cache/bdorz/baidu.min.css><title>ç¾åº¦ä¸ä¸ï¼ä½ å°±ç¥é</title></head> <body link=#0000cc> <div id=wrapper> <div id=head> <div class=head_wrapper> <div class=s_form> <div class=s_form_wrapper> <div id=lg> <img hidefocus=true src=//www.baidu.com/img/bd_logo1.png width=270 height=129> </div> <form id=form name=f action=//www.baidu.com/s class=fm> <input type=hidden name=bdorz_come value=1> <input type=hidden name=ie value=utf-8> <input type=hidden name=f value=8> <input type=hidden name=rsv_bp value=1> <input type=hidden name=rsv_idx value=1> <input type=hidden name=tn value=baidu><span class="bg s_ipt_wr"><input id=kw name=wd class=s_ipt value maxlength=255 autocomplete=off autofocus=autofocus></span><span class="bg s_btn_wr"><input type=submit id=su value=ç¾åº¦ä¸ä¸ class="bg s_btn" autofocus></span> </form> </div> </div> <div id=u1> <a href=http://news.baidu.com name=tj_trnews class=mnav>æ°é»</a> <a href=https://www.hao123.com name=tj_trhao123 class=mnav>hao123</a> <a href=http://map.baidu.com name=tj_trmap class=mnav>å°å¾</a> <a href=http://v.baidu.com name=tj_trvideo class=mnav>è§é¢</a> <a href=http://tieba.baidu.com name=tj_trtieba class=mnav>è´´å§</a> <noscript> <a href=http://www.baidu.com/bdorz/login.gif?login&amp;tpl=mn&amp;u=http%3A%2F%2Fwww.baidu.com%2f%3fbdorz_come%3d1 name=tj_login class=lb>ç»å½</a> </noscript> <script>document.write('<a href="http://www.baidu.com/bdorz/login.gif?login&tpl=mn&u='+ encodeURIComponent(window.location.href+ (window.location.search === "" ? "?" : "&")+ "bdorz_come=1")+ '" name="tj_login" class="lb">ç»å½</a>');
                </script> <a href=//www.baidu.com/more/ name=tj_briicon class=bri style="display: block;">æ´å¤äº§å</a> </div> </div> </div> <div id=ftCon> <div id=ftConw> <p id=lh> <a href=http://home.baidu.com>å³äºç¾åº¦</a> <a href=http://ir.baidu.com>About Baidu</a> </p> <p id=cp>&copy;2017&nbsp;Baidu&nbsp;<a href=http://www.baidu.com/duty/>ä½¿ç¨ç¾åº¦åå¿è¯»</a>&nbsp; <a href=http://jianyi.baidu.com/ class=cp-feedback>æè§åé¦</a>&nbsp;äº¬ICPè¯030173å·&nbsp; <img src=//www.baidu.com/img/gs.gif> </p> </div> </div> </div> </body> </html>

<RequestsCookieJar[<Cookie BDORZ=27315 for .baidu.com/>]>
```

其他请求方式

```
r = requests.post('http://httpbin.org/post')
r = requests.put('http://httpbin.org/put')
r = requests.delete('http://httpbin.org/delete')
r = requests.head('http://httpbin.org/get')
r = requests.options('http://httpbin.org/get')
```

### 3. GET请求 {#3-get请求}

测试连接:[http://httpbin.org/get](https://germey.gitbooks.io/python3webspider/content/[http:/httpbin.org/get)，会判断如果如果是 GET 请求的话，会返回响应的 Request 信息

实例:

```
import requests

response = requests.get('http://httpbin.org/get')
print(response.text)
```

运行结果:

```
{
  "args": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Connection": "close", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.18.4"
  }, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/get"
}
```

在GET请求中构造参数

实例:

```
import requests

# 一般情况下不这样书写，都是伪造一个字典
# response =  requests.get('http://httpbin.org/get?name=angle&like=dongman')

params = {
    'name':'angle',
    'like':'dongmnae',
}
response = requests.get("http://httpbin.org/get", params=params)

print(response.text)
```

运行结果:

```
{
  "args": {
    "like": "dongmnae", 
    "name": "angle"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Connection": "close", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.18.4"
  }, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/get?name=angle&like=dongmnae"
}
```

通过返回信息我们可以判断，请求的链接自动被构造成了：[http://httpbin.org/get?name=angle&like=dongman](http://httpbin.org/get?name=angle&like=dongman)

另外，网页的返回类型实际上是 str 类型，但是它很特殊，是 Json 的格式，所以如果我们想直接把返回结果解析，得到一个字典格式的话，可以直接调用 json\(\) 方法。

实例:

```
import requests

params = {
    'name':'angle',
    'like':'dongmnae',
}
response = requests.get("http://httpbin.org/get", params=params)
print(type(response.text))
print(response.text)
print(type(response.json()))
```

运行结果:

```
<class 'str'>
{
  "args": {
    "like": "dongmnae", 
    "name": "angle"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Connection": "close", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.18.4"
  }, 
  "origin": "220.197.208.229", 
  "url": "http://httpbin.org/get?name=angle&like=dongmnae"
}

<class 'dict'>
```

### 抓取网页

以知了为例子

实例:

```

```



