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
* ![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render4.png)
* 
* 计算出 DOM 树中每个节点的具体样式
*   1.CSS 继承: 每个 DOM 节点都包含有父节点的样式
*   2.样式层叠
  
#### 布局阶段
* 创建布局树
*   1.遍历 DOM 树中的所有可见节点，并把这些节点加到布局树中；
*   2.不可见的节点会被布局树忽略掉
*    ![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render5.png)
*    
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
* ![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render6.png)
* 当图层的绘制列表准备好之后，主线程会把该绘制列表提交（commit）给合成线程
* 合成线程会按照视口附近的图块来优先生成位图，实际生成位图的操作是由栅格化来执行的。所谓栅格化，是指将图块转换为位图
* ![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render7.png)
  
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
* ![](https://earhart-speech.oss-cn-zhangjiakou.aliyuncs.com/session1/img/render8.png)