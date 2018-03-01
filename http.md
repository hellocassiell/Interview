## [一个url的请求过程](https://segmentfault.com/a/1190000006879700)
1. DNS解析
把网址转换为IP地址

2. TCP连接

3. 发送HTTP请求

4. 服务器处理请求并返回HTTP报文

5. 浏览器解析渲染页面

6. 连接结束

输入URL之后，需要寻找到这个url域名的服务器IP，为了找到这个IP，浏览器首先会寻找缓存， 查看缓存中是否有记录，缓存中查找的顺序是浏览器缓存、系统缓存、路由器缓存，缓存中没有则 查找系统的hosts文件中是否有记录，如果没有记录则会查询DNS服务器，得到服务器的IP地址之 后，浏览器根据这个IP以及相应的端口号，（如HTTP协议默认的端口号为80，HTTPS协议的默认 端口号为443，当然可以在url中指定端口号）构造一个HTTP请求，并将这个HTTP包请求封装在 一个TCP包中，（这个HTTP请求报文会包含这次请求的信息，主要是请求方法、请求的说明和请 求附带的数据），这个tcp包依次会经过传输层、网络层、数据链路层、物理层到达服务器，服 务器解析这个请求来做出响应，（我们假定这个url是一个类似谷歌、淘宝这样的网站首页，而 不是简单的文件），服务器返回相应的HTML给浏览器，因为HTML是一个树形结构，浏览器根据 这个HTML来构建DOM树在DOM树的构建过程中如果遇到js脚本和外部js连接，则会停止构建DOM 树来执行和下载相应的代码，这会造成阻塞，这也就是为什么推荐js代码应该放在HTML代码的后 面，之后根据外部样式、内部样式、内联样式构建一个CSS对象模型树（CSSOM树），构建完成之 后和DOM树合并为渲染树，这里主要做的是排除非视觉节点，如script、meta标签和排除display 为none的节点，之后就是进行布局，布局主要是确定各个元素的位置和尺寸，之后就是渲染页面。 因为HTML文件中会含有图片、音频、视频等资源，在解析DOM的过程中，遇到这些都会进行并行下 载，当然浏览器对每个域的并行下载数量有一定的限制，一般是4-6个，当然在这些所有请求中我们 还需要关注的就是缓存，缓存一般通过Cache-Control、Last-Modify、Expires等首部字段控制。 Cache-Control和Expires的区别在于Cache-Control使用相对时间，Expires使用的是基于服务器 端的绝对时间，因为存在时差问题，一般采用Cache-Control，在请求这些有设置了缓存的数据时，会先 查看是否过期，如果没有过期则直接使用本地缓存，过期则请求并在服务器校验文件是否修改，如果上一次 响应设置了ETag值会在这次请求的时候作为If-None-Match的值交给服务器校验，如果一致，继续校验 Last-Modified，没有设置ETag则直接验证Last-Modified，再决定是否返回304



## HTTP状态码及其含义


1XX：信息状态码

100 Continue：客户端应当继续发送请求。这个临时相应是用来通知客户端它的部分请求已经被服务器接收，且仍未被拒绝。客户端应当继续发送请求的剩余部分，或者如果请求已经完成，忽略这个响应。服务器必须在请求万仇向客户端发送一个最终响应

101 Switching Protocols：服务器已经理解力客户端的请求，并将通过Upgrade消息头通知客户端采用不同的协议来完成这个请求。在发送完这个响应最后的空行后，服务器将会切换到Upgrade消息头中定义的那些协议。

2XX：成功状态码

200 OK：请求成功，请求所希望的响应头或数据体将随此响应返回
201 Created：
202 Accepted：
203 Non-Authoritative Information：
204 No Content：
205 Reset Content：
206 Partial Content：

3XX：重定向
300 Multiple Choices：
301 Moved Permanently：
302 Found：
303 See Other：
304 Not Modified：
305 Use Proxy：
306 （unused）：
307 Temporary Redirect：

4XX：客户端错误
400 Bad Request:
401 Unauthorized:
402 Payment Required:
403 Forbidden:
404 Not Found:
405 Method Not Allowed:
406 Not Acceptable:
407 Proxy Authentication Required:
408 Request Timeout:
409 Conflict:
410 Gone:
411 Length Required:
412 Precondition Failed:
413 Request Entity Too Large:
414 Request-URI Too Long:
415 Unsupported Media Type:
416 Requested Range Not Satisfiable:
417 Expectation Failed:

5XX: 服务器错误
500 Internal Server Error:
501 Not Implemented:
502 Bad Gateway:
503 Service Unavailable:
504 Gateway Timeout:
505 HTTP Version Not Supported:

## 常见的网页性能优化方法
- 减少HTTP请求
使用雪碧图、内联图片，合并脚本和样式表。

- 使用内容分发网络（CDN）

- 添加Expires头

- 压缩组件

压缩样式表和脚本，开启gzip压缩大概减少70%的大小

- 样式表放在顶部

- 将脚本放在底部

- 避免CSS表达式

- 使用外部JavaScript和CSS

- 减少DNS查找

- 精简JavaScript

- 避免重定向

网站中除了域名首页外缺少斜杠将引起301重定向，个人测试工作室网站这个重定向消耗的时间在30ms左右

- 删除重复脚本

- 配置ETag

- 使Ajax可缓存