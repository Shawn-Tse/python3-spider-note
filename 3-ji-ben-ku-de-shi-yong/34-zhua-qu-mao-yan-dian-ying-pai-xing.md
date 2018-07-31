### 实战演练

利用 Requests 和正则表达式来抓取猫眼电影 TOP100 的相关内容

### 1.目标

猫眼电影地址:http://maoyan.com/board/4

需要:要提取出猫眼电影 TOP100 榜的电影名称、时间、评分、图片等信息,提取的结果我们以文件形式保存下来

### 2.准备

确保[安装requests库](/1.kaifahuanjing/12-qing-qiu-ku-de-an-zhuang/121-requestsde-an-zhuang.md)

### 3.抓取分析

打开http://maoyan.com/board/4可以查看榜单信息

![](/assets/3.4-3.png)

在图中可以清楚地看到影片的信息，页面中显示的信息有影片名称、主演、上映时间、上映地区、评分、图片等

之后点击下一页

![](/assets/3.4-2.png)可以发现http://maoyan.com/board/4?offset=10比之前的url多了一个参数offset，参数值为10，目前显示的排行数据11~20，可以判断offset是一个偏移量的参数再点击下一页，发现页面的 URL 变成了：[http://maoyan.com/board/4?offset=20](http://maoyan.com/board/4?offset=20)，参数 offset 变成了 20，而显示的结果是排行 21-30 的电影

可以判断offset是一个偏移量，如果偏移值为n，则当前页面的序号为n+1到n+10，这样就可以更根据offset获取top100的所有电影信息了

### 4.抓取首页

定义一个get_first_page



