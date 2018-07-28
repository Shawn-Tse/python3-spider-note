### 1.安装

```
pip install bs4
或者
pip install beautifulsoup4
```

### 2.验证安装

安装完成后，运行代码验证是否安装成功

```
from bs4 import BeautifulSoup
soup = BeautifulSoup("<h1>angle</h1>",'lxml')
print(soup.h1.string)
```

运行结果:

```
angle
```

如果结果一样，就证明安装成功

