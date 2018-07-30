使用urllib的request模块可以方便地实现Request的发送并得到Response

urlopen\(\)函数的API:

`urllib.request.urlopen（url，data = None，[ timeout，] *，cafile = None，capath = None，cadefault = False，context = None ）`

url：网页地址



data必须是指定要发送到服务器的其他数据的对象，或者None如果不需要此类数据。



urllib.request模块使用HTTP / 1.1并Connection:close在其HTTP请求中包含标头。



可选的timeout参数指定阻塞操作（如连接尝试）的超时（以秒为单位）（如果未指定，将使用全局默认超时设置）。这实际上仅适用于HTTP，HTTPS和FTP连接。



如果指定了context，则它必须是ssl.SSLContext描述各种SSL选项的实例。有关HTTPSConnection 详细信息，请参阅



可选的cafile和capath参数为HTTPS请求指定一组可信CA证书。 cafile应指向包含一组 CA证书的单个文件，而capath应指向散列证书文件的目录。更多信息可以在中找到ssl.SSLContext.load\_verify\_locations\(\)。



该cadefault参数被忽略。



此函数始终返回一个对象，该对象可用作 上下文管理器并具有诸如的方法



geturl\(\) - 返回检索到的资源的URL，通常用于确定是否遵循重定向

info\(\)- 以email.message\_from\_string\(\)实例的形式返回页面的元信息，例如标题（请参阅 HTTP标题的快速参考）

getcode\(\) - 返回响应的HTTP状态代码。



