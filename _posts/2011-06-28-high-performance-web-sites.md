---
layout: post
title: 读书分享：《高性能网站建设指南》
author: 张雄
github: bearzx
tags:
  - '前端优化'
  - '网站提速'
  - '高性能网站建设指南'

---


<a rel="attachment wp-att-974" href="http://www.pureweber.com/article/high-performance-web-sites/couverture_du_livre_high_performances_web_sites_large_media/"><img class=" size-full wp-image-974" src="http://www.pureweber.com/wp-content/uploads/2011/06/couverture_du_livre_high_performances_web_sites_large_media.jpg" alt="" width="500" height="656" /></a>

>同样的网络环境，看着别人的网站“唰”的一下就展现出来，你是否和我一样，心急如焚，盼望着早一点攒出一笔钱，给服务器加点内存？或者你已经挽起袖子，开始研究数据库优化？又或者你在暗自思量着可以把哪些设计模式或编码技巧运用在自己的后台代码里，盼望以此带来性能上的巨幅提升？
>哦，别激动，很多时候事情并没有你想象的这么严重。

这是High Performance Web Sites（以下称HPWS）的译者在序中说到的前两段。对于网站的响应速度的优化，后台的优化和硬件的升级往往伴随着很多困难，诸如成本，工作量等。但实际上前台的优化更为重要也更为高效，为什么呢？HPWS中引入了一条性能黄金法则：

<blockquote>只有10%~20%的最终用户响应时间花在了下载HTML上，其余的80%~90%时间花在了下载页面中的所有组件上。</blockquote>

这就是为什么我们要把精力集中到对于前台的优化上。

HPWS中引入了14条可以实施的方案用于优化前台性能，我将逐条说明。

##减少HTTP请求

减少HTTP请求的有效方法，HPWS中提供了以下几个方法：

<h4>图片地图</h4>

对于一个和图片关联在一起的超链接，使用图片地图能够有效减少请求数，因为这样在不改变显示效果的前提下，将很多张图片改为了一张。

<a rel="attachment wp-att-918" href="http://www.pureweber.com/article/high-performance-web-sites/2011-05-31_170304/"><img class="size-full wp-image-918 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-05-31_170304.jpg" alt="" width="196" height="60" /></a>

<img class="size-full wp-image-919 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-05-31_170708.jpg" alt="" width="579" height="181" />

<h4>CSS Sprites</h4>
这种方法类似于图片地图，也是用于合并图片，而且更为灵活

<a rel="attachment wp-att-929" href="http://www.pureweber.com/article/high-performance-web-sites/2011-05-31_215301/"><img class="size-full wp-image-929 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-05-31_215301.jpg" alt="" width="356" height="198" /></a>

<h4>内联图片</h4>

这种方法是将小块的图片内联为“立即数”，图片的全部数据就在其URL自身之中

<p style="text-align: center"><a rel="attachment wp-att-930" href="http://www.pureweber.com/article/high-performance-web-sites/2011-05-31_220446/"><img class="size-full wp-image-930 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-05-31_220446.jpg" alt="" width="618" height="269" /></a></p>

<h4>合并脚本和样式表</h4>
虽然软件工程师会推荐将代码按照模块化原则分开放在多个小文件中，但这样做会降低性能，因为每个文件都会导致一个额外的HTTP请求，所以合并脚本和样式表也可带来性能的提升。

##使用内容发布网络

需要这样做的原因是，当你的用户在地理上分布很广时，你就有必要在多个地理位置不同的服务器上部署内容。所以使用内容发布网络（CDN）能够使HTTP请求响应的时间缩短。CDN是一组分布在多个不同地理位置的Web服务器，用于更有效地向用户发布内容。

##添加Expires头

Expiers头用于控制浏览器对于缓存的保存时间。因此这一条规则的含义是为你的页面添加长久的Expires头，这样可以有效地将大部分组件保存在缓存中，这样当用户再次访问页面时，浏览器将使用缓存的图片从而减少了HTTP请求的数量，从而节省了时间。

Expires头在服务器端配置，如Apache中有mod_expires模块。使用与不使用Expires头的HTTP响应将如下所示

<p >不使用Expires头</p>
<p ><a rel="attachment wp-att-933" href="http://www.pureweber.com/article/high-performance-web-sites/2011-05-31_230710/"><img class="size-full wp-image-933 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-05-31_230710.jpg" alt="" width="416" height="223" /></a></p>
<p >使用Expires头</p>
<p ><a rel="attachment wp-att-934" href="http://www.pureweber.com/article/high-performance-web-sites/2011-05-31_231849/"><img class="size-full wp-image-934 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-05-31_231849.jpg" alt="" width="543" height="227" /></a></p>

两者在YSlow中对Expires的评价中分别得到了F和A（注：YSlow是FireFox下的一款插件，用于对一个网站速度进行多个方面的评价）。可以看到合适的Expires头对于网站速度的重要性。

##压缩组件

减少HTTP响应的大小来减少响应时间这一点很容易理解，只传输很少的数据，肯定相应有很少的响应时间。减小响应包大小的方法之一是使用gzip编码来压缩HTTP响应包。当然也有一些其他的方法，但都不如压缩组件来得效果好。

压缩组件的配置同样在服务器端，如Apache的mod_gzip及mod_deflate

组件压缩后将在响应头中有显示：

<a rel="attachment wp-att-935" href="http://www.pureweber.com/article/high-performance-web-sites/2011-05-31_234059/"><img class="size-full wp-image-935 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-05-31_234059.jpg" alt="" width="432" height="207" /></a>

对于压缩的内容，压缩所有内容在YSlow中得分最高A，不进行压缩将得到D，只压缩HTML将得到C

##将样式表放在顶部

CSS样式表对于用户而言并不是最重要的，因此若将CSS样式表放在顶部将会延迟页面中其他重要组件的下载，但实际情况与此相反（请到文章末尾给出的链接中体会）将CSS放在顶部的加载速度快于将CSS放在底部。这是因为放在底部的CSS将会阻塞浏览器对于页面的渲染，因为假如没有得到准确的CSS信息，那么对于页面的呈现就显得是一种浪费，所以为了避免这点，浏览器会等到CSS下载完毕后再呈现页面，这样就导致用户界面很长时间会出现“白屏”的现象。显然这种用户体验是不好的，因此将CSS放在底部，将有助于浏览器逐步呈现页面，而不是给用户一个浏览器假死的现象。

将CSS放在底部

<a rel="attachment wp-att-936" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_000358/"><img class="size-full wp-image-936 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_000358.jpg" alt="" width="600" /></a>

将CSS放在顶部

<a rel="attachment wp-att-937" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_001618/"><img class="size-full wp-image-937 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_001618.jpg" alt="" width="511" height="143" /></a>

两种做法在YSlow中分别得到B和A

##将脚本放在底部

与CSS样式表类似，脚本也会阻碍页面的逐步呈现，但解决的方法与CSS样式表正相反：将脚本放在底部将加快浏览器的呈现速度。这涉及到浏览器的行为。浏览器在下载组件时，往往采取并行下载多个组件的策略，并行下载数与浏览器相关，但脚本将阻塞并行下载，其中一个原因是，脚本可能使用document.write来修改页面内容，因此浏览器会等待，以确保页面能够恰当地布局，而另一个原因是为了保证脚本能够按照正确的顺序执行。如果并行下载多个脚本，就无法保证响应是按照特定顺序到达浏览器的，这使得脚本的执行顺序不可预知，假如脚本之间有关联，就有可能产生错误。文章后面的链接中有一个例子，从里面可以很明显地看到js脚本是如何阻塞呈现的。

但是对于阻塞并行下载，不同浏览器的行为并不相同，经我们的观察和讨论得出，有些浏览器阻塞的并非是并行下载，而是页面的渲染，但不论如何，这都影响了页面的呈现，所以将脚本放在页面的底部能够加速页面的呈现。

在firefox中js脚本和其他组件也是并行下载的（使用firebug查看）

<a rel="attachment wp-att-938" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_005102/"><img class="size-full wp-image-938 aligncenter" src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_005102.jpg" alt="" width="600" /></a>

##避免CSS表达式

CSS属性设置中可以接受js表达式，在某些情况下（譬如动态改变样式）非常有用，例如在IE中不支持min-width属性，这样就需要使用CSS表达式来设置使得页面拥有最小宽度。但是浏览器对于CSS表达式的频繁求值会导致CSS表达式的低下性能。在文章末尾提供的链接中的例子可以看到，CSS表达式的求值比想象中要频繁。

需要使用CSS表达式又怕降低性能，解决的方法有两个：一个是使用一次性表达式，在一次执行中重写它自身，这样可以将属性设定为一个确定的值，而避免了表达式的重复求值。

一次性表达式

<a rel="attachment wp-att-939" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_010546/"><img class="size-full wp-image-939 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_010546.jpg" alt="" width="488" height="98" /></a>

另一种方法是使用事件处理器，这样已经脱离了CSS表达式的范畴，但使用这种方法也能达到同样的效果，而且不需要频繁求值，即将对表达式的求值与一个事件关联。

事件处理器

<a rel="attachment wp-att-941" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_011141/"><img class="size-full wp-image-941 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_011141.jpg" alt="" width="511" height="117" /></a>

将事件与函数相关联

<a rel="attachment wp-att-942" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_011540/"><img class="size-full wp-image-942 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_011540.jpg" alt="" width="290" height="51" /></a>

##使用外部JavaScript和CSS

使用内联还是外部的js和CSS是一个很基本的问题，在HPWS中的说法是“纯粹而言，使用内联js和CSS更快一些”但是我个人实际的实验却表示使用外部的js和CSS更快，我想着其中很大一部分原因是并行下载，因为内联或者外部，组件的总大小是固定的，而内联将使得并行下载不能，所以反而会降低速度，虽然这样减少了HTTP请求。但实际上当然还是使用外部js和CSS较好，因为这涉及到缓存的问题，外部js和CSS可以保存在缓存中，这样用户下次就不必下载了，内联的文件则不然。

在内联比外部快的前提下，HPWS提出了两全其美的方法：加载后下载，即使用户下载内联文件，但是在页面中加入脚本，使得在用户加载页面结束后开始下载外部的js和CSS，同时还可以再服务器端添加动态内联，判断用户是否有当前组件的缓存，这可以通过cookie实现。

下载后加载的代码：

<a rel="attachment wp-att-945" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_022528/"><img class="size-full wp-image-945 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_022528.jpg" alt="" width="600" /></a>

##精简JavaScript

减小HTTP相应包的方法，除了压缩组件之外，精简js也是一个有效的方法，精简的含义是从代码中移除不必要的字符以减小其大小，进而改善加载时间的实践。在代码被精简后，所有的注释以及不必要的空白字符都将被移除。这样可以减小需要下载的js脚本。混淆是可以应用在源代码上的另外一种方式。和精简一样，它也会移除注释和空白，同时它还会改写代码。作为改写的一部分，函数和变量的名字将被转换为更短的字符串，这是的代码更加精炼，也更难阅读。但混淆有可能引入错误，混淆会改变js符号，这些都是混淆带来的风险，所以精简是最常用的方式。

精简后的脚本

<a rel="attachment wp-att-956" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_030012/"><img class="size-full wp-image-956 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_030012.jpg" alt="" width="604" height="189" /></a>

混淆后的脚本

<a rel="attachment wp-att-957" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_030045/"><img class="size-full wp-image-957 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_030045.jpg" alt="" width="262" height="289" /></a>

并且不要忘记精简CSS脚本

##移除重复脚本

重复脚本经常发生，因为不同的团队都会向项目贡献代码，但是他们相互之间可能不知道对方已经包含了自己想要的脚本，这样重复包含就发生了，重复的脚本会增加不必要的HTTP请求，从而损伤性能。解决的方法可以在后台添加一个脚本管理的模块，将已经包含的脚本假如一个列表，每次添加前加以检测，对于已经添加的脚本则不再添加。

##配置ETag

ETag的作用于Expires头类似，都是标识了一个组件的缓存时间。不同的是Expires头是通过设置保存时间来设置缓存，而ETag是对一个特定版本的组件产生一个特定字符串，然后在以后的请求中通过比对此字符串来决定是否更新此组件。那么为什么要配置ETag呢，因为ETag通常由组件的某些属性来构造，这些属性相对于特定的、寄宿了网站的服务器来说是唯一的。当浏览器从一台服务器上获取了原始组件之后，又向另外一台不同的服务器发起条件GET请求时，ETag是不会匹配的。因此需要配置ETag的构造方法，使得ETag在不同的服务器上相一致。

ETag举例

<a rel="attachment wp-att-960" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_062605/"><img class="size-full wp-image-960 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_062605.jpg" alt="" width="377" height="75" /></a>

<a rel="attachment wp-att-961" href="http://www.pureweber.com/article/high-performance-web-sites/2011-06-01_062612/"><img class="size-full wp-image-961 " src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-06-01_062612.jpg" alt="" width="417" height="88" /></a>

##使Ajax可缓存

由于Ajax是几种已有技术的组合，因而其优化方法大体可以依照前面的优化方法，如配置缓存，压缩组件，精简脚本，等等。

这就是前台优化的一些策略，每一个都很细节，但就是这些细节决定了页面的呈现速度。在阅读HPWS的过程中，我也不止一次感慨：只有对一种技术了解到细节层面才能称为是专家，大面上的东西很容易就了解了，但关键是能不能深入原理和细节。


##相关链接

<a href="http://stevesouders.com/hpws/rules.php">HPWS一书中各条规则实例</a>
