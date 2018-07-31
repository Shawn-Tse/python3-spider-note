### 1.说明

XPath，全称 XML Path Language，即 XML 路径语言，它是一门在XML文档中查找信息的语言。XPath 最初设计是用来搜寻XML文档的，但是它同样适用于 HTML 文档的搜索

### 2.相关链接

官方文档:[https://www.w3.org/TR/xpath/](https://www.w3.org/TR/xpath/)

### 3.XPath常用规则 {#2-xpath常用规则}

| 表达式 | 描述 |
| :--- | :--- |
| nodename | 选取此节点的所有子节点 |
| / | 从当前节点选取直接子节点 |
| // | 从当前节点选取子孙节点 |
| . | 选取当前节点 |
| .. | 选取当前节点的父节点 |
| @ | 选取属性 |

### 4. 实例引入 {#4-实例引入}

```
from lxml import etree

content = '''
<div>
    <ul>
         <li class="item-0"><a href="link1.html">first item</a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </ul>
 </div>
'''
# 调用etree模块的HTML类构造一个XPath解析对象
html = etree.HTML(content)
result = etree.tostring(html)
print(result.decode('utf-8'))
```

HTML 文本中的最后一个 li 节点是没有闭合的，但是 etree 模块可以对 HTML 文本进行自动修正

运行结果:

```
<html><body><div>
    <ul>
         <li class="item-0"><a href="link1.html">first item</a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </li></ul>
 </div>
</body></html>
```

可以直接读取文本进行解析

```
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = etree.tostring(html)
print(result.decode('utf-8'))
```

test.html内容

```
<div>
    <ul>
         <li class="item-0"><a href="link1.html">first item</a></li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-inactive"><a href="link3.html">third item</a></li>
         <li class="item-1"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a>
     </ul>
 </div>
```

解析后结果:

```
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3.org/TR/REC-html40/loose.dtd">
<html><body><div>&#13;
    <ul>&#13;
         <li class="item-0"><a href="link1.html">first item</a></li>&#13;
         <li class="item-1"><a href="link2.html">second item</a></li>&#13;
         <li class="item-inactive"><a href="link3.html">third item</a></li>&#13;
         <li class="item-1"><a href="link4.html">fourth item</a></li>&#13;
         <li class="item-0"><a href="link5.html">fifth item</a>&#13;
     </li></ul>&#13;
 </div></body></html>
```

### 5.所有结点

利用//开头的xpath规则选取所有符合要求的节点

```
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//*')
print(result)
```

\*代表匹配所有的结点

运行结果:

```
[<Element html at 0x185591fd548>, <Element body at 0x185591fd688>, <Element div at 0x185591fd6c8>, <Element ul at 0x185591fd708>, <Element li at 0x185591fd748>, <Element a at 0x185591fd7c8>, <Element li at 0x185591fd808>, <Element a at 0x185591fd848>, <Element li at 0x185591fdac8>, <Element a at 0x185591fd788>, <Element li at 0x185591fdb08>, <Element a at 0x185591fdb48>, <Element li at 0x185591fdb88>, <Element a at 0x185591fdbc8>]
```

只获取li节点

要选取所有 li 节点可以使用 //，然后直接加上节点的名称即可，调用时直接调用 xpath\(\) 方法即可提取

```
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li')
print(result)
```

### 6.子结点

通过/或者//查找子结点或子孙子结点

实例:查找li节点下的所有a子节点

```
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li/a')
print(result)
```

运行结果:

```
[<Element a at 0x1dc63e8d708>, <Element a at 0x1dc63e8d748>, <Element a at 0x1dc63e8d788>, <Element a at 0x1dc63e8d7c8>, <Element a at 0x1dc63e8d808>]
```

实例:查找ul节点下的所有的子孙a节点

```
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li//a')
print(result)
```

运行结果与上个例子是相同的

一定要注意/和//的区别，/是获取直接子节点，//是获取子孙节点

### 7. 父节点 {#7-父节点}

可以通过..来获取父节点

实例:获取href 是 link4.html 的 a 节点的父节点的class属性

```
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//a[@href="link4.html"]/../@class')
print(result)
```

运行结果:

```
['item-1']
```

也可以通过 parent:: 来获取父节点

实例:

```
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//a[@href="link4.html"]/parent::*/@class')
```

### 8. 属性匹配 {#8-属性匹配}

@符号可以进行匹配属性

实例:

```
from lxml import etree

html = etree.parse('test.html',etree.HTMLParser())
result = html.xpath('//li[@class="item-0"]')
print(result)
```

运行结果为:

```
[<Element li at 0x1e85c0bd748>, <Element li at 0x1e85c0bd788>]

```



