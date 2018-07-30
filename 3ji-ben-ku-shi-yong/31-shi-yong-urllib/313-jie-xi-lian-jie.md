### 1.说明

Urllib 库里还提供了 parse 这个模块，定义了处理 URL 的标准接口，例如实现 URL 各部分的抽取，合并以及链接转换。支持如下协议的 URL 处理：file、ftp、gopher、hdl、http、https、imap、mailto、 mms、news、nntp、prospero、rsync、rtsp、rtspu、sftp、shttp、 sip、sips、snews、svn、svn+ssh、telnet、wais

### 2.urlparse\(\) {#1-urlparse}

urlparse\(\) 方法可以实现 URL 的识别和分段

实例:

```
from urllib.parse import urlparse

result = urlparse("https://www.google.com.hk/search;user?q=python#content")
print(type(result),result,sep='\n')
```

运行结果:

```
<class 'urllib.parse.ParseResult'>
ParseResult(scheme='https', netloc='www.google.com.hk', path='/search', params='user', query='q=python', fragment='content')
```

返回结果是一个 ParseResult 类型的对象，它包含了六个部分，分别是 scheme、netloc、path、params、query、fragment

实例url:

```
https://www.google.com.hk/search;user?q=python#content
```

urlparse\(\) 方法将其拆分成了六部分，解析时有特定的分隔符，比如 :// 前面的就是 scheme，代表协议，第一个 / 前面便是 netloc，即域名，分号 ; 前面是 params，代表参数。

所以可以得出一个标准的链接格式如下：

```
scheme://netloc/path;parameters?query#fragment
```

urlparse\(\)API 用法：

```
urllib.parse.urlparse(urlstring, scheme='', allow_fragments=True)
```

* urlstring，是必填项，即待解析的 URL。

* scheme，是默认的协议（比如http、https等），假如这个链接没有带协议信息，会将这个作为默认的协议。

实例:

```
result = urlparse("www.google.com.hk/search;user?q=python#content",scheme="https")
print(result)
```

运行结果:

```
ParseResult(scheme='https', netloc='', path='www.google.com.hk/search', params='user', query='q=python', fragment='content')
```

scheme 参数只有在 URL 中不包含 scheme 信息时才会生效，如果 URL 中有 scheme 信息，那就返回解析出的 scheme

实例:

```
result = urlparse("http://www.google.com.hk/search;user?q=python#content",scheme="https")
print(result)
```

运行结果:

```
ParseResult(scheme='http', netloc='www.google.com.hk', path='/search', params='user', query='q=python', fragment='content')
```

* allow\_fragments，即是否忽略 fragment，如果它被设置为 False，fragment 部分就会被忽略，它会被解析为 path、parameters 或者 query 的一部分，fragment 部分为空。

实例:

```
result = urlparse("http://www.google.com.hk/search;user?q=python#content",allow_fragments=False)
print(result)
```

运行结果:

```
ParseResult(scheme='http', netloc='www.google.com.hk', path='/search', params='user', query='q=python#content', fragment='')
```

当 URL 中不包含 params 和 query 时， fragment 便会被解析为 path 的一部分

实例:

```
result = urlparse("https://www.google.com.hk/webhp#content",allow_fragments=False)
print(result)
```

运行结果:

```
ParseResult(scheme='https', netloc='www.google.com.hk', path='/webhp#content', params='', query='', fragment='')
```

返回结果 ParseResult 实际上是一个元组，我们可以用索引顺序来获取，也可以用属性名称获取

实例:

```
from urllib.parse import urlparse

result = urlparse('http://www.baidu.com/index.html#comment', allow_fragments=False)
print(result.scheme, result[0], result.netloc, result[1], sep='\n')
```

运行结果:

```
http
http
www.baidu.com
www.baidu.com
```

### 3. urlunparse\(\) {#2-urlunparse}

* 与urlparse\(\)相反
* 接受的参数是一个可迭代对象，但是它的长度必须是 6，否则会抛出参数数量不足或者过多的问题

实例:

```
from urllib.parse import urlunparse
data = ['http', 'www.google.com', 'index.html', 'name', 'q=6', 'comment']
print(urlunparse(data))
```

运行结果:

```
http://www.google.com/index.html;name?q=6#comment
```

### 4. urlsplit\(\) {#3-urlsplit}

与urlparse\(\) 方法非常相似，只不过它不会单独解析 parameters 这一部分，只返回五个结果

实例:

```
from urllib.parse import  urlsplit
result = urlsplit("https://www.google.com.hk/webhp#content")
print(result)
```

运行结果:

```
SplitResult(scheme='https', netloc='www.google.com.hk', path='/webhp', query='', fragment='content')
```

返回结果是 SplitResult，其实也是一个元组类型，可以用属性获取值也可以用索引来获取

实例:

```
from urllib.parse import  urlsplit
result = urlsplit("https://www.google.com.hk/webhp#content")
print(result.scheme,result[0])
```

运行结果:

```
https https
```

### 5. urlunsplit\(\) {#4-urlunsplit}

* 与urlsplit\(\)相反
* 与 urlunparse\(\) 类似，也是将链接的各个部分组合成完整链接的方法，传入的也是一个可迭代对象

实例:

```
from urllib.parse import urlunsplit
data = ['http', 'www.google.com', 'index.html', 'q=6', 'comment']
print(urlunsplit(data))
```

运行结果:

```
http://www.google.com/index.html?q=6#comment
```



