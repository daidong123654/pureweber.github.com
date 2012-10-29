---
layout: post
title: 消息推送系统——（零）推倒萝莉之术
tags:
  - comet
  - comet%e5%ba%94%e7%94%a8
  - comet%e6%8a%80%e6%9c%af
  - push-server-2
  - server-push
  - '%e6%8e%a8%e9%80%81'
  - '%e6%9c%8d%e5%8a%a1%e5%99%a8%e6%8e%a8'
  - '%e6%b6%88%e6%81%af%e6%8e%a8%e9%80%81'

---

当一个初学Web开发的童鞋，产生让服务器“主动”给浏览器客户端发送数据的想法的时候，比他入门稍早的同学会说：

“这是Web！只能由浏览器发起请求，然后得到服务器返回的数据。”

可能接触得更多的童鞋会说：

“除非你用Javascript轮询/心跳，不断请求服务器看有没有新的数据。但是用户多了服务器会受不了。”

都没错。

但主动推送数据非是不可实现的。聪明的先驱们已经找到了更优的解决方案，那就是利用http长连接来实现消息推送系统。

消息推送系统又叫服务器推、Comet技术、Push Server、Server Push等等。它们的含义大同小异，只是从不同场景中得来的不同的称呼而已，具体可以google。我个人比较喜欢Push Server这个名称，很形象——用来向客户端push消息的这么一个server，就叫Push Server。

消息推送系统是一个很有魔力的技术，它实现了攻受的颠倒和权力的反转。服务器不用再傻乎乎地等待着客户端的请求才能发送最新的数据，而是占据了主动，当有新数据的时候，服务器可以立即主动地将数据push给相关的客户端。

想一想，这个时候，你就可以push消息指挥客户端的Javascript做任何事，所有用户的页面都是你的线控木偶了。话说萝莉有三宝，轻音柔体易推倒。Web相比传统软件来说，也算是轻音柔体的萝莉了，而这里的Push Server，也就是推倒萝莉之术了:P 。

<a rel="attachment wp-att-2068" href="http://www.pureweber.com/article/push-server-brief/attachment/201110122221581523/"><img class="alignright size-medium wp-image-2068" title="lolita" src="http://www.pureweber.com/wp-content/uploads/2012/05/201110122221581523-300x127.jpg" alt="" width="300" height="127" /></a>

推倒萝莉之后，可以做什么呢？当然是很fancy的事情了：
<ul>
	<li>在线好友列表</li>
	<li>在线聊天（聊天室、点对点，多人聊天）</li>
	<li>即时通知</li>
	<li>统计、监控在线用户</li>
	<li>实时内容更新</li>
</ul>
这里要讲的Push Server，是由Javascript + Python(Tornado) + Memcache实现的。但文章中会着重介绍实现原理，而非具体的代码。

Push Server主要包含以下几个方面：
<ul>
	<li>http长连接</li>
	<li>Javascript 的 CORS (The Cross-Origin Resource Sharing)与跨浏览器实现</li>
	<li>服务器异步响应</li>
	<li>客户端的链接与断开</li>
	<li>性能何如</li>
</ul>
后面的文章会慢慢解来。
