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



