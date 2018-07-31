### 1. 初始化 {#2-初始化}

PyQuery 初始化的时候也需要传入 HTML 数据源来初始化一个操作对象，它的初始化方式有多种，比如直接传入字符串，传入 URL，传文件名

#### 字符串初始化 {#字符串初始化}

```
html = '''
<div>
    <ul>
         <li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     </ul>
 </div>
'''

from pyquery import PyQuery as pq

doc = pq(html)
print(doc('li'))
```

运行结果:

```
<li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
```

#### URL初始化 {#url初始化}

传入指定参数为 url

```
from pyquery import PyQuery as pq

doc = pq(url='https://github.com/CoderAngle')
print(doc('title'))
```

运行结果:

```
<title>CoderAngle · GitHub</title>
```

等同于下面这个:

使用requests模块访问url然后返回源码

```
from pyquery import PyQuery as pq
import requests

doc = pq(requests.get('https://github.com/CoderAngle').text)
print(doc('title'))
```

#### 文件初始化 {#文件初始化}

传入参数指定为 filename

```
from pyquery import PyQuery as pq

doc = pq(filename='test.html')
print(doc('li'))
```

### 2. 基本CSS选择器 {#3-基本css选择器}

实例:

```
html = '''
<div id="container">
    <ul class="list">
         <li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     </ul>
 </div>
'''

from pyquery import PyQuery as pq

doc = pq(html)
print(doc('#container .list li'))
print(type(doc('#container .list li')))
```

运行结果:

```
<li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     
<class 'pyquery.pyquery.PyQuery'>
```



