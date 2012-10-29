---
layout: post
title: 消息推送系统——（一）概念与原理
tags:
  - comet
  - comet%e6%8a%80%e6%9c%af
  - http%e9%95%bf%e8%bf%9e%e6%8e%a5
  - push-server-2
  - '%e5%90%8c%e6%ad%a5'
  - '%e5%bc%82%e6%ad%a5'
  - '%e6%b6%88%e6%81%af%e6%8e%a8%e9%80%81'
  - '%e9%98%bb%e5%a1%9e'
  - '%e9%9d%9e%e9%98%bb%e5%a1%9e'

---

这里我们从系统结构的层面来看消息推送系统（Push Server）的基本原理。

首先需要了解几个基本的概念：
<h3>HTTP长连接</h3>
翻译自http keep-alive connection和http persistent connection，又叫http connection reuse，网上也有反过来翻译成http long connection。

下面这个图来自wikipedia，讲解了http长连接是在一个TCP连接的基础之上，发送多个HTTP请求以及接收多个HTTP响应，这是为了避免每一次请求都去打开一个新的连接。在HTTP 1.1标准中，所有的请求都认为是长连接。

<img class="alignnone" title="http keep-alive connection" src="http://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/HTTP_persistent_connection.svg/450px-HTTP_persistent_connection.svg.png" alt="HTTP长连接图解" width="450" height="280" />

在这里的消息推送系统中，HTTP长连接的作用就是向服务器发送请求，然后一直等待服务器的返回数据。这就相当于客户端在“监听”服务器了，可以随时接收来自服务器的消息。OK，lolita is ready to be pushed!
<h3>同步与异步</h3>
同步：IO操作将导致请求进程阻塞，直到IO操作完成。也就是说<strong>客户端</strong>在发送请求后，必须得在服务端有回应后才发送下一个请求。

异步：IO操作不导致请求进程阻塞。也就是说<strong>客户端</strong>在发送请求后，不必等待服务端的回应就可以发送下一个请求。

同步与异步说的是客户端与服务器端之间的一种通信方式。
<h3>阻塞与非阻塞</h3>
阻塞：<strong>服务器端</strong>的线程或者进程没有处理完数据的时候，不会返回，线程或者进程回被挂起，不再响应其他请求。

非阻塞：<strong>服务器端</strong>在没有处理完的时候，会立即返回，不会挂起线程或者进程，可以继续响应其他请求。

阻塞与非阻塞说的是服务器端对请求的处理方式。

在消息推送系统中，客户端+服务器端一起，使用的是异步非阻塞。

&nbsp;
<h3>消息推送系统（Push Server）的结构和原理</h3>
好了，接下来是就是消息推送系统（Push Server）的结构和原理了：

&nbsp;

<a rel="attachment wp-att-2093" href="http://www.pureweber.com/article/push-server-principle/pushserverprinciple-2/"><img class="alignnone size-full wp-image-2093" title="Push Server Principle" src="http://www.pureweber.com/wp-content/uploads/2012/05/PushServerPrinciple1.png" alt="" width="599" height="587" /></a>

1. 客户端发出一个http长连接请求，然后等待服务器的响应。这个请求是异步的，所以客户端可以继续工作，比如发起其他ajax请求等等。这个时候客户端就是一个待推倒的小萝莉了。

2. 服务器接到请求之后，并不立即发送出数据，而是hold住这个connecton。这个处理是非阻塞的，所以服务器可以继续处理其他请求。

3. 在某个时刻，比如服务器有新数据了，服务器再主动把这个消息推送出去，即通过之前建立好的连接将数据推送给客户端。

4. 客户端收到返回。这个时候就可以处理数据，然后再次发起新的长连接。

基本原理就是这么简单。

但是在具体实现的时候，还有很多细节要处理，需要一些其他的技术。

下一篇会讲解客户端Javascript的实现，主要内容是HTTP长连接的建立和CORS在不同浏览器下的实现。

<em>参考资料：</em>

<em><a href="http://en.wikipedia.org/wiki/HTTP_persistent_connection" target="_blank">http://en.wikipedia.org/wiki/HTTP_persistent_connection</a></em>

<em>
</em>
