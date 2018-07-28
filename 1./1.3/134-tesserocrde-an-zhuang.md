### 1.相关链接 {#2-相关链接}

* Tesserocr GitHub：[https://github.com/sirfz/tesserocr](https://github.com/sirfz/tesserocr)
* Tesserocr PyPi：[https://pypi.python.org/pypi/tesserocr](https://pypi.python.org/pypi/tesserocr)
* Tesseract下载地址：[http://digi.bib.uni-mannheim.de/tesseract](http://digi.bib.uni-mannheim.de/tesseract)
* Tesseract GitHub：[https://github.com/tesseract-ocr/tesseract](https://github.com/tesseract-ocr/tesseract)
* Tesseract 语言包：[https://github.com/tesseract-ocr/tessdata](https://github.com/tesseract-ocr/tessdata)
* Tesseract 文档：[https://github.com/tesseract-ocr/tesseract/wiki/Documentation](https://github.com/tesseract-ocr/tesseract/wiki/Documentation)

### 2.windows下安装![](/assets/1.3.4-1.png)

其中文件名中带有 dev 的为开发版本，不带 dev 的为稳定版本，可以选择下载不带 dev 的最新版本，例如可以选择下载 tesseract-ocr-setup-3.05.01.exe。

接下来安装Tesserocr，直接使用pip 安装

```
pip3 install tesserocr pillow
```

如果tesserocr安装报错

需要使用whl安装，并且需要安装Microsoft Visual C++ 14.0.exe

[下载地址](https://pan.baidu.com/s/1lL3WVCE2T-4zQJbjloP6-w)

```
首先切换到有whl的目录

然后通过pip安装
pip install tesserocr-2.2.2-cp36-cp36m-win_amd64.whl

在这之前需要安装Microsoft Visual C++ 14.0.exe
```

### 3.Linux下的安装 {#4-linux下的安装}

对于 Linux 来说，不同系统已经有了不同的发行包了，它可能叫做 tesseract-ocr 或者 tesseract，直接用对应的命令安装即可。

#### Ubuntu、Debian、Deepin {#ubuntu、debian、deepin}

安装命令如下：

```
sudo apt-get install -y tesseract-ocr libtesseract-dev libleptonica-dev
```

#### CentOS、RedHat {#centos、redhat}

安装命令如下：

```
yum install -y tesseract
```

不同发行版本运行如上命令即可完成 Tesseract 的安装。

安装完成之后便可以调用 tesseract 命令了。

我们查看一下其支持的语言：

```
tesseract --list-langs
```

运行结果示例：

```
List of available languages (3):
eng
osd
equ
```

结果显示其只支持几种语言，如果我们想要安装多国语言还需要安装语言包，官方叫做 tessdata。

tessdata 的下载链接为：[https://github.com/tesseract-ocr/tessdata](https://github.com/tesseract-ocr/tessdata)。

利用 Git 命令将其下载下来并迁移到相关目录即可，不同的版本迁移命令如下：

#### Ubuntu、Debian、Deepin {#ubuntu、debian、deepin}

```
git clone https://github.com/tesseract-ocr/tessdata.git
sudo mv tessdata/* /usr/share/tesseract-ocr/tessdata
```

#### CentOS、RedHat {#centos、redhat}

```
git clone https://github.com/tesseract-ocr/tessdata.git
sudo mv tessdata/* /usr/share/tesseract/tessdata
```

这样就可以将下载下来的语言包全部安装了。

这时我们重新运行列出所有语言的命令：

```
tesseract --list-langs
```

结果如下：

```
List of available languages (107):
afr
amh
ara
asm
aze
aze_cyrl
bel
ben
bod
bos
bul
cat
ceb
ces
chi_sim
chi_tra
...
```

即可发现其列出的语言就多了非常多，比如 chi\_sim 就代表简体中文，这就证明语言包安装成功了。

接下来再安装 Tesserocr 即可，直接使用 Pip 安装：

```
pip3 install tesserocr pillow
```

### 4. Mac下的安装 {#5-mac下的安装}

Mac 下首先使用 Homebrew 安装 Imagemagick 和 Tesseract 库：

```
brew install imagemagick 
brew install tesseract --all-languages
```

接下来再安装 Tesserocr 即可：

```
pip3 install tesserocr pillow
```

这样便完成了 Tesserocr 的安装。

### 5.验证安装

分别测试Tesseract 和 Tesserocr

[测试图片](https://raw.githubusercontent.com/Python3WebSpider/TestTess/master/image.png)：![](/assets/1.2.5.-8.png)用 Tesseract 命令行测试，命令如下：

```
tesseract image.png result -l eng && type result.txt
```

运行结果:

```
Tesseract Open Source OCR Engine v3.05.01 with Leptonica
Python3WebSpider
```



