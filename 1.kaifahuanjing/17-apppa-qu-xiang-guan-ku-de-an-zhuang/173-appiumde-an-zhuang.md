### 1.说明

Appium是移动端的自动化测试工具，可以利用它驱动Android等设备完成自动化测试，比如模拟点击、滑动、输入等操作

### 2. 相关链接 {#1-相关链接}

* GitHub：[https://github.com/appium/appium](https://github.com/appium/appium)
* 官方网站：[http://appium.io](http://appium.io/)
* 官方文档：[http://appium.io/introduction.html](http://appium.io/introduction.html)
* 下载链接：[https://github.com/appium/appium-desktop/releases](https://github.com/appium/appium-desktop/releases)
* Python Client：[https://github.com/appium/python-client](https://github.com/appium/python-client)

### 3. 安装Appium {#2-安装appium}

首先我们需要安装 Appium，Appium 负责驱动移动端来完成一系列操作，对 iOS 设备来说，它使用苹果的 UIAutomation 来实现驱动，对于 Android 来说，它使用 UiAutomator 和 Selendroid 来实现驱动。

同时 Appium 也相当于一个服务器，可以向 Appium 发送一些操作指令，Appium 就会根据不同的指令对移动设备进行驱动，完成不同的动作。

安装 Appium 有两种方式，一种是直接下载安装包 Appium Desktop 来安装，另外一种是通过 Node.js 来安装.

### Appium Desktop

Appium Desktop支持全平台的安装，下载地址:[https://github.com/appium/appium-desktop/releases](https://github.com/appium/appium-desktop/releases)![](/assets/1.7.3-1.png)windows平台可以下载exe如[**appium-desktop-web-setup-1.6.2.exe**](https://github.com/appium/appium-desktop/releases/download/v1.6.2/appium-desktop-web-setup-1.6.2.exe),Mac 平台可以下载 dmg 安装包如 [**Appium-1.6.2.dmg**](https://github.com/appium/appium-desktop/releases/download/v1.6.2/Appium-1.6.2.dmg)，Linux 平台可以选择下载源码



### Node.js

安装Node.js

安装方式参见:http://www.runoob.com/nodejs/nodejs-install-setup.html



