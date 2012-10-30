---
layout: post
title: 网站编码设置及乱码问题解决
description: 在开发网站时，经常会遇到各种各样的乱码问题，可能涉及到网页编码、数据库编码、数据库连接编码等。本文说明了在Web开发过程中保持各处编码一致，从而杜绝乱码现象的方法。通过保持网页、数据库、数据库连接、服务器端配置等的编码一致，彻底解决乱码问题。
author: 付建宇
github: 7lemon
tags:
  - '网站编码'
  - '乱码'
  - '编码'
  - '数据库'
  - '网页'
  - '文件'
  - '解决'
---

LAMP环境配置的重要一步即编码配置。显然，没有统一的编码，就没有正常的显示。没有人希望自己的页面上显示一串问号，或者是一堆方块。那么，就要保持编码统一，才能得到正常的显示效果。总结起来，需要同时保持下四点的一致：

- 数据库编码
- 数据库连接编码
- 网页文件编码
- HTML Head中的编码声明

下面逐一对其进行说明。

##数据库编码

这里的编码指的是数据在数据库中存储所使用的编码。Mysql数据库很奇怪，默认使用的是Latin1编码。我们在创建数据库和表单的时候要指定编码。以下均指定为utf8编码。在创建数据库和表单，字段的语句后面加上参数：

	CHARACTER SET utf8  (COLLATE utf8_general_ci 可选)

这样保证数据库内存储的内容使用的是utf8编码。如果先前已经存入非utf8编码的数据，可以执行如下语句：

修改数据库用utf8：

{% highlight sql %}
alter database_name character set utf8;
{% endhighlight %}

修改表默认用utf8：

{% highlight sql %}
alter table type character set utf8;
{% endhighlight %}

修改字段用utf8：

{% highlight sql %}
alter table type modify type_name varchar(50) character set utf8;
{% endhighlight %}

替换上述语句中的相应参数以适合你的数据库，执行即可。

##数据库连接编码

数据库连接编码指的是客户端与数据库交互时所使用的编码。例如，数据库编码是utf8，但是我发出一条GBK编码的查询指令，返回结果也是GBK编码，那么显示出来的内容就有可能是乱码。而这个编码是由连接到Mysql服务器的客户端（终端，PHP程序等）指定的。如果想要使连接编码也为utf8，在发出查询语句之前需要执行如下语句：
{% highlight sql %}
SET NAMES 'utf8';
{% endhighlight %}

它相当于下面的三句指令：

{% highlight sql %}
SET character_set_client = utf8;
SET character_set_results = utf8;
SET character_set_connection = utf8;
{% endhighlight %}

##修改数据库配置文件

首先终止mysql服务，然后找到mysql的配置文件my.cnf。在`[client]`和`[mysqld]`下面均加上`default-character-set=utf8`，保存并关闭。这种方法一劳永逸，省去了许多麻烦。具体my.cnf在什么位置，依安装情况而定，不同的系统，不同的版本，不同的安装方式放置的位置都不同（很奇怪）。设置完成后，重启mysql服务。

##网页文件编码

数据库的编码都设置好了，那我们编辑的网页文件的编码也要和数据库的编码统一。这里的编码指的就是文件编码。查看你的文本编辑器设置，看看默认编码是否是utf8编码。如果不是，则需要将文件编码转换成utf8编码。

Linux系统可以使用如下命令：

	iconv -f 原始编码 -t 目标编码 文件名 > 新文件名

Windows下有很多文本编辑器例如Notepad++可以转换文本文件编码。

##HTML Head中的编码声明

显然，在`<head></head>`内加入meta标签：

{% highlight html %}
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
{% endhighlight html %}

UTF8和UTF-8是一样的。

##其他编码设置

### Apache编码

Apache同样要设置成UTF8编码。例如我的Apache配置文件在 /etc/apache2/apache2.conf，但是配置文件中没有指定字符集的语句。查看配置文件发现这样一句话：Include /etc/apache2/conf.d/ 。进入到conf.d文件夹，打开charset文件，将AddDefaultCharset uft8前的#去掉。

如果你的Apache配置文件结构和我的不一样，也可以直接在你的配置文件里加入AddDefaultCharset uft8。

然后，重启Apache服务。

### PHP编码
找到php.ini文件。（我的文件在 /etc/php5/apache2/php.ini），查找 default_charset = "utf8" 。如果这句话前面有分号，去掉分号后保存。如果找不到这句话，随便找个位置添加这句话即可。

##参考：
 - [Mysql编码设置](http://goo.gl/8bJEh)
 - [MysQL数据库中utf8_unicode_ci与utf8_general_ci的区别](http://jiangjiao.javaeye.com/blog/679093) 
 - [Linux下GB2312编码转换UTF-8方法](http://www.lslnet.com/linux/docs/linux-28.htm)
