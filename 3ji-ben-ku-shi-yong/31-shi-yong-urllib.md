### 1.相关链接

官方文档:[https://docs.python.org/3/library/urllib.html](https://docs.python.org/3/library/urllib.html)

### 2.内容

Urllib 库，是 Python 内置的 HTTP 请求库，包含四个模块：

* 第一个模块 request，它是最基本的 HTTP 请求模块，我们可以用它来模拟发送一请求，就像在浏览器里输入网址然后敲击回车一样，只需要给库方法传入 URL 还有额外的参数，就可以模拟实现这个过程了。
* 第二个 error 模块即异常处理模块，如果出现请求错误，我们可以捕获这些异常，然后进行重试或其他操作保证程序不会意外终止。
* 第三个 parse 模块是一个工具模块，提供了许多 URL 处理方法，比如拆分、解析、合并等等的方法。
* 第四个模块是 robotparser，主要是用来识别网站的 robots.txt 文件，然后判断哪些网站可以爬，哪些网站不可以爬的，其实用的比较少。



