## url输入后发生了什么

### 浏览器查询本地缓存
### DNS解析 (域名系统)
* 输入 http://www.baidu.com
* 读取dns缓存并查询
* 向根域名服务器发送请求并查询
* 向com顶级域名服务器发送请求
* 向 baidu.com 服务器查询
* 获取到IP，根据IP建立TCP连接（三次握手）
* 所有网址真正的解析过程为: . -> .com -> baidu.com. -> www.baidu.com
  
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/dns.png)

### HTTP请求

#### IP连接  网际协议
* 主机A 上层将数据包交给传输层 并添加UDP头
* 传输层再将 IP头附加到数据包上，组成新的 IP数据包，并交给网络层 (此时数据包，包含数据，UDP头，IP头)
* 网络层通过底层物理网络将数据包传输给主机 B
* 数据包被传输到主机 B 的网络层，在这里主机 B 拆开数据包的 IP 头信息，并将拆开来的数据部分交给传输层
* 传输层通过拆开数据包的 UDP 头(端口等)信息，把数据包送达具体应用
  
#### UDP 用户数据包协议

#### TCP连接 传输控制协议

* 建立连接：客户端和服务器总共要发送三个数据包以确认连接的建立（三次握手）
* 传输数据：接收端需要对每个数据包进行确认操作，需要发送确认数据包给发送端。在规定时间内没有接收到确认消息，触发发送端的重发机制。数据包到达接收端后，接收端会按照 TCP 头中的序号为其排序。
* 断开连接：数据传输完毕之后，通过四次挥手保证双方都能断开连接。

![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/http1.png)
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/http2.png)

#### 三次握手
* 客户端：我要进行传输
* 服务端：收到
* 客户端：收到

#### 四次挥手
* 客户端：我没数据传输
* 服务端：收到
* 服务端：我也没数据传输
* 客户端：收到


#### HTTP请求
* 浏览器会向服务器发送请求行，它包括了请求方法、请求 URI和 HTTP 版本协议
* 以请求头形式发送其他一些信息，把浏览器的一些基础信息告诉服务器
* 服务器端处理 HTTP 请求并返回响应行，包括协议版本和状态码
* 服务器向浏览器发送响应头(服务器自身的一些信息,设置cookie)
* 服务器继续发送响应体的数据

![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/request.png)

#### TCP 和 HTTP 的关系示意图
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/http.png)

### 服务器处理并反馈

### 浏览器解析并渲染

![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/process.png)


* 首先，浏览器进程接收到用户输入的 URL 请求，浏览器进程便将该 URL 转发给网络进程。
* 然后，在网络进程中发起真正的 URL 请求。
* 接着网络进程接收到了响应头数据，便解析响应头数据，并将数据转发给浏览器进程。
* 浏览器进程接收到网络进程的响应头数据之后，发送“提交导航 (CommitNavigation)”消息到渲染进程；
* 渲染进程接收到“提交导航”的消息之后，便开始准备接收 HTML 数据，接收数据的方式是直接和网络进程建立数据管道；
* 最后渲染进程会向浏览器进程“确认提交”，这是告诉浏览器进程：“已经准备好接受和解析页面数据了”。
* 浏览器进程接收到渲染进程“提交文档”的消息之后，便开始移除之前旧的文档，然后更新浏览器进程中的页面状态。
* 同一站点（same-site）。根域名加上协议相同

#### 从输入 URL 到页面展示完整流程

![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/process2.png)


### 渲染进程

![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render1.png)


#### HTML、CSS 和 JavaScript 关系图
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render2.png)

* HTML 的内容是由标记和文本组成。标记也称为标签，每个标签都有它自己的语义，浏览器会根据标签的语义来正确展示 HTML 内容
* 如果需要改变 HTML 的字体颜色、大小等信息，就需要用到 CSS。CSS 又称为层叠样式表，是由选择器和属性组成
* JavaScript（简称为 JS），使用它可以使网页的内容“动”起来

#### 渲染流程
* 构建 DOM 树、样式计算、布局阶段、分层、绘制、光栅化和合成


#### 构建 DOM 树 (document)
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render3.png)


#### 样式计算 (document.styleSheets)
* 当渲染引擎接收到 CSS 文本时，会执行一个转换操作，将 CSS 文本转换为浏览器可以理解的结构 styleSheets。
* 转换样式表中的属性值，使其标准化
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render4.png)
* 计算出 DOM 树中每个节点的具体样式
*   1.CSS 继承: 每个 DOM 节点都包含有父节点的样式
*   2.样式层叠
  
#### 布局阶段
* 创建布局树
*   1.遍历 DOM 树中的所有可见节点，并把这些节点加到布局树中；
*   2.不可见的节点会被布局树忽略掉
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render5.png)
* 计算布局树节点的坐标位置,把结果重新写回布局树中
  
#### 分层 (Layers)
* 渲染引擎给页面分了很多图层，这些图层按照一定顺序叠加在一起，形成了最终的页面
* 并不是布局树的每个节点都包含一个图层，如果一个节点没有对应的层，那么这个节点就从属于父节点的图层。
* 拥有层叠上下文属性的元素会被提升为单独的一层。
* 需要剪裁（clip）的地方也会被创建为图层。

#### 图层绘制
* 渲染引擎实现图层的绘制与之类似，会把一个图层的绘制拆分成很多小的绘制指令，然后再把这些指令按照顺序组成一个待绘制列表，让其执行一个简单的绘制操作

#### 栅格化
* 绘制列表只是用来记录绘制顺序和绘制指令的列表，而实际上绘制操作是由渲染引擎中的合成线程来完成的
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render6.png)
* 当图层的绘制列表准备好之后，主线程会把该绘制列表提交（commit）给合成线程
* 合成线程会按照视口附近的图块来优先生成位图，实际生成位图的操作是由栅格化来执行的。所谓栅格化，是指将图块转换为位图
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render7.png)
  
#### 合成和显示 （CSS 的 transform 动画）
* 所有图块都被光栅化，合成线程就会生成一个绘制图块的命令——“DrawQuad”，然后将该命令提交给浏览器进程
* 浏览器进程将其页面内容绘制到内存中，最后再将内存显示在屏幕上


#### 完整的渲染流程

* 渲染进程将 HTML 内容转换为能够读懂的 DOM 树结构。
* 渲染引擎将 CSS 样式表转化为浏览器可以理解的 styleSheets，计算出 DOM 节点的样式。
* 创建布局树，并计算元素的布局信息。
* 对布局树进行分层，并生成分层树。为每个图层生成绘制列表，并将其提交到合成线程。
* 合成线程将图层分成图块，并在光栅化线程池中将图块转换成位图。
* 合成线程发送绘制图块命令 DrawQuad 给浏览器进程。
* 浏览器进程根据 DrawQuad 消息生成页面，并显示到显示器上。
![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render8.png)


### 完整的解析

> 1，用户输入url并回车  
> 2，浏览器进程检查url，组装协议，构成完整的url  
> 3，浏览器进程通过进程间通信（IPC）把url请求发送给网络进程  
> 4，网络进程接收到url请求后检查本地缓存是否缓存了该请求资源，如果有则将该资源返回给浏览器进程  
> 5，如果没有，网络进程向web服务器发起http请求（网络请求），请求流程如下：  
>     5.1 进行DNS解析，获取服务器ip地址，端口  
>     5.2 利用ip地址和服务器建立tcp连接  
>     5.3 构建请求头信息  
>     5.4 发送请求头信息 
>     5.5 服务器响应后，网络进程接收响应头和响应信息，并解析响应内容  
> 6，网络进程解析响应流程；  
>     6.1 检查状态码，如果是301/302，则需要重定向，从Location自动中读取地址，重新进行第4步 
>         （301/302跳转也会读取本地缓存吗？这里有个疑问），如果是200，则继续处理请求。  
>     6.2 200响应处理：  
>         检查响应类型Content-Type，如果是字节流 类型，则将该请求提交给下载管理器，该导航流程结束，不再进行 
>         后续的渲染，如果是html则通知浏览器进程准备渲染进程准备进行渲染。  
> 7，准备渲染进程  
>     7.1 浏览器进程检查当前url是否和之前打开的渲染进程根域名是否相同，如果相同，则复用原来的进程，如果不同，则开启新的渲染进程  
> 8，传输数据、更新状态  
>     8.1 渲染进程准备好后，浏览器向渲染进程发起“提交文档”的消息，渲染进程接收到消息和网络进程建立传输数据的“管道”  
>     8.2 渲染进程接收完数据后，向浏览器发送“确认提交”  
>     8.3 浏览器进程接收到确认消息后更新浏览器界面状态：安全、地址栏url、前进后退的历史状态、更新web页面  