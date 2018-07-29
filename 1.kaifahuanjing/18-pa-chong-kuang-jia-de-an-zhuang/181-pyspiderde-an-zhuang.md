### 1.说明

带有强大的 WebUI、脚本编辑器、任务监控器、项目管理器以及结果处理器，同时它支持多种数据库后端、多种消息队列，另外它还支持 JavaScript 渲染页面的爬取，使用起来非常方便。

### 2. 相关链接 {#1-相关链接}

* 官方文档：[http://docs.pyspider.org/](http://docs.pyspider.org/)
* PyPi：[https://pypi.python.org/pypi/pyspider](https://pypi.python.org/pypi/pyspider)
* GitHub：[https://github.com/binux/pyspider](https://github.com/binux/pyspider)
* 官方教程：[http://docs.pyspider.org/en/latest/tutorial](http://docs.pyspider.org/en/latest/tutorial)
* 在线实例：[http://demo.pyspider.org](http://demo.pyspider.org/)

### 3.准备工作

PySpider 是支持 JavaScript 渲染的，而这个过程是依赖于 PhantomJS 的，所以还需要安装 PhantomJS，所以在安装之前请[安装](/1.kaifahuanjing/12-qing-qiu-ku-de-an-zhuang/125-phantomjsde-an-zhuang.md)好 PhantomJS

### 4.常见错误

Windows 下可能会出现这样的错误提示：Command "python setup.py egg\_info" failed with error code 1 in /tmp/pip-build-vXo1W3/pycurl

这是pycurl安装错误，需要安装pucurlku，下载地址:[http://www.lfd.uci.edu/~gohlke/pythonlibs/\#pycurl](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pycurl)，找到与之对应的wheel文件。

如Windows 64 位，Python3.6 则下载 pycurl‑7.43.0‑cp36‑cp36m‑win\_amd64.whl

```
pip install pycurl‑7.43.0‑cp36‑cp36m‑win_amd64.whl
```

Linux 下如果遇到 PyCurl 的错误:\_\_main\_\_.ConfigurationError: Could not run curl-config: \[Errno2\] No such file or directory

  






