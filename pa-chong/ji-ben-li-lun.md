# 基本理论

---

## HTTP协议

协议，通俗来讲就是一个约定，客户端和服务端两方面进行数据交换时规定的数据格式。http协议包括

![](/assets/http协议.png)

---

## 请求行

HTTP1.0定义了三种请求方法： GET, POST 和 HEAD方法。

HTTP1.1新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法。

最常见的是GET和POST请求。

| 序号 | 方法 | 描述 |
| :--- | :--- | :--- |
| 1 | **GET** | 请求指定的页面信息，并返回实体主体。请求参数在url里 |
| 2 | HEAD | 类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头 |
| 3 | **POST** | 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。 |
| 4 | PUT | 从客户端向服务器传送的数据取代指定的文档的内容。 |
| 5 | DELETE | 请求服务器删除指定的页面。 |
| 6 | CONNECT | HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。 |
| 7 | OPTIONS | 允许客户端查看服务器的性能。 |
| 8 | TRACE | 回显服务器收到的请求，主要用于测试或诊断。常用的主要有两种get和post两种 |

---

#### 请求头信息

常用的参数是Cookie，存放登录信息，所以如果想爬取用户登录之后才能操作的数据，在浏览器上登录后获取这个参数的值，在代码中发送请求时带上这个值就可以了。

![](/assets/详情.jpg)

---

#### 请求体

存放请求参数，对于Get方法而言，不需要这一部分，对于Post方法，请求的参数不放在URL中，放在这里。

---

#### 返回头

| 应答头 | 说明 |
| :--- | :--- |
| Allow | 服务器支持哪些请求方法（如GET、POST等）。 |
| Content-Encoding | 文档的编码（Encode）方法。只有在解码之后才可以得到Content-Type头指定的内容类型。利用gzip压缩文档能够显著地减少HTML文档的下载时间。Java的GZIPOutputStream可以很方便地进行gzip压缩，但只有Unix上的Netscape和Windows上的IE 4、IE 5才支持它。因此，Servlet应该通过查看Accept-Encoding头（即request.getHeader\("Accept-Encoding"\)）检查浏览器是否支持gzip，为支持gzip的浏览器返回经gzip压缩的HTML页面，为其他浏览器返回普通页面。 |
| Content-Length | 表示内容长度。只有当浏览器使用持久HTTP连接时才需要这个数据。如果你想要利用持久连接的优势，可以把输出文档写入 ByteArrayOutputStream，完成后查看其大小，然后把该值放入Content-Length头，最后通过byteArrayStream.writeTo\(response.getOutputStream\(\)发送内容。 |
| Content-Type | 表示后面的文档属于什么MIME类型。Servlet默认为text/plain，但通常需要显式地指定为text/html。由于经常要设置Content-Type，因此HttpServletResponse提供了一个专用的方法setContentType。 |
| Date | 当前的GMT时间。你可以用setDateHeader来设置这个头以避免转换时间格式的麻烦。 |
| Expires | 应该在什么时候认为文档已经过期，从而不再缓存它？ |
| Last-Modified | 文档的最后改动时间。客户可以通过If-Modified-Since请求头提供一个日期，该请求将被视为一个条件GET，只有改动时间迟于指定时间的文档才会返回，否则返回一个304（Not Modified）状态。Last-Modified也可用setDateHeader方法来设置。 |
| Location | 表示客户应当到哪里去提取文档。Location通常不是直接设置的，而是通过HttpServletResponse的sendRedirect方法，该方法同时设置状态代码为302。 |
| Refresh | 表示浏览器应该在多少时间之后刷新文档，以秒计。除了刷新当前文档之外，你还可以通过setHeader\("Refresh", "5; URL=http://host/path"\)让浏览器读取指定的页面。 注意这种功能通常是通过设置HTML页面HEAD区的＜META HTTP-EQUIV="Refresh" CONTENT="5;URL=http://host/path"＞实现，这是因为，自动刷新或重定向对于那些不能使用CGI或Servlet的HTML编写者十分重要。但是，对于Servlet来说，直接设置Refresh头更加方便。  注意Refresh的意义是"N秒之后刷新本页面或访问指定页面"，而不是"每隔N秒刷新本页面或访问指定页面"。因此，连续刷新要求每次都发送一个Refresh头，而发送204状态代码则可以阻止浏览器继续刷新，不管是使用Refresh头还是＜META HTTP-EQUIV="Refresh" ...＞。  注意Refresh头不属于HTTP 1.1正式规范的一部分，而是一个扩展，但Netscape和IE都支持它。 |
| Server | 服务器名字。Servlet一般不设置这个值，而是由Web服务器自己设置。 |
| Set-Cookie | 设置和页面关联的Cookie。Servlet不应使用response.setHeader\("Set-Cookie", ...\)，而是应使用HttpServletResponse提供的专用方法addCookie。参见下文有关Cookie设置的讨论。 |
| WWW-Authenticate | 客户应该在Authorization头中提供什么类型的授权信息？在包含401（Unauthorized）状态行的应答中这个头是必需的。例如，response.setHeader\("WWW-Authenticate", "BASIC realm=＼"executives＼""\)。 注意Servlet一般不进行这方面的处理，而是让Web服务器的专门机制来控制受密码保护页面的访问（例如.htaccess）。 |

 

 

 

---

#### 拓展：

#### HTTP1.0、HTTP1.1和HTTP2.0

* http1.0不支持长连接，每次访问都需要重新进行TCP协议的三次握手，可以通过keep-alive参数设置。

* http1.1

  * 默认支持长连接。
  * 节省带宽。支持只发送header信息\(不带任何body信息\)，如果服务器认为客户端有权限请求服务器，则返回100，否则返回401。客户端如果接受到100，才开始把请求body发送到服务器。
  * 支持HOST域

* HTTP2.0

  * 多路复用。使用了多路复用的技术，做到同一个连接并发处理多个请求，而且并发请求的数量比HTTP1.1大了好几个数量级。

  * 首部压缩。HTTP2.0使用HPACK算法对header的数据进行压缩，这样数据体积小了，在网络上传输就会更快。

  * 服务器推送。在HTTP/2中，服务器可以对客户端的一个请求发送多个响应。

#### **Websocket：**

双工通信，解决只能有客户端发起请求的问题。轮询的效率低，非常浪费资源（因为必须不停连接，或者 HTTP 连接始终打开）

应用场景：实时数据抓取（比如斗鱼弹幕数据）

---

**参考资料：**

[关于HTTP协议，一篇就够了](https://www.cnblogs.com/ranyonsue/p/5984001.html)

[HTTP请求行、请求头、请求体详解](https://blog.csdn.net/u010256388/article/details/68491509)

[HTTP1.0 HTTP 1.1 HTTP 2.0主要区别](https://blog.csdn.net/linsongbin1/article/details/54980801)

[HTTP/2.0 相比1.0有哪些重大改进？](https://www.zhihu.com/question/34074946)

[深入研究：HTTP2 的真正性能到底如何](https://segmentfault.com/a/1190000007219256)

[WebSocket 教程](http://www.ruanyifeng.com/blog/2017/05/websocket.html)

[抓取斗鱼直播弹幕](https://blog.csdn.net/bfboys/article/details/52853041)

