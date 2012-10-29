---
layout: post
title: '从CSS看浏览器的兼容性'
tags:
  - css%e5%85%bc%e5%ae%b9
  - '%e6%b5%8f%e8%a7%88%e5%99%a8%e5%85%bc%e5%ae%b9'
  - '%e6%b5%8f%e8%a7%88%e5%99%a8%e5%85%bc%e5%ae%b9%e6%80%a7'

---

访问量大了，用什么浏览器的鸟都有，用什么鸟浏览器的都有。

现在的浏览器种类太多，版本太多。而且每个种类的各个版本，都有用户在使用。

不要让用户产生疑惑：咦，这个网站怎么在公司电脑上看着挺好的，回家了看就乱七八糟的呢？

想让所有用户都能没有障碍地看到和分享你的劳动成果？那就提高你网站的浏览器兼容性吧！那就让你的网页在各个浏览器下都能呈现出相同的表现和行为！

<!--more--><strong> </strong>

<strong><a href="http://www.fancycedar.info/wp-content/uploads/2011/03/browsers-css.jpg"><img class="alignright size-medium wp-image-65" title="browsers-css" src="http://www.fancycedar.info/wp-content/uploads/2011/03/browsers-css-300x300.jpg" alt="" width="300" height="300" /></a>其实浏览器的兼容性包括两个方面，就是刚才说的——表现和行为</strong>：
<ul>
	<li><strong>表现的兼容性</strong>，简单说现就是同一个网页在不同浏览器里显示的样子会不一样。这个是和CSS密切相关的。</li>
	<li>行为的兼容性，一般表现为Javascript执行状况会不一样。这个方面本文暂不讨论，有兴趣的童鞋可以自己Google下——不要急，等看完这篇文章的</li>
</ul>
现在有哪些常用的浏览器呢？

IE6, IE7, IE8, IE9, Firefox, Chrome, Safari, Opera, 360, 搜狗, 遨游, 世界之窗, 腾讯TT。

不用慌，要透过现象看本质。下面是按照浏览器的引擎分类：
<ol>
	<li><strong>Trident</strong>：IE6, IE7, IE8, IE9, 360, 搜狗, 遨游, 世界之窗, 腾讯TT</li>
	<li><strong>Gecko</strong>：Firefox</li>
	<li><strong>Webkit</strong>：Chrome, Safari</li>
	<li><strong>Presto</strong>：Opera</li>
</ol>
根据经验来看，使用Gecko和Webkit的浏览器对Web标准支持最到位，相同的代码在它们的渲染下样式基本没有差别。Presto对Web标准支持得也不错，但偶尔会出现一些小问题。

最让人头疼的，就是Trident的那些玩意儿了。

国内公司的这些浏览器就不讨论了，都是跟着IE走的。IE的版本越高，对Web标准的支持越好。

现在还用IE5的话就是个悲剧了，基本绝种，可以不考虑。但是IE6在国内占有的比例还是相当大的，至少有半壁江山。IE9出来之后还没有专门调试过前端样式，不敢妄言。

所以最终浏览器的兼容问题，主要就缩略到了IE6, IE7, IE8 和 Firefox的兼容问题。解决了它们之间兼容性之后，再考虑其他浏览器吧。

要做好浏览器的兼容，我觉得理解好以下的一些知识点会很有帮助：
<ol>
	<li><strong>reset.css （<a href="http://www.pureweber.com/article/reset-css/" target="_blank">Reset CSS的前生今世</a>）
</strong></li>
	<li><strong>正确理解盒模型</strong></li>
	<li><strong>block与inline</strong></li>
	<li><strong>float与clear</strong></li>
	<li><strong>CSS Hack</strong></li>
</ol>
其实做浏览器兼容性，也就是将以上的几点做好。

稍后我会写几篇文章分别说一下鄙人的心得和看法，希望和大家讨论交流哈~

&nbsp;

忍不住要先嚷嚷一句：做浏览器的兼容的时候，不要过于迷恋CSS Hack！Hack越多说明懂得越浅。

没啦~

&nbsp;

原文参见： <a href="http://www.fancycedar.info/2011/03/browser-compatibility-on-css-0/" target="_blank">http://www.fancycedar.info/2011/03/browser-compatibility-on-css-0/</a>

&nbsp;
