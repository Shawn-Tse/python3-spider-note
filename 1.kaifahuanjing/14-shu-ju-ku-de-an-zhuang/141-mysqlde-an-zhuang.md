### 1. 相关链接

* 官方网站：[https://www.mysql.com/cn](https://www.mysql.com/cn)
* 下载地址：[https://www.mysql.com/cn/downloads](https://www.mysql.com/cn/downloads)
* 中文教程：[http://www.runoob.com/mysql/mysql-tutorial.html](http://www.runoob.com/mysql/mysql-tutorial.html)

### 2.windows下的安装

访问[官网](https://dev.mysql.com/downloads/mysql/)下载

安装完成后，可以在管理员状态下输入命令来启动或停止服务

```
net start mysql57

net stop mysql57
```

### 3. Linux下的安装 {#3-linux下的安装}

下面仍然分不同平台进行介绍。

#### Ubuntu、Debian、Deepin {#ubuntu、debian、deepin}

直接使用 apt-get 命令即可下载安装:

```
sudo apt-get update
sudo apt-get install -y mysql-server mysql-client

```

在安装过程中会提示输入用户名密码，输入之后等待片刻即可完成安装。

启动、关闭、重启 MySQL 服务命令：

```
sudo service mysql start
sudo service mysql stop
sudo service mysql restart

```

#### CentOS、RedHat {#centos、redhat}

以 MySQL 5.6 的 Yum 源为例，如果需要更高版本可以另寻，安装命令如下：

```
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
yum install -y mysql mysql-server

```

运行如上命令即可完成安装，初始密码为空。接下来需要启动 MySQL 服务。

启动 MySQL 服务命令：

```
sudo systemctl start mysqld

```

停止、重启命令：

```
sudo systemctl stop mysqld
sudo systemctl restart mysqld

```

以上我们就完成了 Linux 下 MySQL 的安装，安装完成之后可以修改密码，可以执行如下命令：

```
mysql -u root -p

```

输入密码后进入 MySQL 命令行模式。

```
use mysql;
UPDATE user SET Password = PASSWORD('newpass') WHERE user = 'root';
FLUSH PRIVILEGES;

```

命令中 newpass 即为修改的新的 MySQL 密码，请自行替换。

由于 Linux 一般会作为服务器使用，为了使得 MySQL 可以被远程访问，我们需要修改 MySQL 的配置文件，配置文件路径一般为 /etc/mysql/my.cnf。

如使用 vi 进行修改的命令如下：

```
vi /etc/mysql/my.cnf

```

取消此行的注释：

```
bind-address = 127.0.0.1

```

此行限制了 MySQL 只能本地访问而不能远程访问，取消注释即可解除此限制。

修改完成之后重启 MySQL 服务，这样 MySQL 就可以被远程访问了。

到此为止，Linux 下安装 MySQL 的过程结束。

### 4. Mac下的安装 {#4-mac下的安装}

推荐使用 Homebrew 安装，执行 brew 命令即可。

```
brew install mysql

```

启动、停止、重启 MySQL 服务的命令：

```
sudo mysql.server start
sudo mysql.server stop
sudo mysql.server restart

```

Mac 一般不会作为服务器使用，如果要想取消本地 host 绑定，同样修改 my.cnf 文件，然后重启服务即可。

