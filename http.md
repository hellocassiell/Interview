## [一个url的请求过程](https://segmentfault.com/a/1190000006879700)
1. DNS解析
把网址转换为IP地址

2. TCP连接

3. 发送HTTP请求

4. 服务器处理请求并返回HTTP报文

5. 浏览器解析渲染页面

6. 连接结束



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