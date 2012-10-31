---
layout: post
title: 'PureWeber Goo Shortener编写总结'
author: 张雄
github: bearzx
tags:
  - css
  - 'goo gl'
  - 'psd to html'
  - '短网址'

---

##接到任务

上周的某一天收到段神的邮件，得到任务一枚：要我利用已经由7lemon编写好的API写一个提供短网址服务的页面，并提供给了我PSD设计稿。虽然看起来并不是很难的任务，然而我对css还相当生疏，而且之前也没有根据PSD来设计页面的经验（谈不上设计倒是，只是实现了界面而已）。

##趟地图

我琢磨着PSD 2 div+css肯定是一项已经被广泛使用的方式，遂去问度娘，得到文章一篇《<a href="http://www.uimaker.com/plus/view.php?aid=3379">PSD网页切图制作HTML全过程教程</a>》）上面给出了一个PSD切图制作html的教程，相当详细，对于入门者很是受用。我照着做下去，却遇到了一个问题：自己切的图总是不能正确显示在网页上，比如切出了按钮的图，加入到css中，按钮还是原来的样子，后来分析后发现是切图的问题，一定要用切片工具选定一个区域后再切图，而不能只是将画面调整至想要的状态后直接ctrl+shift+alt+s。

##完成任务&amp;修正八阿哥

解决了上述问题，开始各种切图，写css，却在安排组件位置时遇到了麻烦，不知道该如何书写css语句以将组件（图片）安排至我想要的位置，一开始很傻X的使用了position: absolute手动定义坐标，实为权宜之计，因为只要浏览器大小一变，布局就又乱了，后来经段神指点，得知可以将一个div中加上margin: 0 auto并给div设置好大小，这样就可以自动地将页面调整至居中，然后将其他组件放在上面的div里布局，相当于认为指定了页面的大小。之后的组件再在div中内部使用绝对坐标布局即可，还有一点，在一个div内部的div中如果使用了posiotn: absolute其top, left属性是相对于上层的div而言的，不是屏幕的左上角。

绘制好了界面，加入逻辑部分（这部分灰常简单，直接将API include进来调用即可）就基本完成了，发给段神，收工，转天却收到段神的邮件，指出了几个问题，其中一个是meta标签与php的header只写一个即可，还有一个是说我切图不够精准，这一点我还真没有注意，打开浏览器放大几倍才发现很多地方下面的边框被我无情地切掉了。还有一个问题是给出的按钮有两个状态，而我给当成一个状态使用了，改正这一点的时候，我又学会了一个新东西：input标签的事件属性，通过触发时间的处理可以实现动态改变样式的效果，即使用this.className=xxx（具体方法参见本文末尾的参考资料）。

最后还修正了一个问题：文本框中的文字在出IE之外的浏览器中都能显示在文本框的中央，然而在IE中却总是靠上一点，经7lemon指点，在css中设置了line-height属性与图片大小一致后得到解决。

通过这次的coding，让我体会到了div+css之美，还有仔细与严谨的重要性。

##最终效果

[PureWeber Goo Shortener](http://www.pureweber.com/works/short/)

##参考资料

 - <a href="http://www.uimaker.com/plus/view.php?aid=3379">PSD网页切图制作HTML全过程教程</a>
 - <a href="http://apps.hi.baidu.com/share/detail/16856547">html input type text标签属性和方法事件</a>
 - <a href="http://www.ninedns.com/html/20074221602392639.html">Html:网页制作基础： 表单按钮的使用</a>
