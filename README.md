# python3 爬虫笔记

[![Coveralls bitbucket branch](	https://img.shields.io/badge/python3爬虫笔记-心跳回忆-green.svg?longCache=true&style=plastic)](https://github.com/CoderAngle/python3-spider-note)

爬虫笔记地址:https://xintiaohuiyi.gitbook.io/python3-spider-note/
  
python使用版本:python3

\(python3网络爬虫开发实战笔记\)

---

### pip换源

```
pip源:
豆瓣：http://pypi.douban.com/simple/
清华：https://pypi.tuna.tsinghua.edu.cn/simple
```

#### 第一种:暂时性换源

有时候pip下载速度有点慢，可以换成国内源提升一下速度

```
pip install -i https://pypi.doubanio.com/simple/ 包名 

pip install -i https://pypi.doubanio.com/simple/ flask
```

#### 第二种:永久换源

永久换源的方法如下:

linux下，修改 ~/.pip/pip.conf \(没有就创建一个\)， 修改 index-url，内容如下：

```
[global]

index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

windows下，直接在用户目录中创建一个pip目录，如：C:\Users\miku\pip，新建文件pip.ini，内容如下

```
[global]

index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

![](/assets/000.png)

---

### IDE工具

为了提升编码速度，需要好的编译器，推荐使用pycharm

以下是pycharm破解,使用2017版本就可以了

```
http://idea.lanyus.com/


-javaagent: E:\JetBrains\WebStorm 2018.1\lib\JetbrainsCrack-2.7-release-str


ThisCrackLicenseId-{
"licenseId":"ThisCrackLicenseId",
"licenseeName":"idea",
"assigneeName":"",
"assigneeEmail":"idea@163.com",
"licenseRestriction":"For This Crack, Only Test! Please support genuine!!!",
"checkConcurrentUse":false,
"products":[
{"code":"II","paidUpTo":"2099-12-31"},
{"code":"DM","paidUpTo":"2099-12-31"},
{"code":"AC","paidUpTo":"2099-12-31"},
{"code":"RS0","paidUpTo":"2099-12-31"},
{"code":"WS","paidUpTo":"2099-12-31"},
{"code":"DPN","paidUpTo":"2099-12-31"},
{"code":"RC","paidUpTo":"2099-12-31"},
{"code":"PS","paidUpTo":"2099-12-31"},
{"code":"DC","paidUpTo":"2099-12-31"},
{"code":"RM","paidUpTo":"2099-12-31"},
{"code":"CL","paidUpTo":"2099-12-31"},
{"code":"PC","paidUpTo":"2099-12-31"}
],
"hash":"2911276/0",
"gracePeriodDays":7,
"autoProlongated":false}
```

[下载地址](https://pan.baidu.com/s/1si1u-15AhTkWq2bRdkascQ ) 密码：v97f

### Linux中切换python版本

首先先来看一下我们的默认Python版本

```
$ python --version
Python 2.7.6
```

然后我们修改一下别名

```
$ alias python='/usr/bin/python3'
$ python --version
Python 3.4.3  # 版本已经改变
```

