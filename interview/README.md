[WebSocket 是什么原理？为什么可以实现持久连接？](https://www.zhihu.com/question/20215561)

> 其实我们所用的程序是要经过两层代理的，即`HTTP协议`在`Nginx`等服务器的解析下，然后再传送给相应的`Handler`（PHP等）来处理。简单地说，我们有一个非常快速的`接线员（Nginx）`，他负责把问题转交给相应的`客服（Handler）`。本身接线员基本上速度是足够的，但是每次都卡在`客服（Handler）`了，老有客服处理速度太慢。，导致客服不够。`Websocket`就解决了这样一个难题，建立后，可以直接跟接线员建立持久连接，有信息的时候客服想办法通知接线员，然后`接线员`在统一转交给客户。这样就可以解决客服处理速度过慢的问题了。

> 同时，在传统的方式上，要`不断的建立`，关闭HTTP协议，由于HTTP是非状态性的，每次都要重新传输`identity info（鉴别信息）`，来告诉服务端你是谁。虽然接线员很快速，但是每次都要听这么一堆，效率也会有所下降的，同时还得不断把这些信息转交给客服，不但浪费客服的处理时间，而且还会在网路传输中消耗过多的流量/时间。但是Websocket只需要一次HTTP握手，所以说整个通讯过程是建立在一次连接/状态中，也就避免了HTTP的非状态性，服务端会一直知道你的信息，直到你关闭请求，这样就解决了接线员要反复解析HTTP协议，还要查看identity info的信息。同时由客户主动询问，转换为服务器（推送）有信息的时候就发送（当然客户端还是等主动发送信息过来的。。），没有信息的时候就交给接线员（Nginx），不需要占用本身速度就慢的客服（Handler）了。

[babelrc](https://zhuanlan.zhihu.com/p/24224107)

[阿里面试](https://zhuanlan.zhihu.com/p/26528397)

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
原理：HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，
这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。


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

在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根
据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使
用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操
作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。离线的情况下，浏览器就直接使用离线存储的资源。

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
（2）盒模型： 内容(content)、填充(padding)、边框(border)、边界(margin)；
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
https://jsbin.com/kuxahelohu/edit?html,css,output

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
 不同类型的 Box,会参与不同的 Formatting Context（决定如何渲染文档的容器）,因此Box内的元素会以不同的方式渲染,也
 就是说BFC内部的元素和外部的元素不会互相影响。
```
* css多列等高如何实现

[参考文档](http://codepen.io/yangbo5207/post/equh)

[大漠老师](https://www.w3cplus.com/css/creaet-equal-height-columns)

* 浏览器是怎样解析CSS选择器的？

```
样式系统从关键选择器开始匹配，然后左移查找规则选择器的祖先元素。
只要选择器的子树一直在工作，样式系统就会持续左移，直到和规则匹配，或者是因为不匹配而放弃该规则。
```
* ::before 和 :after中双冒号和单冒号 有什么区别？解释一下这2个伪元素的作用。

```
单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素。（伪元素由双冒号和伪元素名称组成）
双冒号是在当前规范中引入的，用于区分伪类和伪元素。不过浏览器需要同时支持旧的已经存在的伪元素写法，
比如:first-line、:first-letter、:before、:after等，
而新的在CSS3中引入的伪元素则不允许再支持旧的单冒号的写法。

想让插入的内容出现在其它内容前，使用::before，否者，使用::after；
在代码顺序上，::after生成的内容也比::before生成的内容靠后。
如果按堆栈视角，::after生成的内容会在::before生成的内

```
* 如何修改chrome记住密码后自动填充表单的黄色背景 ？

```
input:autofill, 
textarea:autofill, 
select:autofill {
  background-color: rgb(250, 255, 189); 
  background-image: none;
  color: rgb(0, 0, 0);
}
```
* 你对line-height是如何理解的？
 
[segmentfault](https://segmentfault.com/a/1190000003038583)

* 设置元素浮动后，该元素的display值是多少？

```
自动变成了 display:block
```
* 让页面里的字体变清晰，变细用CSS怎么做

```
-webkit-font-smoothing: antialiased;
```
* position:fixed;在android下无效怎么

```
fixed的元素是相对整个页面固定位置的，你在屏幕上滑动只是在移动这个所谓的viewport，
原来的网页还好好的在那，fixed的内容也没有变过位置，
所以说并不是iOS不支持fixed，只是fixed的元素不是相对手机屏幕固定的。
<meta name="viewport" content="width=device-width, initial-scale=1.0, 
maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>

```
* 如果需要手动写动画，你认为最小时间间隔是多久，为什么？

```
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms

```
* display:inline-block 什么时候会显示间隙？

```
移除空格、使用margin负值、使用font-size:0、letter-spacing、word-spacing

```
* overflow: scroll时不能平滑滚动的问题怎么处理

```
-webkit-overflow-scrolling: touch;

```
[实现原理](http://blog.csdn.net/hursing/article/details/9186199)

* 清楚浮动的方式

```
目前最简单的方式：
.clearfix{ 
  overflow: auto; 
  zoom: 1;   // 处理IE兼容性问题
} 
二:
.clearfix {
  zoom: 1;
}
.clearfix :after {
  clear:both;
  content:'.';
  display:block;
  height: 0;
  visibility:hidden;
}

<h2 id="js">js</h2>

* 介绍js的基本数据类型。

```
 Undefined、Null、Boolean、Number、String、
 ECMAScript 2015 新增:Symbol(创建后独一无二且不可变的数据类型 )
 
```
* 介绍js有哪些内置对象？

```
Object 是 JavaScript 中所有对象的父对象

数据封装类对象：Object、Array、Boolean、Number 和 String
其他对象：Function、Arguments、Math、Date、RegExp、Error

```
[参考文档](http://www.ibm.com/developerworks/cn/web/wa-objectsinjs-v1b/index.html)

* JavaScript原型，原型链 ? 有什么特点？

```
每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，
如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，
于是就这样一直找下去，也就是我们平时所说的原型链的概念。
关系：instance.constructor.prototype = instance.__proto__

特点：
JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，
与之相关的对象也会继承这一改变。


 当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的话，
 就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。
    function Func(){}
    Func.prototype.name = "Sean";
    Func.prototype.getInfo = function() {
      return this.name;
    }
    var person = new Func();//现在可以参考var person = Object.create(oldObject);
    console.log(person.getInfo());//它拥有了Func的属性和方法
    //"Sean"
    console.log(Func.prototype);
    // Func { name="Sean", getInfo=function()}

```
* 如何将浮点数点左边的数每三位添加一个逗号，如12000000.11转化为『12,000,000.11』?

```
function commafy(num){
  return num && num
  .toString()
  .replace(/(\d)(?=(\d{3})+\.)/g, function($1, $2){
     return $2 + ',';
  });
}

```
* Javascript如何实现继承？

```
1、构造继承
2、原型继承
3、实例继承
4、拷贝继承

原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。
例如：Object.prototype.toString.call(param).slice(8, -1) !== 'Object'

function Parent(){
  this.name = 'wang';
}

function Child(){
  this.age = 28;
}
Child.prototype = new Parent();//继承了Parent，通过原型

var demo = new Child();
alert(demo.age);
alert(demo.name);//得到被继承的属性


```
* 谈谈This对象的理解

	* this总是指向函数的直接调用者（而非间接调用者）；
	* 如果有new关键字，this指向new出来的那个对象；
	* 在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent中的this总是指向全局对象Window；

* eval是做什么的？

```
它的功能是把对应的字符串解析成JS代码并运行；
应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。
由JSON字符串转换为JSON对象的时候可以用eval，var obj =eval('('+ str +')');

```
* 什么是window对象? 什么是document对象?

```
window对象是指浏览器打开的窗口。
document对象是Documentd对象（HTML 文档对象）的一个只读引用，window对象的一个属性。

```
* null，undefined 的区别？

```
null        表示一个对象是“没有值”的值，也就是值为“空”；
undefined   表示一个变量声明了没有初始化(赋值)；

undefined不是一个有效的JSON，而null是；
undefined的类型(typeof)是undefined；
null的类型(typeof)是object；


Javascript将未赋值的变量默认值设为undefined；
Javascript从来不会将变量设为null。它是用来让程序员表明某个用var声明的变量时没有值的。

typeof undefined
    //"undefined"
    undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。
    当尝试读取时会返回 undefined； 例如变量被声明了，但没有赋值时，就等于undefined

typeof null
    //"object"
    null : 是一个对象(空对象, 没有任何属性和方法)；
    例如作为函数的参数，表示该函数的参数不是对象；

注意：
    在验证null时，一定要使用　=== ，因为 == 无法分别 null 和　undefined
    null == undefined // true
    null === undefined // false

再来一个例子：

    null
    Q：有张三这个人么？
    A：有！
    Q：张三有房子么？
    A：没有！

    undefined
    Q：有张三这个人么？
    A：有！
    Q: 张三有多少岁？
    A: 不知道（没有被告诉）

```
* IE与火狐的事件机制有什么区别？ 如何阻止冒泡？

	* 事件处理机制：IE是事件冒泡、Firefox同时支持捕获型和冒泡型两种事件模型；
	* ev.stopPropagation();（旧ie的方法 ev.cancelBubble = true;）
	
* new操作符具体干了什么呢?

```
1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
2、属性和方法被加入到 this 引用的对象中。
3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。

var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);

```
* Javascript中，有一个函数，执行时对象查找时，永远不会去查找原型

```
hasOwnProperty

javaScript中hasOwnProperty函数方法是返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原
型链中是否具有该属性；该属性必须是对象本身的一个成员。

使用方法：
object.hasOwnProperty(proName)
其中参数object是必选项。一个对象的实例。
proName是必选项。一个属性名称的字符串值。

如果 object 具有指定名称的属性，那么JavaScript中hasOwnProperty函数方法返回 true，反之则返回 false。

```
* JSON 的了解？

```
JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。
它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小
如：{"age":"12", "name":"back"}

JSON字符串转换为JSON对象:
var obj =eval('('+ str +')');
var obj = str.parseJSON();
var obj = JSON.parse(str);

JSON对象转换为JSON字符串：
var last=obj.toJSONString();
var last=JSON.stringify(obj);

```
* js延迟加载的方式有哪些？

```
defer和async、动态创建DOM方式（用得最多）、按需异步载入js

```
* 如何解决跨域问题?

```
jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面、cors

```
* documen.write和 innerHTML的区别

```
document.write只能重绘整个页面

innerHTML可以重绘页面的一部分

```
* DOM操作——怎样添加、移除、移动、复制、创建和查找节点?

```
（1）创建新节点
  createDocumentFragment()    //创建一个DOM片段
  createElement()   //创建一个具体的元素
  createTextNode()   //创建一个文本节点
（2）添加、移除、替换、插入
  appendChild()
  removeChild()
  replaceChild()
  insertBefore() //在已有的子节点前插入一个新的子节点
（3）查找
  getElementsByTagName()    //通过标签名称
  getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
  getElementById()    //通过元素Id，唯一性

```
* AMD（Modules/Asynchronous-Definition）、CMD（Common Module Definition）规范区别？

```

```
* requireJS的核心原理是什么？（如何动态加载的？如何避免多次加载的？如何 缓存的？）
* 参考：http://annn.me/how-to-realize-cmd-loader/

```

```
* ECMAScript6 怎么写class么，为什么会出现class这种东西?

```

```
* Object.is() 与原来的比较操作符“ ===”、“ ==”的区别？

```
两等号判等，会在比较时进行类型转换；
三等号判等(判断严格)，比较时不进行隐式类型转换,（类型不同则会返回false）； 

Object.is 在三等号判等的基础上特别处理了 NaN 、-0 和 +0 ，保证 -0 和 +0 不再相同，
但 Object.is(NaN, NaN) 会返回 true.

Object.is 应被认为有其特殊的用途，而不能用它认为它比其它的相等对比更宽松或严格。

```
<h2 id="其他">其他</h2>

* 设计模式 知道什么是singleton, factory, strategy, decrator么?

```

```
* 页面重构怎么操作？

```
网站重构：在不改变外部行为的前提下，简化结构、添加可读性，而在网站前端保持一致的行为。
也就是说是在不改变UI的情况下，对网站进行优化，在扩展的同时保持一致的UI。

对于传统的网站来说重构通常是：

表格(table)布局改为DIV+CSS
使网站前端兼容于现代浏览器(针对于不合规范的CSS、如对IE6有效的)
对于移动平台的优化
针对于SEO进行优化
深层次的网站重构应该考虑的方面

减少代码间的耦合
让代码保持弹性
严格按规范编写代码
设计可扩展的API
代替旧有的框架、语言(如VB)
增强用户体验
通常来说对于速度的优化也包含在重构中

压缩JS、CSS、image等前端资源(通常是由服务器来解决)
程序的性能优化(如数据读写)
采用CDN来加速资源加载
对于JS DOM的优化
HTTP服务器的文件缓存

```
* 是否了解公钥加密和私钥加密。

```
一般情况下是指私钥用于对数据进行签名，公钥用于对签名进行验证;
HTTP网站在浏览器端用公钥加密敏感数据，然后在服务器端再用私钥解密。

```
* WEB应用从服务器主动推送Data到客户端有那些方式？

```
tml5提供的Websocket
不可见的iframe
WebSocket通过Flash
XHR长时间连接
XHR Multipart Streaming
<script>标签的长时间连接(可跨域)

```
* 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？（流程说的越详细越好）

```
注：这题胜在区分度高，知识点覆盖广，再不懂的人，也能答出几句，
  而高手可以根据自己擅长的领域自由发挥，从URL规范、HTTP协议、DNS、CDN、数据库查询、
  到浏览器流式解析、CSS规则构建、layout、paint、onload/domready、JS执行、JS API绑定等等；

  详细版：
    1、浏览器会开启一个线程来处理这个请求，对 URL 分析判断如果是 http 协议就按照 Web 方式来处理;
    2、调用浏览器内核中的对应方法，比如 WebView 中的 loadUrl 方法;
    3、通过DNS解析获取网址的IP地址，设置 UA 等信息发出第二个GET请求;
    4、进行HTTP协议会话，客户端发送报头(请求报头);
    5、进入到web服务器上的 Web Server，如 Apache、Tomcat、Node.JS 等服务器;
    6、进入部署好的后端应用，如 PHP、Java、JavaScript、Python 等，找到对应的请求处理;
    7、处理结束回馈报头，此处如果浏览器访问过，缓存上有对应资源，会与服务器最后修改时间对比，一致则返回304;
    8、浏览器开始下载html文档(响应报头，状态码200)，同时使用缓存;
    9、文档树建立，根据标记请求所需指定MIME类型的文件（比如css、js）,同时设置了cookie;
    10、页面开始渲染DOM，JS根据DOM API操作DOM,执行事件绑定等，页面显示完成。

  简洁版：
    浏览器根据请求的URL交给DNS域名解析，找到真实IP，向服务器发起请求；
    服务器交给后台处理完成后返回数据，浏览器接收文件（HTML、JS、CSS、图象等）；
    浏览器对加载到的资源（HTML、JS、CSS等）进行语法解析，建立相应的内部数据结构（如HTML的DOM）；
    载入解析到的资源文件，渲染页面，完成。

```
