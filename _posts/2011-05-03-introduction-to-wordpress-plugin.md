---
layout: post
title: WordPress插件制作简介
tags:
  - plugin
  - wordpress
  - '%e5%bc%80%e5%8f%91'
  - '%e6%8f%92%e4%bb%b6'

---

<h3>第二次分享会详情</h3>

<a href="http://www.pureweber.com/wp-content/uploads/2011/05/shown.jpg"><img src="http://www.pureweber.com/wp-content/uploads/2011/05/shown-300x199.jpg" alt="" title="分享现场" width="300" height="199" class="alignright size-medium wp-image-733" style="clear:both" /></a>

<table>
<tr><th>主讲人</th><td>田大龙</td></tr>
<tr><th>题目</th><td>Wordpress插件开发</td></tr>
<tr><th>时间</th><td>2011-4-24</td></tr>
<tr><th>&nbsp;</th><td><a href="http://www.pureweber.com/wp-content/uploads/2011/05/wordpress插件.ppt">下载课件</td></tr>
</table>



-------------华丽的分割线-------------

这里并没有手把手教你制作一个插件出来，本篇文章意在向大家介绍WordPress插件制作的基本步骤以及需要了解的必要知识，详细的WP插件制作教程网上有很多，本文最后也推荐了一些比较好的教程网站。

OK，言归正传.

<h3>1:介绍</h3>
简单定义：
WordPress插件是一个能够扩展WordPress博客功能的PHP脚本程序或函数集。
目的是为了使WordPress变得扩展性强，易修改和个性化。而且不需要修改WordPress的核心代码。

<h3>2:新建一个插件</h3>

<strong>2.1 名字，文件，位置</strong>

<strong>2.1.1 插件名</strong>
因为一个网站上可能会装很多个WordPress插件，所以要确保插件名字的唯一性。

<strong>2.1.2 插件文件</strong>
新建一个文件夹，将你插件的文件放入/wp-content/plugins/中，当然这个目录的名字也要唯一。

<strong>2.1.3 Readme 文件</strong>
无论是插件还是其他什么应用程序，README都是必不可少的。

<strong>2.1.4 主页</strong>

如果想制作一个较好的插件，最好为它设置一个主页，介绍关于插件的版本信息，使用说明等内容。

<strong>2.2 头信息</strong>

<strong>2.2.1 标准插件信息</strong>

需要在PHP头部插入标准的插件信息，WordPress才能识别你的插件。

形式如下:

[coolcode lang="php"]
/*
Plugin Name: Name Of The Plugin
Plugin URI: http://URI_Of_Page_Describing_Plugin_and_Updates
Description: A brief description of the Plugin.
Version: The Plugin's Version Number, e.g.: 1.0
Author: Name Of The Plugin Author
Author URI: http://URI_Of_The_Plugin_Author
*/
[/coolcode]

最主要的是Plugin Name，WordPress主要是识别它来显示出一个插件。

<strong>2.2.2 授权信息</strong>

通常大家就直接用标准的授权信息当作自己的授权信息。很多的插件用得就是GPL。加入下面的文字，

可以简要的说明GPL：

[coolcode lang="php"]/* Copyright Glove glovenone@gmail.com */[/coolcode]

<strong>2.3 开始编程</strong>

<strong>2.3.1 WordPress插件钩子</strong>

API：Application Programming Interface 应用编程接口。

wordpress插件主要使用一种叫hook的接口：

<strong>A.动作 (Action)：</strong> 动作是 WordPress 运行到某些环节，或者在某些事件发生时，就会被执行的一种钩子。比如说发表一篇文章、更换主题或者访问后台的某个管理界面，这些都是一件事件的例子。而插件则可以指定某些 PHP 函数来响应这些事件

使用动作来挂载插件的基本步骤如下：

在插件代码中定义当某个事件发生时，需要执行的 PHP　函数用add_action() 把这个函数注册到动作执行挂勾上把插件源码放到 WordPress 指定的地方，然后启用它

添加一个filter的格式为:

[coolcode lang="php"]add_action ( 'hook_name', 'your_function_name', [priority], [accepted_args] );[/coolcode]

例子:

当访客访问站点后，执行的是index.php，即WordPress的入口程序。index.php先后载入一些基本参数（如数据库信息、默认语言），进行一些必要的检查（如WordPress是否已经安装），然后载入我们的插件，当然，前提是这个插件已经启用。在插件中，我们输入以下代码：

[coolcode lang="php"]
function print_my_feed(){
    //do something
    echo 'Hello, boy!';
}
add_action('wp_head','print_my_feed');
[/coolcode]


如代码所示，wp_head就是一个Action名，当WordPress执行到wp_head这个Action时，它将执行我们插入的print_my_feed函数。这里的函数既可以做某些后台的操作，如update_option，也可以用于前台的输出，如echo，做一些适合在该Action发生的动作。

<strong>B.过滤器 (filter)</strong>：是WordPress加载的，当文本被存入数据库或发送到浏览器之前，filter可用来对其进行多种类型的处理。使用filter，你的插件可以使用定义在其中的PHP函数来对文本进行多种处理。

添加一个filter的格式为：

[coolcode lang="php"]add_filter('hook_name','your_filter',[priority],[accepted_args]);[/coolcode]

例子:

[coolcode lang="php"]
function addContent($content = “”) {
    //the content we modified
    $data = 'the data we added';
    $content .= $data; //add the data to the content originally
    return $content;
}
add_filter(“the_content”, addContent);
[/coolcode]

调用add_filter函数时,必须在数据显示、保存等操作之前进行.

<strong>2.3.2 保存插件数据到数据库</strong>

WordPress有多种方法将插件数据保存到数据表，我们既可以创建新的数据表，也可以用post_meta对单独文章、页面、附件等相关数据进行处理，也可以用“option”，这会是一个很常用的东西。

<strong>2.3.3 WordPress的option机制</strong>

WordPress有一套在数据库中保存、更改、读取独立的、有名字的数据（”options”）的机制，安装WP后，如果访问数据库，会发现里面有一个叫wp_option的数据表，它保存的内容就是有关我们博客的一些信息：地址，站点名称，文章属性等内容。我们可以通过调用option函数对数据库进行相关的添加、获取、更新等功能。
<div><strong>2.4  i18n你的插件</strong></div>
一个很有意思的词：i18n—internationalization，国际化的缩写，之所以如此缩写是因为从i到n有18个字母，它意指让我们的插件能够在世界上使用，即可以被翻译成各国语言。我们需要在定义字符串和输出字符串时做一些操作。

<h3>3:插件开发建议</h3>
<ul>
	<li>要遵循标准，统一标准可以给自己和他人同时带来方便，“WordPress Coding Stardards”。</li>
</ul>
<ul>
	<li>函数不要重名，否则可能会造成混乱，通常加一个不会重复的前缀就好了。</li>
	<li>代码中不要把WordPress前缀写成“wp_”，要写成$wpdb-&gt;prefix，虽然它们的意思相同。</li>
</ul>
<ul>
	<li>为了提高你插件的效率和可用性，尽量减少向数据写东西的次数，并且只“Select”你需要的字段。不要用“Select *”这样的语句，这种插件会让你WP的速度变慢很多。</li>
</ul>
<h3>4:相关资源</h3>
<ol>
	<li><a href="http://codex.wordpress.org/Plugin_API">wordpress官方API</a></li>
	<li><a href="http://liucheng.name/864/">WordPress插件制作入门教程</a></li>
	<li><a href="http://fairyfish.net/2007/12/28/write-plugin-by-yourself/">自己动手写 WordPress 插件</a></li>
	<li><a href="http://www.wpcourse.com/tag/wordpress%E6%8F%92%E4%BB%B6">WordPress教程网</a> -  WordPress插件的各种信息,也有关于wordpress其他的信息</li>
	<li><a href="http://plugins.wopus.org/tutorial">WordPress插件介绍</a></li>
	<li><a href="http://paranimage.com/">帕兰映像</a> - 不仅有WP的东西,是一个一个关于web的很不错的网站</li>
</ol>
