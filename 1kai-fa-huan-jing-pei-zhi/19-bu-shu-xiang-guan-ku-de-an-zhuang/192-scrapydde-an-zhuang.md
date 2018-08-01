# 1.9.2 Scrapyd的安装

## 1.说明

Scrapyd是一个用于布署和运行的Scrapy的工具，可以利用它将写好的Scrapy项目上传到云主机并通过API来控制运行

## 2.相关链接

* GitHub：[https://github.com/scrapy/scrapyd](https://github.com/scrapy/scrapyd)
* PyPi：[https://pypi.python.org/pypi/scrapyd](https://pypi.python.org/pypi/scrapyd)0
* 官方文档：[https://scrapyd.readthedocs.io](https://scrapyd.readthedocs.io/)

## 3.安装

```text
pip install scrapyd
```

## 4.配置

## windows

windows下已经配置好了:

如:E:\Python36\Lib\site-packages\scrapyd\default\_scrapyd.conf

```text
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

## Linux

安装完毕之后需要新建一个配置文件 /etc/scrapyd/scrapyd.conf，Scrapyd 在运行的时候会读取此配置文件。

因为在 Scrapyd 1.2 版本之后不会自动创建该文件，需要我们自行添加。

执行命令新建文件：

```text
sudo mkdir /etc/scrapyd
sudo vim /etc/scrapyd/scrapyd.conf
```

写入windows下的default\_scrapyd.conf的内容

最后输入:wq退出

配置文件的内容可以参见[官方文档](https://scrapyd.readthedocs.io/en/stable/config.html#example-configuration-file)：在这里的配置文件有所修改，其中之一是 max\_proc\_per\_cpu 官方默认为 4，即一台主机每个 CPU 最多运行 4 个Scrapy Job，另外一个是 bind\_address，默认为本地 127.0.0.1，在此修改为 0.0.0.0，外网可以访问。

## 5. 后台运行 {#4-后台运行}

由于 Scrapyd 是一个纯 Python 项目，在这里可以直接调用 scrapyd 来运行，为了使程序一直在后台运行，Linux 和 Mac 可以使用如下命令：

```text
(scrapyd > /dev/null &)
```

这样 Scrapyd 就会在后台持续运行了，控制台输出直接忽略，当然如果想记录输出日志可以修改输出目标，如：

```text
(scrapyd > ~/scrapyd.log &)
```

则会输出 Scrapyd 运行输出到 ~/scrapyd.log 文件中。

运行之后便可以在浏览器的 6800 访问 WebUI 了，可以简略看到当前 Scrapyd 的运行 Job、Log 等内容

![](../../.gitbook/assets/1.9.2-1.png)运行 Scrapyd 更佳的方式是使用 Supervisor 守护进程运行，如果感兴趣可以参考：[http://supervisord.org/](http://supervisord.org/)。

## 6. 访问认证 {#5-访问认证}

限制配置完成之后 Scrapyd 和它的接口都是可以公开访问的，如果要想配置访问认证的话可以借助于 Nginx 做反向代理，在这里需要先安装 Nginx 服务器。

在此以 Ubuntu 为例进行说明，安装命令如下：

```text
sudo apt-get install nginx
```

然后修改 Nginx 的配置文件 nginx.conf，增加如下配置：

```text
http {
    server {
        listen 6801;
        location / {
            proxy_pass    http://127.0.0.1:6800/;
            auth_basic    "Restricted";
            auth_basic_user_file    /etc/nginx/conf.d/.htpasswd;
        }
    }
}
```

在这里使用的用户名密码配置放置在 /etc/nginx/conf.d 目录，我们需要使用 htpasswd 命令创建，例如创建一个用户名为 admin 的文件，命令如下：

```text
htpasswd -c .htpasswd admin
```

接下就会提示我们输入密码，输入两次之后，就会生成密码文件，查看一下内容：

```text
cat .htpasswd 
admin:5ZBxQr0rCqwbc
```

配置完成之后我们重启一下 Nginx 服务，运行如下命令：

```text
sudo nginx -s reload
```

这样就成功配置了 Scrapyd 的访问认证了。

