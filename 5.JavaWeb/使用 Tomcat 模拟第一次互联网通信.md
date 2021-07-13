## 使用 Tomcat 模拟第一次互联网通信

1. 在 tomcat 文件目录下的 `webapps` 目录下新建一个新的文件夹 `myWeb` ，代表一个网站。

![image-20210303195723592](C:%5CUsers%5C30117%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210303195723592.png)

2. 将一些静态文件放入 文件夹下

![image-20210303200001309](C:%5CUsers%5C30117%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210303200001309.png)

3. 启动 Tomcat（在每次开启时最好先使用 `shutdown` 命令将 Tomcat 关闭一下，因为一台电脑不能同时打开两个 Tomcat ，之后在使用命令 `startup`）

![image-20210303200345113](C:%5CUsers%5C30117%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210303200345113.png)

4. 在浏览器中访问 `http://localhost:8080/myWeb/p1.jpg`

![image-20210303200550199](C:%5CUsers%5C30117%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210303200550199.png)



分析过程

1. 当在浏览器中按下回车键的时候，会产生一个 `Http请求协议包`，浏览器会将输入内容写进请求协议包中，请求协议包中分为四层：`请求行` `请求头` `空白行` `请求体`，浏览器会将最基本的请求三要素：`请求地址` `请求方式` 放入 请求行中，将 `请求参数` 放入 请求头中。

![image-20210303202336199](C:%5CUsers%5C30117%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210303202336199.png)

2. 之后浏览器会将 Http请求协议包发给服务端计算机（本机），通过端口号服务端会将请求协议包转交给 Http服务器（即 Tomcat 服务器）。
3. Tomcat 服务器通过请求协议包中的 url 地址知道此时需要 myWeb目录下的 p1.jpg 文件，因此就会在 `webapps`目录下定位到所需资源，之后将资源文件转换为二进制，写入到`Http相应协议包` 中的`响应体`中，并且在`响应头`中设置当前响应体中文件的编译类型，以便之后浏览器对响应体中的二进制数据进行解析。

![image-20210303203528555](C:%5CUsers%5C30117%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210303203528555.png)

4. Tomcat 服务器会将响应协议包推送给浏览器，浏览器解析后将文件内容展现出来。