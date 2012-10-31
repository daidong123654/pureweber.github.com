---
layout: post
title: 'WP Goo Shortener - 基于Goo.gl的Wordpress短网址插件'
description: WP Goo Shortener 是一款基于Google的短网址服务Goo.gl的Wordpress插件，自动为Wordpress的文章生成短网址。提供template tag，以便在主题中自行调用。同时提供shortcode，可以为文章中出现的任意URL生成短链接。
author: 付建宇
github: 7lemon
tags:
  - wordpress
  - '短网址'
  - '插件'
  - 'goo.gl'
  - 'google'

---

![](http://i.min.us/ikuzgg.jpg)

Wordpress插件WP Goo Shortener正式发布啦！下载地址：<a href="http://goo.gl/JE58N">http://goo.gl/JE58N</a>

<h3>插件介绍</h3>
WP Goo Shortener的作用是将文章链接转换成goo.gl短链接并按照指定格式附加到文章末尾，还可以将文章中指定的链接转换为goo.gl短链接后发布。此次发布的版本为1.0版。此插件还会有后续版本发布，敬请关注。

<h3>安装方法</h3>
进入Wordpress后台，在左边栏的“插件”菜单中点击“添加新插件”，直接选择上传WP-Goo-Shortener.zip即可。也可以在服务器端进入Wordpress的wp-content/plugins/目录，将WP-Goo-Shortener.zip中的文件解压到该文件夹内。然后到Wordpress后台激活插件即可。

<h3>使用说明</h3>
激活插件后，再次查看文章，就会将该文章链接的goo.gl短链接显示在文章末尾。您可以通过“GooShortener设置”页面来决定是否显示该链接，或者设置其显示为不同的格式。格式说明：通配符%url和%text在1.0版本中均会被替换成相应的goo.gl短链接。暂不支持自定义%text显示的内容。

使用此插件将文章中的长链接转换为短链接可使用如下形式：

	[wpgoo]链接[/wpgoo]

文章发布后会自动将链接缩短。缩短样式可参见文章开头的下载链接。

如果想在主题中自定义短链接显示位置，请关闭自动在文章末尾添加短链接的选项。然后在编辑主题时，在The Loop中调用以下两个函数：

 - `the_goo_short_url()`：打印文章短链接（仅输出URL）
 - `the_goo_short_link()`：按照设定的格式打印文章短链接

WP-Goo-Shortener 还提供两个函数，开发者可以在其他位置调用这两个函数：

 - `get_goo_short_url($post_id)`：获取ID为$post_id的文章的短链接（仅输出URL）
 - `get_goo_short_link($post_id)`：按照设定格式获取ID为$post_id的文章的短链接

<h3>联系信息</h3>
作者：7lemon
博客：http://www.7lemon.net
邮箱：7lemonsoul (at) gmail.com
