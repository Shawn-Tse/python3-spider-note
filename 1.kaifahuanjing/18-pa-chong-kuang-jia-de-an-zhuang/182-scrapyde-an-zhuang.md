### 1. 相关链接 {#1-相关链接}

* 官方网站：[https://scrapy.org](https://scrapy.org/)
* 官方文档：[https://docs.scrapy.org](https://docs.scrapy.org/)
* PyPi：[https://pypi.python.org/pypi/Scrapy](https://pypi.python.org/pypi/Scrapy)
* GitHub：[https://github.com/scrapy/scrapy](https://github.com/scrapy/scrapy)
* 中文文档：[http://scrapy-chs.readthedocs.io](http://scrapy-chs.readthedocs.io/)

### 2. Anaconda安装 {#2-anaconda安装}

如果已经安装好了 Anaconda，那么可以通过 conda 命令安装 Scrapy，安装命令如下：

```
conda install Scrapy
```

运行之后便可以完成 Scrapy 的安装。

### 3. Windows下的安装 {#3-windows下的安装}

[所有工具可在这里下载](https://pan.baidu.com/s/1ZUb8WhkajsWkUlfDpRiBYg)

#### 安装lxml

[lxml安装](/1.kaifahuanjing/1.3/131-lxmlde-an-zhuang.md)

#### 安装pyOpenSSL

wheel文件下载地址:[https://pypi.python.org/pypi/pyOpenSSL\#downloads](https://pypi.python.org/pypi/pyOpenSSL#downloads)![](/assets/1.8.2-4.png)下载完成后安装

```
pip install pyOpenSSL-18.0.0-py2.py3-none-any.whl
```

#### 安装Twisted {#安装twisted}

下载 Wheel 文件:[http://www.lfd.uci.edu/~gohlke/pythonlibs/\#twisted](#)

如 Python 3.6 版本，Windows 64 位系统，当前最新版本为 [Twisted‑18.7.0‑cp36‑cp36m‑win\_amd64.whl](javascript:;)

下载完后安装

```
pip install Twisted‑18.7.0‑cp36‑cp36m‑win_amd64.whl
```

### 安装PyWin32 {#安装pywin32}

从官方网站下载对应版本的安装包即可，链接为：[https://sourceforge.net/projects/pywin32/files/pywin32/Build%20221/](https://sourceforge.net/projects/pywin32/files/pywin32/Build 221/)

![](/assets/1.8.2-5.png)如 Python 3.6 版本可以选择下载 pywin32-221.win-amd64-py3.6.exe，下载完毕之后双击安装即可。

注意这里使用的是 Build 221 版本，随着时间推移，版本肯定会继续更新，最新的版本可以查看：[https://sourceforge.net/projects/pywin32/files/pywin32/](https://sourceforge.net/projects/pywin32/files/pywin32/)，查找最新的版本安装即可。

#### 安装Scrapy {#安装scrapy}

```
pip install scrapy
```

### 4. Linux下的安装 {#4-linux下的安装}

#### CentOS、RedHat {#centos、redhat}

首先确保一些依赖库已经安装，运行如下命令：

```
sudo yum groupinstall -y development tools
sudo yum install -y epel-release libxslt-devel libxml2-devel openssl-devel
```

最后利用 Pip 安装 Scrapy 即可，运行如下命令：

```
pip3 install Scrapy
```

#### Ubuntu、Debian、Deepin {#ubuntu、debian、deepin}

首先确保一些依赖库已经安装，运行如下命令：

```
sudo apt-get install build-essential python3-dev libssl-dev libffi-dev libxml2 libxml2-dev libxslt1-dev zlib1g-dev
```

然后利用 Pip 安装 Scrapy 即可，运行如下命令：

```
pip3 install Scrapy
```

### 5. Mac下的安装 {#5-mac下的安装}

在 Mac 上构建 Scrapy 的依赖库需要 C 编译器以及开发头文件，它一般由 Xcode 提供，运行如下命令安装即可：

```
xcode-select --install
```

随后利用 Pip 安装 Scrapy 即可，运行如下命令：

```
pip3 install Scrapy
```

### 6. 验证安装 {#6-验证安装}

安装之后，在命令行下输入 scrapy

```
scrapy
```

![](/assets/1.8.2.9.png)

