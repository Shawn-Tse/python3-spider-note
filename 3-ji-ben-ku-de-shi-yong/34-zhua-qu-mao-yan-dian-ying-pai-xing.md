### 实战演练

利用 Requests 和正则表达式来抓取猫眼电影 TOP100 的相关内容

### 1.目标

猫眼电影地址:[http://maoyan.com/board/4](http://maoyan.com/board/4)

需要:要提取出猫眼电影 TOP100 榜的电影名称、时间、评分、图片等信息,提取的结果我们以文件形式保存下来

### 2.准备

确保[安装requests库](/1.kaifahuanjing/12-qing-qiu-ku-de-an-zhuang/121-requestsde-an-zhuang.md)

### 3.抓取分析

打开[http://maoyan.com/board/4可以查看榜单信息](http://maoyan.com/board/4可以查看榜单信息)

![](/assets/3.4-3.png)

在图中可以清楚地看到影片的信息，页面中显示的信息有影片名称、主演、上映时间、上映地区、评分、图片等

之后点击下一页

![](/assets/3.4-2.png)可以发现[http://maoyan.com/board/4?offset=10比之前的url多了一个参数offset，参数值为10，目前显示的排行数据11~20，可以判断offset是一个偏移量的参数再点击下一页，发现页面的](http://maoyan.com/board/4?offset=10比之前的url多了一个参数offset，参数值为10，目前显示的排行数据11~20，可以判断offset是一个偏移量的参数再点击下一页，发现页面的) URL 变成了：[http://maoyan.com/board/4?offset=20](http://maoyan.com/board/4?offset=20)，参数 offset 变成了 20，而显示的结果是排行 21-30 的电影

可以判断offset是一个偏移量，如果偏移值为n，则当前页面的序号为n+1到n+10，这样就可以更根据offset获取top100的所有电影信息了

### 4.抓取首页

定义一个get\_first\_page\(\)函数方法，实现抓取首页，代码实现

```
import requests
import time

headers = {
'Cookie': 'uuid_n_v=v1; uuid=AF3D1220948011E8B2AA9FA8B2681702285785F0A8C6440893B814F988D9E847; _csrf=7e74e8ba9e19ad80506d12f9c59ca4d0663c09568af4bd8ab119e7fa42cf0406; _lxsdk_cuid=164eec2d003c8-08f976660a5271-2711f38-144000-164eec2d003c8; _lxsdk=AF3D1220948011E8B2AA9FA8B2681702285785F0A8C6440893B814F988D9E847; __mta=210171562.1533014102076.1533015465347.1533015624851.12; _lxsdk_s=164eec2d004-581-309-f99%7C%7C29',
'Host': 'maoyan.com',
'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.15 Safari/537.36',
}

# 获取首页
def get_first_page(url):
    time.sleep(2)
    response = requests.get(url,headers=headers)
    if response.status_code == requests.codes.ok:
        return response.text
    return None

# 主程序
def main():
    url = "http://maoyan.com/board/4"
    html = get_first_page(url)
    print(html)

if __name__ == "__main__":
    main()
```

tips:一定要加上请求头，不然猫眼网站会禁止访问

### 5. 正则提取 {#5-正则提取}

现在抓取了首页，需要进一步抓取相关信息，接下来回到网页看一下页面的真实源码，在开发者工具中 Network 监听，然后查看一下源代码，注意这里不要在 Elements 选项卡直接查看源码，此处的源码可能经过 JavaScript 的操作而和原始请求的不同，需要从Network选项卡部分查看原始请求得到的源码

![](/assets/3.4-5.png)

先看下一个电影的相关内容

```
<dd>
                        <i class="board-index board-index-1">1</i>
    <a href="/films/1203" title="霸王别姬" class="image-link" data-act="boarditem-click" data-val="{movieId:1203}">
      <img src="//ms0.meituan.net/mywww/image/loading_2.e3d934bf.png" alt="" class="poster-default" />
      <img data-src="http://p1.meituan.net/movie/20803f59291c47e1e116c11963ce019e68711.jpg@160w_220h_1e_1c" alt="霸王别姬" class="board-img" />
    </a>
    <div class="board-item-main">
      <div class="board-item-content">
              <div class="movie-item-info">
        <p class="name"><a href="/films/1203" title="霸王别姬" data-act="boarditem-click" data-val="{movieId:1203}">霸王别姬</a></p>
        <p class="star">
                主演：张国荣,张丰毅,巩俐
        </p>
<p class="releasetime">上映时间：1993-01-01(中国香港)</p>    </div>
    <div class="movie-item-number score-num">
<p class="score"><i class="integer">9.</i><i class="fraction">6</i></p>        
    </div>

      </div>
    </div>

                </dd>
```

现在需要从这段里面提取需要的信息，书写正则表达式

```
排名信息:<i.*?board-index.*?>(.*?)</i>'

进一步编写:

封面图片:<i.*?board-index.*?>(.*?)</i>.*?data-src="(.*?)"

继续:

电影名称<i.*?board-index.*?>(.*?)</i>.*?data-src="(.*?)".*?a.*?>(.*?)</a>

依次类推:

所有信息:<i.*?board-index.*?>(.*?)</i>.*?data-src="(.*?)".*?a.*?>(.*?)</a>.*?star.*?>(.*?)</p>.*?releasetime.*?>(.*?)</p>.*?integer.*?>(.*?)</i>.*?fraction.*?>(.*?)</i>.*?</dd>
```



