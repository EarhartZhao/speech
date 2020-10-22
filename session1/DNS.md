### DNS解析 (域名系统)
* 输入 http://www.baidu.com
* 读取dns缓存并查询
* 向根域名服务器发送请求并查询
* 向com顶级域名服务器发送请求
* 向 baidu.com 服务器查询
* 获取到IP，根据IP建立TCP连接（三次握手）
* 所有网址真正的解析过程为: . -> .com -> baidu.com. -> www.baidu.com
  
![](./img/dns.png)