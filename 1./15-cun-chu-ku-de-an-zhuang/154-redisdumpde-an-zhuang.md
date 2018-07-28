### 1.说明

RedisDump是一个用于Redis数据导入导出的工具，是基于Ruby实现的，所以要安装RedisDump需要安装Ruby

### 2. 相关链接 {#1-相关链接}

* GitHub：[https://github.com/delano/redis-dump](https://github.com/delano/redis-dump)
* 官方文档：[http://delanotes.com/redis-dump](http://delanotes.com/redis-dump)

### 3.安装Ruby

官网:[http://www.ruby-lang.org/zh\_cn/documentation/installation](http://www.ruby-lang.org/zh_cn/documentation/installation)

windows-下载地址:[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)

![](/assets/1.5.4-1.png)msys2:[http://repo.msys2.org/distrib/x86\_64/msys2-x86\_64-20180531.exe](http://repo.msys2.org/distrib/x86_64/msys2-x86_64-20180531.exe)

### 3.Gem安装

打开Start Command Prompt with Ruby

![](/assets/15.4-4.png)![](/assets/1.5.4-6.png)如果出现上面类似情况，需要更换源

```
$ gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
或者 
添加淘宝镜像：gem source -a https://ruby.taobao.org/ --remove https://rubygems.org/

# 查看源
$ gem sources -l
*** CURRENT SOURCES ***

https://gems.ruby-china.org
```

利用gem命令安装

```
gem install redis-dump
```

### 4.验证安装

安装成功后就可以执行如下两个命令：

```
redis-dump
redis-load
```

使用redis-dump导出数据

导出指令如下：

```
redis-dump -u :mypassword@localhost:6379 -d database_name >test.json
```

-u 后边跟redis数据库的信息，如果没有密码可以不写

```
redis-dump -u localhost:6379 -d database_name  >test.json
```

如果直接导出本机端口为6379的可以把 -u 的部分给省去

```
redis-dump >test.json
```

-d 指定导出哪个数据库的数据，如果不写则导出所有的，一定要注意数据库名字（这里是 database\_name ）前后必须要加空格。

