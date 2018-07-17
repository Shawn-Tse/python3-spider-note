# Summary

## Spider-Note

* [Introduction](README.md)

## 1.开发环境配置

* [1.1 python3的安装](1./1.1-python3.md)
  * [1.1.1 windows下的安装](1./1.1.1-windows.md)
  * [1.1.2 Linux下的安装](1./1.1.2-linux.md)
  * 1.1.3 Mac下的安装
* [1.2 请求库的安装](1./12-qing-qiu-ku-de-an-zhuang.md)
  * [1.2.1 requests的安装](1./12-qing-qiu-ku-de-an-zhuang/121-requestsde-an-zhuang.md)
  * [1.2.2 selenium的安装](1./12-qing-qiu-ku-de-an-zhuang/122-seleniumde-an-zhuang.md)
  * [1.2.3 ChromeDriver的安装](1./12-qing-qiu-ku-de-an-zhuang/123-chromedriverde-an-zhuang.md)
  * 1.2.4 GrckoDriver的安装
  * 1.2.5 aiohttp的安装
* [1.3 解析库的安装](1./1.3.md)
  * 1.3.1 lxml的安装
  * 1.3.2 Beautiful Soup的安装
  * 1.3.3 pyquery的安装
  * 1.3.4 tesserocr的安装
* [1.4 数据库的安装](1./14-shu-ju-ku-de-an-zhuang.md)
  * 1.4.1 MySQL的安装
  * 1.4.2 MongoDB的安装
  * 1.4.3 Redis的安装
* 1.5 存储库的安装
  * 1.5.1 PyMySQL的安装
  * 1.5.2 PyMongo的安装
  * 1.5.3 redis-py的安装
  * 1.5.4 RedisDump的安装
* [1.6 Web库的安装](1./16-webku-de-an-zhuang.md)
  * 1.6.1 Flask的安装
  * 1.6.2 Tornado的安装
* 1.7 App爬取相关库的安装
  * 1.7.1 Charles的安装
  * 1.7.2 mitmproxy的安装
  * 1.7.3 Appium的安装
* 1.8 爬虫框架的安装
  * 1.8.1 pyspider的安装
  * 1.8.2 Scrapy的安装
  * 1.8.3 Scrapy-Splash的安装
  * 1.8.4 Scrapy-Splash的安装
* 1.9 部署相关库的安装
  * 1.9.1 Docker的安装
  * 1.9.2 Scrapyd的安装
  * 1.9.3 Scrapyd-Client的安装
  * 1.9.4 Scrapyd API的安装
  * 1.9.5 Scrapyrt的安装
  * 1.9.6 Gerapy的安装

## 2.爬虫基础

* 2.1 HTTP 基本原理
  * 2.1.1 URI和URL
  * 2.1.2 超文本
  * 2.1.3 HTTP和HTTPS
  * 2.1.4 HTTP请求过程
  * 2.1.5 请求
  * 2.1.6 响应
* 2.2 网页基础
  * 2.2.1网页的组成
  * 2.2.2 网页的结构
  * 2.2.3 节点树及节点间的关系
  * 2.2.4 选择器
* [2.3 爬虫的基本原理](2pa-chong-ji-chu/23-pa-chong-de-ji-ben-yuan-li.md)
  * 2.3.1 爬虫概述
  * 2.3.2 能抓怎样的数据
  * 2.3.3 javascript渲染的页面
* 2.4 会话和Cookies
  * 2.4.1 静态网页和动态网页
  * 2.4.2 无状态HTTP
  * 2.4.3 常见误区
* 2.5 代理的基本原理
  * 2.5.1 基本原理
  * 2.5.2 代理的作用
  * 2.5.3 爬虫代理
  * 2.5.4 代理分类
  * 2.5.5 常见代理设置

## 3. 基本库的使用

* 3.1 使用urllib
  * 3.1.1 发送请求
  * 3.1.2 处理异常
  * 3.1.3 解析链接
  * 3.1.4 分析Robots协议
* 3.2 使用requests
  * 3.2.1 基本用法
  * 3.2.2 高级用法
* [3.3 正则表达式](3-ji-ben-ku-de-shi-yong/33-zheng-ze-biao-da-shi.md)
* 3.4 抓取猫眼电影排行

## 4.解析库的使用

* [4.1 使用xpath](4jie-xi-ku-de-shi-yong/41-shi-yong-xpath.md)
* 4.2 使用Beautiful Soup
* 4.3 使用pyquery

## 5.数据存储

* 5.1 文件存储
  * 5.1.1 TXT 文件存储
  * 5.1.2 JSON文件存储
  * 5.1.3 CSV文件存储
* [5.2 关系型数据库存储](5shu-ju-cun-chu/52-guan-xi-xing-shu-ju-ku-cun-chu.md)
  * 5.2.1 MySQL的存储
* 5.3 非关系数据库存储
  * 5.3.1 MongoDB存储
  * 5.3.2 Redis存储

## 6.Ajax数据爬取

* 6.1 什么是Ajax
* 6.2 Ajax分析方法
* 6.3 Ajax结果提取
* [6.4 分析Ajax爬取今日头条街拍美图](6ajaxshu-ju-pa-qu/64-fen-xi-ajax-pa-qu-jin-ri-tou-tiao-jie-pai-mei-tu.md)

## 7.动态渲染页面爬取

* 7.1 Selenium的使用
* [7.2 Splash的使用](7dong-tai-xuan-ran-ye-mian-pa-qu/72-splashde-shi-yong.md)
* [7.3 Splash负载均衡配置](7dong-tai-xuan-ran-ye-mian-pa-qu/73-splashfu-zai-jun-heng-pei-zhi.md)
* [7.4 使用selenium爬取淘宝商品](7dong-tai-xuan-ran-ye-mian-pa-qu/74-shi-yong-selenium-pa-qu-tao-bao-shang-pin.md)

## 8.验证码的识别

* [8.1 图形验证码的识别](8yan-zheng-ma-de-shi-bie/81-tu-xing-yan-zheng-ma-de-shi-bie.md)
* [8.2 极验滑动验证码的识别](8yan-zheng-ma-de-shi-bie/82-ji-yan-hua-dong-yan-zheng-ma-de-shi-bie.md)
* [8.3 点触验证码的识别](8yan-zheng-ma-de-shi-bie/83-dian-hong-yan-zheng-ma-de-shi-bie.md)
* [8.4微博宫格验证码的识别](8yan-zheng-ma-de-shi-bie/84wei-bo-gong-ge-yan-zheng-ma-de-shi-bie.md)

## 9.代理的使用

* 9.1 代理的设置
* 9.2 代理池的维护
* 9.3 付费代理的使用
* 9.4 ADSL拨号代理
* 9.5 使用代理爬取微信公总号文章

## 10.模拟登录

* 10.1 模拟登陆并爬去GitHub
* 10.2 Cookies池的搭建

## 11.App的爬取

* 11.1 Charles的使用
* 11.2 mitmproxy的使用
* 11.3 mitmdump“得到”App电子书信息
* 11.4 Appium的基本使用
* 11.5 Appnium爬取微信朋友圈
* 11.6 Appium+mitmdump爬取京东商品

## 12.pyspider框架的使用

* 12.1 pyspider框架介绍
* 12.2 pyspider的基本使用
* 12.3 pyspider用法详解

## 13.Scrapy框架的使用

* 13.1 scrapy框架介绍
* 13.2 入门
* 13.3 selector的用法
* 13.4 spider的用法
* 13.5 Downloader Middleware的用法
* 13.6 Spider Middleware的用法
* 13.7 Item Pipeline的用法
* 13.8 Scrapy对接Selenium
* 13.9 Scrapy对接Splash
* 13.10 Scrapy通用爬虫
* 13.11 Scrapyrt的使用
* 13.12 Scrapy对接Docker
* 13.13 Scrapy爬取新浪微博

## 14. 分布式爬虫

* 14.1 分布式爬虫原理
* 14.2 Scrapy-Redis源码解析
* 14.3 Scrapy分布式实现
* 14.4 Bloom Filter的对接

## 15.分布式爬虫的部署

* 15.1 Scrapyd分布式部署
* 15.2 Scrapyd-Client的使用
* 15.3 Scrapyd对接Docker
* 15.4 Scrapyd批量部署
* 15.5 Gerapy分布式管理

## 微信采集

* 微信公众号爬虫基本原理
* 使用fiddler抓包分析公众号请求过程
* 抓取微信公众号第一篇文章
* 抓取微信公众号所有历史文章
* 将爬取的文章存储到MongoDB
* 获取文章阅读数、点赞数、评论数、赞赏数

