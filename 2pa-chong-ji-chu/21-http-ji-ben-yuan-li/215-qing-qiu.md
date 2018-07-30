### Request

Request，即请求，由客户端向服务端发出。

Request 有四部分内容：

* Request Method\(请求方式\)
* Request URL\(请求链接\)
* Request Headers\(请求头\)
* Request Body\(请求体\)

### Request Method

请求方式中有两种常见的类型:GET和POST

_GET:_从指定的资源请求数据。比如在谷歌中直接搜索花，这便发起了一个get请求，请求的参数会直接包含到url中，如:[https://www.google.com.hk/search?q=花&oq=花&aqs=chrome..69i57j69i60l4.5466j0j7&sourceid=chrome&ie=UTF-8，url中包含了请求的参数信息，这里的参数q就是搜索的关键字](https://www.google.com.hk/search?q=花&oq=花&aqs=chrome..69i57j69i60l4.5466j0j7&sourceid=chrome&ie=UTF-8，url中包含了请求的参数信息，这里的参数q就是搜索的关键字)

_POST:_向指定的资源提交要被处理的数据。POST 请求大多为表单提交发起，如一个登录表单，输入用户名密码，点击登录按钮，这通常会发起一个 POST 请求，其数据通常以 Form Data 即表单的形式传输，不会体现在 URL 中。

GET 和 POST 请求方法有如下区别：

* GET 方式请求中参数是包含在 URL 里面的，数据可以在 URL 中看到，而 POST 请求的 URL 不会包含这些数据，数据都是通过表单的形式传输，会包含在 Request Body 中。
* GET 方式请求提交的数据最多只有 1024 字节，而 POST 方式没有限制。

请求方式以及描述

| 方法 |
| :--- |


|  | 描述 |
| :--- | :--- |
| GET | 请求指定的页面信息，并返回实体主体。 |
| HEAD | 类似于 GET 请求，只不过返回的响应中没有具体的内容，用于获取报头。 |
| POST | 向指定资源提交数据进行处理请求，数据被包含在请求体中。 |
| PUT | 从客户端向服务器传送的数据取代指定的文档的内容。 |
| DELETE | 请求服务器删除指定的页面。 |
| CONNECT | HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器。 |
| OPTIONS | 允许客户端查看服务器的性能。 |
| TRACE | 回显服务器收到的请求，主要用于测试或诊断。 |

本表参考：[http://www.runoob.com/http/http-methods.html](http://www.runoob.com/http/http-methods.html)

