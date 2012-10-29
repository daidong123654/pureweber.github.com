---
layout: post
title: Ajax初步
tags:
  - ajax
  - javascript
  - xhr

---

Genra: Ajax学习手记

Resource: Foundation of Ajax (Ajax基础教程)

内容提要:
<ol>
	<li><a href="#why">为什么使用Ajax?</a></li>
	<li><a href="#when">什么场合下使用Ajax?</a></li>
	<li><a href="#what">Ajax技术包括哪些组成部分?</a></li>
	<li><a href="#xhr">使用XMLHttpRequest对象.</a></li>
</ol>
<a name="why"></a>
<h3>1.为什么使用Ajax?</h3>
原因有二:

一. Ajax是一种客户端方法, 它可以与任何服务器端技术进行交互, 因此, 开发者可以不必关心具体的服务器端技术, 而开发出具有高移植性的WEB应用程序.

二. Ajax可以实现客户端与服务器间的异步通信, 从而可以免去用户等待服务器响应和刷新整个页面的苦恼. 换句话说, Ajax可以在不刷新页面和不停止响应用户输入的前提下实现与服务器的交互.

上述的第一点让ＷＥＢ程序开发人员有更好的体验，而第二点让ＷＥＢ程序的用户有更好的体验。所以，我们要使用Ajax技术。

<a name="when"></a>
<h3>２、在什么场合使用Ajax?</h3>
可以说几乎每个Web应用都可以使用Ajax而从中获益，不过还是有一些场合最适合使用Ajax.
<ol>
	<li>需要处理复杂的验证时；</li>
	<li>用户需要更好的体验时；</li>
	<li>希望在与服务器通信时不停止响应用户输入时；</li>
	<li>只希望改变页面的一小部分，而不是刷新整个页面时。</li>
</ol>
＊注意：尽管Ajax有着很广泛的应用，而且它也能给我们带来更好的体验，但是有的时候还是不能使用它。下面列出了其中的几种情形:
<ol>
	<li>由于一些老版本的浏览器并不支持做为Ajax应用基础的XMLHttpRequest对象，因此，当你的主要用户群在使用这样的浏览器时，使用Ajax进行Web开发是不明智的；</li>
	<li>传统的Web应用让用户养成了这样的习惯，他们习惯于使用浏览器的“后退”按钮来返回他们刚访问的页面。但是Ajax应用使用的是异步通信的方式，不刷新页面，从而也不改变浏览器的栈，这样，如果用户想用“后退”按钮来返回上一个状态时，就会发生想不到的事情，因此，如果这种情况经常发生，请不要使用Ajax技术。</li>
</ol>
<a name="what"></a>
<h3>３、Ajax技术包括哪些组成部分？</h3>
Ajax包括四个部分，他们是：
<ul>
	<li>Javascript:  Ajax应用程序是使用Javascript编写的。它为Ajax应用提供逻辑。</li>
	<li>CSS:　CSS为Ajax应用提供表现。</li>
	<li>DOM:　DOM为Ajax提供一种可访问的文档结构，从而使脚本可以在运行时改变用户界面。</li>
	<li>XMLHttpRequest:　XMLHttpRequest对象允许Web应用与服务器进行异步通信。</li>
</ul>
Javascript是Ajax应用的核心，而XMLHttpRequest则是实现Ajax异步特点的关键。

<a name="xhr"></a>
<h3>４、使用XMLHttpRequest对象</h3>
Ajax技术并不是一种新的技术，甚至于不能说它是一种技术。它其实是基于XMLHttpRequest对象的一种应用技巧。而XMLHttpRequest对象早在IE5.0的时候就已经被支持了。只是那时只有ＩＥ支持它，所以没能得到普遍的应用。而现在不同了。大多数浏览器都对XMLHttpRequest对象做了相似的实现，虽然还没有一个统一的标准，但是进行可移植的Ajax应用开发已经成为了可能。

下面简单介绍一下XMLHttpRequest对象的应用。首先说一说如何实例化一个XMLHttpRequest对象。

由于IE把XMLHttpRequest实现为一个ActiveX对象，而其它的浏览器则把它实现为一个本地Javascript对象，因此，在实例化一个XMLHttpRequest 对象时要进行一下必要的判断。

[coolcode lang="javascript"]
var xmlHttp;
function createXHR(){
    if(window.ActiveXObject){
        xmlHttp = new ActiveXObject("Microsoft.XMLHTTP");
    }else if(window.XMLHttpRequest){
        xmlHttp = new XMLHttpRequest();
    }
}
[/coolcode]

这样就实例化了一个XMLHttpRequest对象。

下面简单介绍一下XMLHttpRequest对象的属性与方法：
<div>[coolcode lang="javascript"]
// 方法
abort()    //停止当前请求
getAllResponseHeader()   //把HTTP请求的所有响应首部作为键／值对返回
GetResponseHeader("header")    //返回指定首部的串值
open("method", "url")　　/*建立对服务器的调用。method参数可以是GET,POST或PUT。url参数可以是相对URL或绝对URL。此方法还有三个可选参数*/
send(content)     //向服务器发送请求
setRequestHeader("header", "value")     //把指定首部设置为所提供的值。在此之前必须先调用open()

//属性：
onreadystatechange          //事件处理器，每个状态改变时都会触发这个事件处理器。一般为一个Javascript函数
readyState        //请求的状态。０：未初始化，１：正在加载，２：已加载，３：交互中，４：完成。
responseText　　　//服务器的响应，一个字符串
responseXML        //服务器的响应，表示为XML。这个对象可以解析为一个DOM对象。
status　　　　//服务器的HTTP状态码
statusText    //服务器的HTTP 状态码对应的文本提示
[/coolcode]

一个交互实例：

一个Ajax交互的步骤主要如下：
<ol>
	<li>客户端事件触发一个Ajax事件；</li>
	<li>创建XMLHttpRequest对象的一个实例；</li>
	<li>向服务器发送请求；</li>
	<li>服务器处理请求并传回数据；</li>
	<li>XMLHttpRequest调用onreadystatechange事件处理器响应状态变化。</li>
</ol>
写个例子来看看：

[coolcode lang="javascript"]
var xmlHttp;
function validateEmail(){
    var email = document.getElementById("email");
    var url = "validate?email="+escape(email.value);
    createXHR();    //这里使用了我们刚才定义过的函数
    xmlHttp.open("GET", url);  //通过GET方法，打开与服务器的链接
    xmlHttp.onreadystatechange = callback;  //当状态发生改变时，调用callback函数来处理
    xmlHttp.send(null);　//向服务器发送请求
}

function callback(){
    //do something that you want.
    if(xmlHttp.readyState == 4){
        if(xmlHttp.status == 200){
            //当xmlHttp对象的readyState为4即"完成"时，同时服务器返回200即成功时，显示一个提示信息。
            alert("OK, the query has been sent to the server");　
        }
    }
}
[/coolcode]

这就是使用XMLHttpRequest对象与服务器交互的基本方法了。当然，这是一个极简单的例子，不过，了解了其工作原理后，你就可以使用Javascript创建更加丰富，功能更加强大的Ajax 应用了。

原文链接（有改动）：<a href="http://www.zhiyan.info/2006/12/21/ajax-foundation.html">http://www.zhiyan.info/2006/12/21/ajax-foundation.html</a>

</div>
