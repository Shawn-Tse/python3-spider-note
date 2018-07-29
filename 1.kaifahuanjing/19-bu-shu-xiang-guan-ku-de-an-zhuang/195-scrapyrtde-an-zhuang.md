Scrapyrt 为 Scrapy 提供了一个调度的 HTTP 接口，有了它我们不需要再执行 Scrapy 命令而是通过请求一个 HTTP 接口即可调度 Scrapy 任务，Scrapyrt 比 Scrapyd 轻量级，如果不需要分布式多任务的话可以简单使用 Scrapyrt 实现远程 Scrapy 任务的调度。

### 1. 相关链接 {#1-相关链接}

* GitHub：
  [https://github.com/scrapinghub/scrapyrt](https://github.com/scrapinghub/scrapyrt)
* 官方文档：
  [http://scrapyrt.readthedocs.io](http://scrapyrt.readthedocs.io/)

### 2. Pip安装 {#2-pip安装}

推荐使用 Pip 安装，命令如下：

```
pip3 install scrapyrt

```

命令执行完毕之后即可完成安装。

接下来在任意一个 Scrapy 项目中运行如下命令即可启动 HTTP 服务：

```
scrapyrt

```

运行之后会默认在 9080 端口上启动服务，类似的输出结果如下：

```
scrapyrt
2017-07-12 22:31:03+0800 [-] Log opened.
2017-07-12 22:31:03+0800 [-] Site starting on 9080
2017-07-12 22:31:03+0800 [-] Starting factory 
<
twisted.web.server.Site object at 0x10294b160
>
```

如果想更换运行端口可以使用 -p 参数，如：

```
scrapyrt -p 9081

```

这样就会在 9081 端口上运行了。

### 3. Docker安装 {#3-docker安装}

另外 Scrapyrt 也支持 Docker，如想要在 9080 端口上运行，且本地 Scrapy 项目的路径为 /home/quotesbot，可以使用如下命令运行：

```
docker run -p 9080:9080 -tid -v /home/user/quotesbot:/scrapyrt/project scrapinghub/scrapyrt

```

这样同样可以在 9080 端口上监听指定的 Scrapy 项目。

