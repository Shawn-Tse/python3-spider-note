[官网文档](http://pyquery.readthedocs.io/en/latest/api.html)

### 1. 初始化

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

#### 父节点 {#父节点}

可以用 parent\(\) 方法来获取某个节点的父节点

实例:返回class属性值list当前节点的父节点下的内容

```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''


from pyquery import PyQuery as pq
doc = pq(html)
items = doc('.list')
container = items.parent()
print(type(container))
print(container)
```

运行结果:

```
<class 'pyquery.pyquery.PyQuery'>
<div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
```

#### parents\(\)

parents\(\) 方法会返回所有的祖先节点

```
from pyquery import PyQuery as pq
doc = pq(html)
items = doc('.list')
parents= items.parents()
print(type(parents))
print(parents)
```

结果会有两个节点

运行结果:

```
<class 'pyquery.pyquery.PyQuery'>
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div><div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
```

筛选出指定父节点

实例:筛选出属性值为wrap的父节点

```
from pyquery import PyQuery as pq
doc = pq(html)
items = doc('.list')
parents = items.parents('.wrap')
print(type(parents))
print(parents)
```

运行结果:

```
<class 'pyquery.pyquery.PyQuery'>
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
```

#### 兄弟节点 {#兄弟节点}

要获取兄弟节点可以使用 siblings\(\) 方法

```
from pyquery import PyQuery as pq

doc = pq(html)
li = doc('.list .item-0.active')
print(li.siblings())
```

运行结果:

```
<li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0">first item</li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
```

筛选某个指定兄弟节点

```
from pyquery import PyQuery as pq

doc = pq(html)
li = doc('.list .item-0.active')
print(li.siblings('.active'))
```

运行结果:

```
<li class="item-1 active"><a href="link4.html">fourth item</a></li>
```

### 4. 遍历 {#5-遍历}

对于多个节点的结果，需要遍历来获取了

实例:把每一个 li 节点进行遍历,，需要调用 items\(\) 方法

```
from pyquery import PyQuery as pq

doc = pq(html)
lis = doc('li').items()
print(type(lis))
for li in lis:
    print(li,type(li))
```

运行结果:

```
<class 'generator'>
<li class="item-0">first item</li>
              <class 'pyquery.pyquery.PyQuery'>
<li class="item-1"><a href="link2.html">second item</a></li>
              <class 'pyquery.pyquery.PyQuery'>
<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
              <class 'pyquery.pyquery.PyQuery'>
<li class="item-1 active"><a href="link4.html">fourth item</a></li>
              <class 'pyquery.pyquery.PyQuery'>
<li class="item-0"><a href="link5.html">fifth item</a></li>
          <class 'pyquery.pyquery.PyQuery'>
```

### 5.获取信息 {#6-获取信息}

* 获取属性
* 获取文本

#### 获取属性 {#获取属性}

使用attr\(\) 方法获取属性

```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''


from pyquery import PyQuery as pq

doc = pq(html)
a = doc('.item-0.active a')
print(a,type(a))
print(a.attr('href'))
print(a.attr.href)
```

有两种获取属性方法:

```
a.attr('href')
a.attr.href
```

运行结果:

```
<a href="link3.html"><span class="bold">third item</span></a> <class 'pyquery.pyquery.PyQuery'>
link3.html
link3.html
```

当返回结果包含多个节点时，调用 attr\(\) 方法只会得到第一个节点的属性

```
from pyquery import PyQuery as pq

doc = pq(html)
a = doc('a')
for item in a.items():
    print(item.attr('href'))
```

运行结果:

```
link2.html
link3.html
link4.html
link5.html
```

#### 获取文本 {#获取文本}

调用了 text\(\) 方法，就可以获取其内部的文本信息了，它会忽略掉节点内部包含的所有 HTML，只返回纯文字内容

```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''

from pyquery import PyQuery as pq

doc = pq(html)
a = doc('.item-0.active a')
print(a)
print(a.text())
```

运行结果:

```
<a href="link3.html"><span class="bold">third item</span></a>
third item
```

获取这个节点内部的 HTML 文本，就可以用 html\(\) 方法

```
from pyquery import PyQuery as pq

doc = pq(html)
a = doc('.item-0.active a')
print(a)
print(a.html())
```

运行结果:

```
<a href="link3.html"><span class="bold">third item</span></a>
<span class="bold">third item</span>
```

在多个节点的情况下，html\(\) 方法返回第一个 li 节点的内部 HTML 文本，而 text\(\) 返回所有的 li 节点内部纯文本

### 6. 节点操作 {#7-节点操作}

PyQuery 提供了一系列方法来对节点进行动态修改操作

#### add\_class、remove\_class {#addclass、removeclass}

添加、删除类属性

```
from pyquery import  PyQuery as pq

doc = pq(html)
li = doc('.item-0.active')
print(li)
li.remove_class('active')
print(li)
li.add_class("active")
print(li)
```

返回结果:

```
<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>

<li class="item-0"><a href="link3.html"><span class="bold">third item</span></a></li>

<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
```

#### attr、text、html {#attr、text、html}

```
from pyquery import PyQuery as pq
doc = pq(html)
li = doc('.item-0.active')
print(li)
li.attr('name','link')
print(li)
li.text('chaned item')
print(li)
li.html('<span>changed item</span')
print(li)
```

attr\(\) 方法如果只传入第一个参数属性名，则是获取这个属性值，如果传入第二个参数，可以用来修改属性值，text\(\) 和 html\(\) 方法如果不传参数是获取节点内纯文本和 HTML 文本，如果传入参数则是进行赋值

返回结果:

```
<li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>

<li class="item-0 active" name="link"><a href="link3.html"><span class="bold">third item</span></a></li>

<li class="item-0 active" name="link">chaned item</li>

<li class="item-0 active" name="link"><span>changed item</span></li>
```

#### remove {#remove}

移除

实例:

```
html = '''
<div class="wrap">
    Hello, World
    <p>This is a paragraph.</p>
 </div>
'''

from pyquery import PyQuery as pq

doc = pq(html)
wrap = doc('.wrap')
print(wrap.text())
```

运行结果:

```
Hello, World
This is a paragraph.
```

例子:移除p节点

```
from pyquery import PyQuery as pq

doc = pq(html)
wrap = doc('.wrap')
wrap.find('p').remove()
print(wrap.text())
```

运行结果:

```
Hello, World
```

另外其实还有很多节点操作的方法，比如 append\(\)、empty\(\)、prepend\(\) 等方法，这些函数和 jQuery 的用法是完全一致的，详细的用法可以参考官方文档：

[http://pyquery.readthedocs.io/en/latest/api.html](http://pyquery.readthedocs.io/en/latest/api.html)

### 7.伪类选择器 {#8-伪类选择器}

CSS选择器用法:[http://www.w3school.com.cn/css/index.asp](http://www.w3school.com.cn/css/index.asp)

例如选择第一个节点、最后一个节点、奇偶数节点、包含某一文本的节点等等

实例:

```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''

from pyquery import  PyQuery as pq
doc = pq(html)
# 第一个 li 节点
li = doc('li:first-child')
print(li)
# 最后一个 li 节点
li = doc('li:last-child')
print(li)
# 第二个 li 节点
li = doc('li:nth-child(2)')
print(li)
# 第三个 li 之后的 li 节点
li = doc('li:gt(2)')
print(li)
# 偶数位置的 li 节点
li = doc('li:nth-child(2n)')
print(li)
# 包含 second 文本的 li 节点
li = doc('li:contains(second)')
print(li)
```

运行结果:

```
<li class="item-0">first item</li>
             
<li class="item-0"><a href="link5.html">fifth item</a></li>
         
<li class="item-1"><a href="link2.html">second item</a></li>
             
<li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         
<li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             
<li class="item-1"><a href="link2.html">second item</a></li>
```



