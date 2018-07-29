### 1.说明

Tornado是一个支持异步的web框架，通过使用非阻塞I/O流，可以支撑成千上万的开放连接，效率很高

### 2. 相关链接 {#1-相关链接}

* GitHub：[https://github.com/tornadoweb/tornado](https://github.com/tornadoweb/tornado)
* PyPi：[https://pypi.python.org/pypi/tornado](https://pypi.python.org/pypi/tornado)
* 官方文档：[http://www.tornadoweb.org](http://www.tornadoweb.org/)

### 3. 安装 {#2-pip安装}

```
pip install tornado
```

### 4.验证安装

```
import tornado.ioloop
import tornado.web

# 类继承自tornado.web.RequestHandler
class MainHandler(tornado.web.RequestHandler):
    # get请求
    def get(self):
        self.write("Hello, world")

def make_app():
    return tornado.web.Application([
        # 映射类视图
        (r"/", MainHandler),
    ])

if __name__ == "__main__":
    # 主程序接口
    app = make_app()
    # 监听端口8888
    app.listen(8888)
    # 启动
    tornado.ioloop.IOLoop.current().start()
```



