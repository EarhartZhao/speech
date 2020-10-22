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