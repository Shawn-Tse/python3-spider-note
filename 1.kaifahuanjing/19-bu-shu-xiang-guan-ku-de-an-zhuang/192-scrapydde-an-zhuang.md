### 1.说明

Scrapyd是一个用于布署和运行的Scrapy的工具，可以利用它将写好的Scrapy项目上传到云主机并通过API来控制运行

### 2.相关链接

* GitHub：[https://github.com/scrapy/scrapyd](https://github.com/scrapy/scrapyd)
* PyPi：[https://pypi.python.org/pypi/scrapyd](https://pypi.python.org/pypi/scrapyd)0
* 官方文档：[https://scrapyd.readthedocs.io](https://scrapyd.readthedocs.io/)

### 3.安装

```
pip install scrapyd
```

### 4.配置

### windows

windows下已经配置好了:

如:E:\Python36\Lib\site-packages\scrapyd\default\_scrapyd.conf

```
[scrapyd]
eggs_dir    = eggs
logs_dir    = logs
items_dir   =
jobs_to_keep = 5
dbs_dir     = dbs
max_proc    = 0
max_proc_per_cpu = 4
finished_to_keep = 100
poll_interval = 5.0
bind_address = 127.0.0.1
http_port   = 6800
debug       = off
runner      = scrapyd.runner
application = scrapyd.app.application
launcher    = scrapyd.launcher.Launcher
webroot     = scrapyd.website.Root

[services]
schedule.json     = scrapyd.webservice.Schedule
cancel.json       = scrapyd.webservice.Cancel
addversion.json   = scrapyd.webservice.AddVersion
listprojects.json = scrapyd.webservice.ListProjects
listversions.json = scrapyd.webservice.ListVersions
listspiders.json  = scrapyd.webservice.ListSpiders
delproject.json   = scrapyd.webservice.DeleteProject
delversion.json   = scrapyd.webservice.DeleteVersion
listjobs.json     = scrapyd.webservice.ListJobs
daemonstatus.json = scrapyd.webservice.DaemonStatus
```

### Linux

安装完毕之后需要新建一个配置文件 /etc/scrapyd/scrapyd.conf，Scrapyd 在运行的时候会读取此配置文件。

因为在 Scrapyd 1.2 版本之后不会自动创建该文件，需要我们自行添加。

执行命令新建文件：

```
sudo mkdir /etc/scrapyd
sudo vim /etc/scrapyd/scrapyd.conf
```

写入windows下的default\_scrapyd.conf的内容

最后输入:wq退出



配置文件的内容可以参见[官方文档](https://scrapyd.readthedocs.io/en/stable/config.html#example-configuration-file)：在这里的配置文件有所修改，其中之一是 max\_proc\_per\_cpu 官方默认为 4，即一台主机每个 CPU 最多运行 4 个Scrapy Job，另外一个是 bind\_address，默认为本地 127.0.0.1，在此修改为 0.0.0.0，以使外网可以访问。

