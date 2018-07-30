当在浏览器输入一个url，回车后，便可看到该网页的内容，实际上过程是浏览器向该网站的服务器发送一个Request\(请求\)，网站的服务器接收之后，然后返回与之对应的一个Response\(响应\)，然后返回给浏览器，response响应中包含了页面的源代码等内容，浏览器解析会后便将网页给呈现出来

![](/assets/2.1.4-1.png)![](/assets/2.1.4-2.png)按下F12，然后点击network面板，便可看到一次发送请求和接收响应之间的过程

每列属性名称及含义：

* Name，即 Request 的名称。
* Status，即 Response 的状态码。通过状态码我们可以判断发送了 Request 之后是否得到了正常的 Response。
* Type，即 Request 请求的文档类型。
* Initiator，即请求源。
* Size，即从服务器下载的文件和请求的资源大小。
* Time，即发起 Request 到获取到 Response 所用的总时间。
* Timeline，即网络请求的可视化瀑布流。



