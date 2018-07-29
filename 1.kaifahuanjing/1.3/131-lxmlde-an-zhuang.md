lxml是python的一个解析库，支持html和xml的解析，并支持xpath的解析方式

### 1.Windows下安装

```
pip install lxml
```

### 2. Linux下的安装 {#3-linux下的安装}

```
pip3 install lxml

```

如果报错，可以尝试下方的解决方案。

#### CentOS、RedHat {#centos、redhat}

对于此类系统，报错主要是因为缺少必要的库。

执行如下命令安装所需的库即可：

```
sudo yum groupinstall -y development tools
sudo yum install -y epel-release libxslt-devel libxml2-devel openssl-devel

```

主要是 libxslt-devel libxml2-devel 这两个库，lxml依赖于它们。安装好了之后重新尝试 Pip 安装即可。

#### Ubuntu、Debian、Deepin {#ubuntu、debian、deepin}

报错的原因同样可能是缺少了必要的类库，执行如下命令安装：

```
sudo apt-get install -y python3-dev build-essential libssl-dev libffi-dev libxml2 libxml2-dev libxslt1-dev zlib1g-dev

```

安装好了之后重新尝试 Pip 安装即可。

### 3. Mac下的安装 {#4-mac下的安装}

在 Mac 平台下，仍然可以首先尝试 Pip 安装，命令如下：

```
pip3 install lxml

```

如果产生错误，可以执行如下命令将必要的类库安装：

```
xcode-select --install

```

之后再重新运行 Pip 安装就没有问题了。

LXML 是一个非常重要的库，后面的 BeautifulSoup、Scrapy 框架都需要用到此库，所以请一定安装成功。

### 4.验证安装

```
python3

>>> import lxml
```

如果没有报错，就代表安装成功了

