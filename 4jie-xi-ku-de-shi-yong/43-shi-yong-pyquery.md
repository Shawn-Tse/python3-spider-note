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

### 3. 查找节点 {#4-查找节点}

pyquery的常用的查询函数，这些函数和 jQuery 中的函数用法完全相同

#### 子节点 {#子节点}

查找子节点需要用到 find\(\) 方法，传入的参数是 CSS 选择器

```
from pyquery import PyQuery as pq

doc = pq(html)
items = doc('.list')
print(type(items))
print(items)
list_itmes = items.find('li')
print(type(list_itmes))
print(list_itmes)
```

运行结果:

```
<class 'pyquery.pyquery.PyQuery'>
<ul class="list">
         <li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     </ul>

<class 'pyquery.pyquery.PyQuery'>
<li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>()
```

#### children\(\)

find\(\) 的查找范围是节点的所有子孙节点，而如果我们只想查找子节点，那可以用 children\(\) 方法

```
from pyquery import PyQuery as pq

doc = pq(html)
lis = doc.children()
print(type(lis))
print(lis)
```

运行结果:

```
<class 'pyquery.pyquery.PyQuery'>
<ul class="list">
         <li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     </ul>
```

实例:筛选出子节点class属性值为active

```
from pyquery import PyQuery as pq

items = pq(html)
lis = items.children('.list .active')
print(type(lis))
print(lis)

```

运行结果:

```
<class 'pyquery.pyquery.PyQuery'>
<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
<li class="item-1 active"><a href="link4.html">fourth item</a></li>
```



