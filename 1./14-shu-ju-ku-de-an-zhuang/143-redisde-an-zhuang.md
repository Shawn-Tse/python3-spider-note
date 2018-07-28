### 1. 相关链接 {#1-相关链接}

* 官方网站：
  [https://redis.io](https://redis.io/)
* 官方文档：
  [https://redis.io/documentation](https://redis.io/documentation)
* 中文官网：
  [http://www.redis.cn](http://www.redis.cn/)
* GitHub：
  [https://github.com/antirez/redis](https://github.com/antirez/redis)
* 中文教程：
  [http://www.runoob.com/redis/redis-tutorial.html](http://www.runoob.com/redis/redis-tutorial.html)
* Redis Desktop Manager：
  [https://redisdesktop.com](https://redisdesktop.com/)
* Redis Desktop Manager GitHub：
  [https://github.com/uglide/RedisDesktopManager](https://github.com/uglide/RedisDesktopManager)

### 2. Windows下的安装 {#2-windows下的安装}

Redis 在 Windows 下可以直接到 GitHub 的发行版本里面下载，[https://github.com/MSOpenTech/redis/releases](https://github.com/MSOpenTech/redis/releases)。

可以下载 Redis-x64-3.2.100.msi 安装即可。

另外推荐下载一个 Redis Desktop Manager 可视化管理工具，来管理Redis。

可以到官方网站下载，链接为：[https://redisdesktop.com/download](https://redisdesktop.com/download)也可以到 GitHub 下载最新发行版本，链接为：[https://github.com/uglide/RedisDesktopManager/releases](https://github.com/uglide/RedisDesktopManager/releases)。

### 3. Linux下的安装 {#3-linux下的安装}

#### Ubuntu、Debian、Deepin {#ubuntu、debian、deepin}

使用a pt-get 命令行安装：

```
sudo apt-get -y install redis-server

```

运行如上命令即可完成 Redis 的安装，然后输入 redis-cli 即可进入 Redis 命令行模式。

```
$ redis-cli
127.0.0.1:6379
>
 set 'name' 'Germey'
OK
127.0.0.1:6379
>
 get 'name'
"Germey"

```

这样就证明 Redis 成功安装了，但是现在 Redis 还是无法远程连接的，依然需要修改配置文件，配置文件路径为 /etc/redis/redis.conf。

注释这一行：

```
bind 127.0.0.1

```

另外推荐给 Redis 设置密码，取消注释这一行：

```
requirepass foobared

```

foobared 即当前密码，可以自行修改。

然后重启 Redis 服务，使用如下命令：

```
sudo /etc/init.d/redis-server restart

```

现在就可以使用密码远程连接 Redis 了。

另外停止和启动 Redis 服务的命令如下：

```
sudo /etc/init.d/redis-server stop
sudo /etc/init.d/redis-server start

```

#### CentOS、RedHat {#centos、redhat}

首先添加 EPEL 仓库，然后更新 Yum 源：

```
sudo yum install epel-release
sudo yum update

```

然后安装 Redis 数据库：

```
sudo yum -y install redis

```

安装好之后启动 Redis 服务：

```
sudo systemctl start redis

```

同样可以使用 redis-cli 进入 Redis 命令行模式操作。

另外为了可以使 Redis 能被远程连接，需要修改配置文件，路径为 /etc/redis.conf。

注释这一行：

```
bind 127.0.0.1

```

另外推荐给 Redis 设置密码，取消注释这一行：

```
requirepass foobared

```

foobared 即当前密码，可以自行修改。

之后保存重启 Redis 服务：

```
sudo systemctl restart redis

```

这样就可以远程连接 Redis 了。

### 4. Mac下的安装 {#4-mac下的安装}

推荐使用 Homenbrew 安装，执行 brew 命令即可。

```
brew install redis

```

启动 Redis 服务：

```
brew services start redis
redis-server /usr/local/etc/redis.conf

```

这样就启动了 Redis 服务。

同样可以使用 redis-cli 进入 Redis 命令行模式。

Mac 下 Redis 的配置文件路径是 /usr/local/etc/redis.conf，可以通过修改它来配置访问密码。

修改配置文件后需要重启 Redis 服务，停止、重启 Redis 服务的命令如下：

```
brew services stop redis
brew services restart redis

```

另外在 Mac 下也可以安装 Redis Desktop Manager 可视化管理工具来管理 Redis。

