### 1.说明

Urllib 库里还提供了 parse 这个模块，定义了处理 URL 的标准接口，例如实现 URL 各部分的抽取，合并以及链接转换。支持如下协议的 URL 处理：file、ftp、gopher、hdl、http、https、imap、mailto、 mms、news、nntp、prospero、rsync、rtsp、rtspu、sftp、shttp、 sip、sips、snews、svn、svn+ssh、telnet、wais

### 2.urlparse\(\) {#1-urlparse}

urlparse\(\) 方法可以实现 URL 的识别和分段

实例:

```
from urllib.parse import urlparse

result = urlparse("https://www.google.com.hk/search?q=python")
print(type(result),result,sep='\n')
```

运行结果:

```
<class 'urllib.parse.ParseResult'>
ParseResult(scheme='https', netloc='www.google.com.hk', path='/search', params='', query='q=python', fragment='')

```



