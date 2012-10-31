---
layout: post
title: 'Ajax简介 - 异步交互'
description: 本文对比传统网页的交互方式和Ajax交互方式的不同之处，分析异步交互的优点，并以两个实例讲解如何使用Ajax进行异步交互。
author: 朱玺
tags:
  - ajax
  - '异步交互'
  - '实例'
  - '教程'

---

<table class="grid">
<tr><th>主讲人</th><td>朱玺</td></tr>
<tr><th>题目</th><td>Ajax简介 - 异步交互</td></tr>
<tr><th>时间</th><td>2011-5-8</td></tr>
<tr><th>&nbsp;</th><td><a href="#downloads">相关下载</a></td></tr>
</table>

##简单介绍

Ajax——“Asynchronous JavaScript and XML”（异步JavaScript和XML)...看上去很抽象吧。
还是再介绍介绍JavaScript和XML吧。


 - JavaScript：是一种脚本语言,结构简单,使用方便,其代码可以直接放入HTML文档中,可以直接在支持JavaScript的浏览器中运行.——总而言之就是一种在客户端运行的语言。
 - XML：可扩展标记语言，Xml是Internet环境中跨平台的，依赖于内容的技术，是当前处理结构化文档信息的有力工具。——原来是处理信息用的。


##Ajax是干什么的？

通过 AJAX，您的 JavaScript 可使用 JavaScript 的 XMLHttpRequest 对象来直接与服务器进行通信。通过这个对象，您的 JavaScript 可在不重载页面的情况与 Web 服务器交换数据。即实现网页与服务器的异步通信功能。

而传统网页同步处理请求的方法是用户触发一个HTTP请求到服务器,服务器对其进行处理后再返回一个新的HTHL页到客户端——<strong>用户每次都要浪费时间和带宽去重新读取整个页面</strong>。造成的结果是在网速较低或需要传输的页面较大的情况下原页面会锁死。大大降低用户的浏览体验。

对比传统网页交换数据的方法使Ajax技术拥有两大优点：


 - 可以像桌面应用程序只同服务器进行数据层面的交换,减轻服务器负担，缩短了用户等候时间。
 - 加快了页面的相应速度，大大提高了页面的交互性。使因特网应用程序更小、更快，更友好。


##原理图解

###传统网页交互方式
页面直接与服务器交换数据，两次user activity之间的世界就是用户页面锁死的时间。

![Sync Request](http://www.pureweber.com/wp-content/uploads/2011/05/1.png)

###通过Ajax技术的交互方式

Ajax技术在用户页面和服务器之间加入了一个中间层（Ajax engine），用户提出的请求先提交到中间层，中间层再分析用户提交的请求后确定向服务器提交的请求。最后根据服务器返回的数据通过JavaScript实时将结果显示到用户页面上。——以上的数据交换都是在中间层上完成的，所以不会造成整个页面的锁死。加强了用户体验。

![Async Request](http://www.pureweber.com/wp-content/uploads/2011/05/2.png)


##Ajax小应用

 - <a  href="http://www.pureweber.com/works/demos/ajax-intro/index.htm">获取服务器时间</a>——在不重新加载整个页面的情况下在页面上显示服务器时间。
 - <a  href="http://www.pureweber.com/works/demos/ajax-intro/index1.htm">实时显示物品信息</a>——加强页面交互性。

![Ajax Demo Show](http://www.pureweber.com/wp-content/uploads/2011/05/3.png)


##具体实现


 - 文件组成：有3个文件index.htm ajax.js 和 telltimeXML.php 组成。
 - 核心部件：其中的关键就在于ajax.js文件里的XMLHttpRequest 对象。


XMLHttpRequest对象的属性和方法见文末的<a href="#appendix">附录</a>。

我们来重点分析一下ajax.js文件中 getServerTime() 和 useHttpResponse()两个函数。

最前面的getXMLHTTPRequest()函数是针对不同浏览器来建立 XMLHttpRequest 对象，有兴趣的童鞋可以自行google其中的奥妙。

先来看 getServerTime() 

{% highlight javascript %}
var myurl = "telltimeXML.php";
var myRand = parseInt(Math.random() * 999999999);
var modurl = myurl + "?rand=" + myRand;
{% endhighlight %}

这里构造了一个open函数里的url参数，即Ajax需要发出的服务器请求。这里使用了一Math.random()具体作用后面会再做介绍。

{% highlight javascript %}
http.open("GET", modurl, true);
{% endhighlight %}

设定对服务器请求的一些参数：请求类型GET， url：为前面生成，true：异步传输数据。

{% highlight javascript %}
http.onreadystatechange = useHttpResponse;
{% endhighlight %}

设定当readyState 属性改变时，就调用 useHttpResponse() 函数。这里作一下说明，readyState 属性是根据XMLHttpRequest 对服务器请求的不同状态而自动发生变化。具体可参见对readyState 属性的介绍。

{% highlight javascript %}
http.send(null);
{% endhighlight %}

最后发送请求就可以了。

然后来看 useHttpResponse() 函数对readyState 属性改变时所做出的相应。

我的代码是对readyState == 4 和 status == 200 同时成立时（即一般情况下Ajax对服务器请求完成，且服务器返回相应已就绪）对服务器返回的responseXML（包含服务器时间信息）进行处理，并利用javascript对网页进行修改，做到无刷新的数据交换。

在其他情况下就显示一个Loading...表示网页正在后台与服务器交换信息。

##Ajax的几个缺陷

###缓存

由于 XMLHttpRequest 对象是通过url来对服务器进行请求的，这就不可避免的与浏览器的缓存机制产生了冲突。简单的说，由于服务器端的信息可能是时刻改变的，浏览器缓存则是以url为标准记录缓存。当通过同一url访问服务器时，可能服务器端的数据已经改变，而浏览器却只是读取了本地缓存，而使在网页上显示的信息和在服务器上的信息不一致。造成问题。所以在getServerTime() 函数中我使用了一个Math.random()函数来使每次请求的url不一致，来欺骗浏览器，使其不读取缓存。在讨论中段哥也提到了这个问题，并指出这个方法并不科学，因为random()函数也有小概率产生同样的url同样可能造成问题。现在正确的做法是先读取服务器端返回的状态，若为304则表明服务器端数据未修改，则可以直接读取缓存，否则需从服务器端重新读取信息。

###历史

由于Ajax对网页进行的是实时改变，并不改变网页的url，所以会导致浏览器没有办法记录访问地址，并且无法与好友分享网页上的信息。


谢谢大家耐心阅读。

<h2 id="downloads">相关下载</h2>


 - <a href="http://www.pureweber.com/works/demos/ajax-intro/Ajax-intro.zip">示例程序</a>
 - <a href="http://www.pureweber.com/works/demos/ajax-intro/Ajax-intro.ppt">演示PPT</a>


<h2 id="appendix">附录</h2>

参考文章：[Ajax初步](/article/2011/02/ajax-get-started.html)

在此摘录XMLHttpRequest对象的一些属性和方法。

如需将请求发送到服务器，我们使用 XMLHttpRequest 对象的 open() 和 send() 方法：

<pre><code>open(method,url,async)	method：请求的类型；GET 或 POST
					url：文件在服务器上的位置
					async：true（异步）或 false（同步）
send(string)			string：post请求中所要传输的数据。
onreadystatechange		存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。
readyState			存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
					0: 请求未初始化
					1: 服务器连接已建立
					2: 请求已接收
					3: 请求处理中
					4: 请求已完成，且响应已就绪
status				返回的服务器状态，一般正常的话为200。
responseText			获得字符串形式的响应数据。
responseXML			获得 XML 形式的响应数据。
</code></pre>
