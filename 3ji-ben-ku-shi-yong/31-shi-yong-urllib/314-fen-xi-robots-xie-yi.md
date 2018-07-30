### 1.说明

利用 Urllib 的 robotparser 模块我们可以实现网站 Robots 协议的分析

### 2. Robots协议 {#1-robots协议}

Robots 协议也被称作爬虫协议、机器人协议，它的全名叫做网络爬虫排除标准（Robots Exclusion Protocol），用来告诉爬虫和搜索引擎哪些页面可以抓取，哪些不可以抓取。它通常是一个叫做 robots.txt 的文本文件，放在网站的根目录下。

当搜索爬虫访问一个站点时，它首先会检查下这个站点根目录下是否存在 robots.txt 文件，如果存在，搜索爬虫会根据其中定义的爬取范围来爬取。如果没有找到这个文件，那么搜索爬虫便会访问所有可直接访问的页面。

例如:

```
https://blog.csdn.net/robots.txt
```

robots.txt内容:

```
User-agent: *
Disallow: /css/
Disallow: /images/
Disallow: /content/
Disallow: /ui/
Disallow: /js/

Sitemap: https://blog.csdn.net/s/sitemap/pcsitemapindex.xml
```

User-agent 描述了搜索爬虫的名称，在这里将值设置为 \*，则代表该协议对任何的爬取爬虫有效

Disallow 指定了不允许抓取的目录，比如上述例子中设置为/则代表不允许抓取所有页面。

Allow 一般和 Disallow 一起使用，一般不会单独使用，用来排除某些限制，现在我们设置为 /public/ ，起到的作用是所有页面不允许抓取，但是 public 目录是可以抓取的

### 3. 爬虫名称 {#2-爬虫名称}

大家可能会疑惑，爬虫名是哪儿来的？为什么就叫这个名？其实它是有固定名字的了，比如百度的就叫做 BaiduSpider，下面的表格列出了一些常见的搜索爬虫的名称及对应的网站：

| 爬虫名称 | 名称 | 网站 |
| :--- | :--- | :--- |
| BaiduSpider | 百度 | www.baidu.com |
| Googlebot | 谷歌 | www.google.com |
| 360Spider | 360搜索 | www.so.com |
| YodaoBot | 有道 | www.youdao.com |
| ia\_archiver | Alexa | www.alexa.cn |
| Scooter | altavista | www.altavista.com |



