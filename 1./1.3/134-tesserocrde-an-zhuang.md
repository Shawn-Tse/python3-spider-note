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

如果报错

需要使用whl安装，并且需要安装Microsoft Visual C++ 14.0.exe

[下载地址](https://pan.baidu.com/s/1lL3WVCE2T-4zQJbjloP6-w)

```
首先切换到有whl的目录

然后通过pip安装
pip install tesserocr-2.2.2-cp36-cp36m-win_amd64.whl

在这之前需要安装Microsoft Visual C++ 14.0.exe
```



