---
layout: post
title: 学做网页这件小事
tags:
  - '%e5%ad%a6%e5%81%9a%e7%bd%91%e9%a1%b5'
  - '%e7%bd%91%e9%a1%b5%e5%88%b6%e4%bd%9c%e5%85%a5%e9%97%a8'
  - '%e7%bd%91%e9%a1%b5%e5%88%b6%e4%bd%9c%e6%95%99%e7%a8%8b'
  - '%e9%9d%99%e6%80%81%e9%a1%b5%e9%9d%a2%e5%88%b6%e4%bd%9c'

---

&nbsp;

神马都是浮云，神马都在云端。

在这个时代，很多人都会面临网页制作这个事情。特别是对广大程序猿们，网页制作应该是很基本的技能了——你也不用会得太多，但你也不能一点不会。

但是对于到底怎么学做网页这个小事，对新手来说却是个大事。遵循“复用”的原则，我希望这一篇文章能解除多个人的疑惑。

[caption id="attachment_366" align="alignright" width="183" caption="A guide for newbie"]<a href="http://www.pureweber.com/wp-content/uploads/2011/03/guide.jpg"><img class="size-medium wp-image-366  " title="A guide for newbie" src="http://www.pureweber.com/wp-content/uploads/2011/03/guide-286x300.jpg" alt="A guide for newbie" width="183" height="192" /></a>[/caption]

俗话说，师父领进门，修行靠个人。这里不会教你怎样做美工怎样编码怎样制作表单怎样控制样式，这里只会<strong>教你怎样去学习</strong>制作网页，怎样从一个菜鸟成长为一个老鸟。

我只是一个掌灯的NPC，打怪练级还得靠你自己。

好了，闲话不多说了，开始谈点正经的吧～以下的内容请循序渐进，一步一步来。

P.S. 为了降低学习的难度提高学习的速度，这里给出的基本都是中文资料。
<h3><span style="color: #000000;">1. 首先, 明确概念</span></h3>
<ul>
	<li>
<h4>做网页 vs 做网站</h4>
<ul>
	<li>做网页：这里就只代表制作<a title="静态网页的概念" href="http://baike.baidu.com/view/348763.htm" target="_blank">静态网页</a>。静态网页是一切网站的基础。制作静态网页非常之简单，少看个电影就能入门了。而且很多童鞋很多时候其实就只需要几个静态网页。本文会集中火力讲解怎样学习静态网页的制作。</li>
	<li>做网站：这里就指<a title="动态网页概念" href="http://baike.baidu.com/view/348756.htm" target="_blank">动态网页</a>了。这个需要有高级程序语言的基础，这里不讲，等下篇吧。</li>
</ul>
</li>
</ul>
<ul>
	<li>
<h4>设计网页 vs 制作网页</h4>
<ul>
	<li>设计网页：简单地说，就是指将网页画出来。这个属于美工的范畴，而不是程序。程序猿们还是先使劲学程序吧，你学的那点很难上得了厅堂。</li>
	<li>制作网页：简单地说，就是指将美工画出来的网页做成静态网页。目前国内这个还是程序猿的活。但国外很多美工都能做出代码质量很高的静态网页。因为静态网页的制作真的很好学，很简单。看到这里，你的信心增强不少了吧！</li>
</ul>
</li>
</ul>

<h3>2. Web标准&nbsp;

[caption id="attachment_361" align="alignright" width="181" caption="W3C"]<a href="http://www.pureweber.com/wp-content/uploads/2011/03/w3c.jpg"><img class="size-medium wp-image-361 " title="W3C" src="http://www.pureweber.com/wp-content/uploads/2011/03/w3c-300x166.jpg" alt="W3C" width="181" height="100" /></a>[/caption]</h3>
<ul>
	<li>什么是<a href="http://www.w3cschool.cn/w3c_intro.html" target="_blank">W3C</a>？（<a href="http://www.w3.org/" target="_blank">官方网站</a>）</li>
	<li><a href="http://baike.baidu.com/view/7921.htm" target="_blank">Web标准的含义</a></li>
</ul>
这个部分第一次看的时候，不用看得太明白。等掌握了HTML和CSS之后应该再复习一下这个部分。
<h3>3. 唠叨几句</h3>
请同学们先暂时压抑一下自己写代码的冲动，请先看看以下的几点注意事项：
<ul>
	<li>用什么来写代码？不要使用自动生成代码的工具！不要用Dreamwaver的设计模式！如果你对自己要求不高，你可以使用Dreamwaver的代码模式。如果你对自己要求很高，推荐使用有代码高亮功能的文本编辑器，比如：<a href="http://xbeta.info/vim-tutorials.htm" target="_blank">Vim</a>， UltraEdit，<a href="http://doc.linuxpk.com/3947.html" target="_blank">Emacs</a></li>
	<li>看教程时，所有示例代码必须自己实现</li>
	<li>Dirty your hands. 实现示例时，所有的代码<strong>必须手动输入</strong>。从第一个示例程序就开始坚持！Ctrl+C Ctrl+V的话是学不会的。得真刀真枪才能锻炼出来</li>
	<li>当你等下看教程的时候，会发现会有很多内容，你或许会感叹内容太多甚至望而却步。不要慌！其实教程的很多东西都是目前不用屌的。先把这里罗列出的入门知识看完再去慢慢学其他的也不迟</li>
	<li>当你遇到问题的时候，首先应该思考——找到问题所在并尝试去找解决方案，其次应该查询参考手册（文后附下载地址），再次问Google（百度就免了），最后也可以到这里提问</li>
</ul>
<h3>4. HTML</h3>
[caption id="attachment_315" align="alignright" width="187" caption="HTML DOM TREE"]<a href="http://www.pureweber.com/wp-content/uploads/2011/03/tree.gif"><img class="size-medium wp-image-315       " title="HTML DOM TREE" src="http://www.pureweber.com/wp-content/uploads/2011/03/tree-264x300.gif" alt="HTML DOM TREE" width="187" height="213" /></a>[/caption]

HTML并非是单纯的一行一行的代码，而应该有严禁的结构——<a href="http://www.w3cschool.cn/index-26.html" target="_blank">DOM</a>。您写的不是代码，您写的也不是寂寞，您写的是一棵树。

HTML就是网页的骨骼，就是网页的结构。

关于HTML的教程，网上有很多，但很多都有些过时或者繁琐。个人比较推荐 <a href="http://www.w3cn.org/" target="_blank">网页设计师</a> 和 <a href="http://www.w3school.com.cn/" target="_blank">W3School</a> (<a href="http://www.w3schools.com/" target="_blank">英文版</a>)。

这个阶段需要看的内容为：
<ul>
	<li><a href="http://www.w3school.com.cn/html/index.asp" target="_blank">HTML教程</a> 只看其中的基础教程</li>
</ul>
好了，对于HTML，就只需要学习这么多。不要惊讶，这就是基础，就这么少，但一定要全部掌握。
<h3>4. CSS</h3>
CSS就是网页的皮肤。学会CSS之后你就可以随心所欲地控制网页的样式了。
<ul>
	<li><a href="http://www.w3school.com.cn/css/index.asp" target="_blank">CSS教程</a> 也要注重实践哦！</li>
</ul>
<h3>5. XHTML+CSS</h3>
这个部分将告诉你怎样将HTML和CSS结合起来使用，做出漂亮且实用的网页。一定要手动编写代码实践！
<ul>
	<li><a href="http://www.w3school.com.cn/xhtml/xhtml_html.asp" target="_blank">XHTML与HTML的异同</a></li>
	<li><a href="http://www.w3cn.org/article/step/index.html" target="_blank">循序渐进</a> 这里有12篇文章</li>
	<li><a href="http://www.aa25.cn/special/10day/" target="_blank">十天学会DIV+CSS布局</a> 这里有10篇文章</li>
	<li><a href="http://www.blueidea.com/tech/site/2006/3574.asp" target="_blank">DIV+CSS入门</a> 蓝色理想网站的文章</li>
</ul>
<h3>6. 回头复习 2. Web标准</h3>
<h3>7. 没有了</h3>
如果您能耐心地看完这里给出的资料，并且都实践了，那么恭喜您，入门成功！

这个时候你可以说自己会做静态网页了。

当然，要学的其实还有很多很多，比如如何切图，如何使用JavaScript等等。

有关这些的文章会在近期推出，有兴趣的同学可以关注一下，谢谢。

如有谬误，敬请斧正！

另外有个好消息，想听现场讲座的同学有福了！<strong><a href="http://www.pureweber.com/article/pureweber-register-open/" target="_blank">猛击这里报名</a></strong>！完全免费的哦。
<h3>附. 手册下载</h3>
这两本手册很精简，但是绝对够用了，我一直就使用这两本手册。

HTML超精简手册：<a rel="attachment wp-att-346" href="http://www.pureweber.com/article/how-to-learn-web-programing/html/">HTML参考手册</a>

CSS2参考手册：<a rel="attachment wp-att-347" href="http://www.pureweber.com/article/how-to-learn-web-programing/css2/">CSS2参考手册</a>

原文地址：<a href="http://www.fancycedar.info/2011/03/how-to-learn-web-programing/" target="_blank">http://www.fancycedar.info/2011/03/how-to-learn-web-programing/</a>
