[html](#htm)

[css](#css)

[js](#js)

[其他](#其他)

<h2 id="html">html</h2>

* 页面导入样式时，使用link和@import有什么区别？

 ```
（1）link属于XHTML标签，除了加载CSS外，还能用于定义RSS, 定义rel连接属性等作用；而@import是CSS提供的，只能用于加载CSS;
	ps:只有 rel 属性的 "stylesheet" 值得到了所有浏览器的支持。其他值只得到了部分地支持。

（2）页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;

（3）import是CSS2.1 提出的，只在IE5以上才能被识别，而link是XHTML标签，无兼容问题;

 ```
* html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？

```
* HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
      绘画 canvas;
      用于媒介回放的 video 和 audio 元素;
      本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
      sessionStorage 的数据在浏览器关闭后自动删除;
      语意化更好的内容元素，比如 article、footer、header、nav、section;
      表单控件，calendar、date、time、email、url、search;
      新的技术webworker, websocket, Geolocation;

  移除的元素：
      纯表现的元素：basefont，big，center，font, s，strike，tt，u;
      对可用性产生负面影响的元素：frame，frameset，noframes；

* 支持HTML5新标签：
     IE8/IE7/IE6支持通过document.createElement方法产生的标签，
     可以利用这一特性让这些浏览器支持HTML5新标签，
     浏览器支持新标签后，还需要添加标签默认的样式。

     当然也可以直接使用成熟的框架、比如html5shim;
     <!--[if lt IE 9]>
        <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
     <![endif]-->

* 如何区分HTML5： DOCTYPE声明\新增的结构元素\功能元素

```

* HTML5的离线储存怎么使用及工作原理

```
在用户没有与因特网连接时，可以正常访问站点或应用，在用户与因特网连接时，更新用户机器上的缓存文件。
原理：HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。


如何使用：
1、页面头部像下面一样加入一个manifest的属性；
  <html manifest = "cache.manifest">
    ...
  </html>
2、在cache.manifest文件的编写离线存储的资源；
   CACHE MANIFEST
   #v0.11
   CACHE:
   js/app.js
   css/style.css
   NETWORK:
   resourse/logo.png
   FALLBACK:
   / /offline.html
3、在离线状态时，操作window.applicationCache进行需求实现。

在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
离线的情况下，浏览器就直接使用离线存储的资源。

```
详细的使用请参考：

[HTML5 离线缓存-manifest简介](http://yanhaijing.com/html/2014/12/28/html5-manifest/)

[有趣的HTML5：离线存储](https://segmentfault.com/a/1190000000732617)

* HTML5的form如何关闭自动完成功能？

```
给不想要提示的 form 或某个 input 设置为 autocomplete=off。
```
* 如何实现浏览器内多个标签页之间的通信? (阿里)

```
WebSocket,也可以调用localstorge、cookies等本地存储方式；

localstorge另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，
我们通过监听事件，控制它的值来进行页面信息通信；
注意quirks：Safari 在无痕模式下设置localstorge值时会抛出 QuotaExceededError 的异常；
```
* 页面可见性（Page Visibility API） 可以有哪些用途？

```
通过 visibilityState 的值检测页面当前是否可见，以及打开网页的时间等;
在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放；

```

<h2 id="css">css</h2>
* 介绍一下标准的CSS的盒子模型？低版本IE的盒子模型有什么不同的？


```
 (1）有两种， IE 盒子模型、W3C 盒子模型；
（2）盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)；
（3）区  别： IE的content部分把 border 和 padding计算了进去;

```
* CSS3新增伪类有那些？

```
举例：
    p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
    p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
    p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
    p:only-child        选择属于其父元素的唯一子元素的每个 <p> 元素。
    p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。

    :after          在元素之前添加内容,也可以用来做清除浮动。
    :before         在元素之后添加内容
    :enabled        
    :disabled       控制表单控件的禁用状态。
    :checked        单选框或复选框被选中。

```
* 如何让 div 水平垂直居中？

```
（一）
	div {
    	position: absolute;     /* 相对定位或绝对定位均可 */
    	width:500px;
    	height:300px;
    	top: 50%;
    	left: 50%;
    	transform: translate(-50%, -50%);
	}

（二）
	div {
    	position: relative;     /* 相对定位或绝对定位均可 */
    	width:500px;
    	height:300px;
    	top: 50%;
    	left: 50%;
    	margin: -150px 0 0 -250px;      /* 外边距为自身宽高的一半 */
  	}

（三）
	.container {
    	display: flex;
    	align-items: center;        /* 垂直居中 */
    	justify-content: center;    /* 水平居中 */
	}

	.container div {
    	width: 100px;
    	height: 100px;
	}  

```
* position的值relative和absolute定位原点是？

```
  absolute
    生成绝对定位的元素，相对于值不为 static的第一个父元素进行定位（原文档流中的位置不做保留）。
  fixed （老IE不支持）
    生成绝对定位的元素，相对于浏览器窗口进行定位。
  relative
    生成相对定位的元素，相对于其正常位置进行定位（原文档流中的位置依然保留）。
  static
    默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right z-index 声明）。
  inherit
    规定从父元素继承 position 属性的值。
```
[absolute和relative的区别](http://www.html-js.com/article/3044)

* 用纯CSS创建一个三角形的原理是什么？

```
把上、左、右三条边隐藏掉（颜色设为 transparent）
#demo {
  width: 0;
  height: 0;
  border-width: 20px;
  border-style: solid;
  border-color: transparent transparent red transparent;
}

```
* 对BFC规范(块级格式化上下文：block formatting context)的理解？

```
W3C CSS 2.1 规范中的一个概念,它是一个独立容器，决定了元素如何对其内容进行定位,以及与其他元素的关系和相互作用。）
 一个页面是由很多个 Box 组成的,元素的类型和 display 属性,决定了这个 Box 的类型。
 不同类型的 Box,会参与不同的 Formatting Context（决定如何渲染文档的容器）,因此Box内的元素会以不同的方式渲染,也就是说BFC内部的元素和外部的元素不会互相影响。
```
*

```

```

<h2 id="js">js</h2>

*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
<h2 id="其他">其他</h2>

*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
