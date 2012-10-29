---
layout: post
title: 'LAMP编码'
tags:
  - apache
  - mysql
  - php
  - '%e7%bc%96%e7%a0%81'

---

<p>LAMP环境配置的重要一步即编码配置。显然，没有统一的编码，就没有正常的显示。没有人希望自己的页面上显示一串问号，或者是一堆方块。那么，就要保持编码统一，才能得到正常的显示效果。总结起来，需要同时保持下四点的一致：</p>
<p>
<ul>
	<li>数据库编码</li>
	<li>数据库连接编码</li>
	<li>网页文件编码</li>
	<li>HTML Head中的编码声明</li>
</ul>
</p>
<p>下面逐一对其进行说明。</p>
<h3>数据库编码</h3>
<p>这里的编码指的是数据在数据库中存储所使用的编码。Mysql数据库很奇怪，默认使用的是Latin1编码。我们在创建数据库和表单的时候要指定编码。以下均指定为utf8编码。在创建数据库和表单，字段的语句后面加上参数：</p>

CHARACTER SET utf8  (COLLATE utf8_general_ci 可选)

<p>这样保证数据库内存储的内容使用的是utf8编码。如果先前已经存入非utf8编码的数据，可以执行如下语句：</p>
<p>修改数据库用utf8：</p>
[coolcode lang="mysql"]
alter database_name character set utf8;
[/coolcode]
<p>修改表默用utf8：</p>
[coolcode lang="mysql"]
alter table type character set utf8;
[/coolcode]
<p>修改字段用utf8：</p>
[coolcode lang="mysql"]
alter table type modify type_name varchar(50) character set utf8;
[/coolcode]

<p>替换上述语句中的相应参数以适合你的数据库，执行即可。</p>
<h3>数据库连接编码</h3>
<p>数据库连接编码指的是客户端与数据库交互时所使用的编码。例如，数据库编码是utf8，但是我发出一条GBK编码的查询指令，返回结果也是GBK编码，那么显示出来的内容就有可能是乱码。而这个编码是由连接到Mysql服务器的客户端（终端，PHP程序等）指定的。如果想要使连接编码也为utf8，在发出查询语句之前需要执行如下语句：</p>
[coolcode lang="mysql"]
SET NAMES ‘utf8’;
[/coolcode]
它相当于下面的三句指令：
[coolcode lang="mysql"]
SET character_set_client = utf8;
SET character_set_results = utf8;
SET character_set_connection = utf8;
[/coolcode]
<h3>修改数据库配置文件</h3>
首先终止mysql服务，然后找到mysql的配置文件my.cnf。在[client]和[mysqld]下面均加上default-character-set=utf8，保存并关闭。这种方法一劳永逸，省去了许多麻烦。具体my.cnf在什么位置，依安装情况而定，不同的系统，不同的版本，不同的安装方式放置的位置都不同（很奇怪）。设置完成后，重启mysql服务。
<h3>网页文件编码</h3>
数据库的编码都设置好了，那我们编辑的网页文件的编码也要和数据库的编码统一。这里的编码指的就是文件编码。查看你的文本编辑器设置，看看默认编码是否是utf8编码。如果不是，则需要将文件编码转换成utf8编码。
Linux系统可以使用如下命令：
iconv -f 原始编码 -t 目标编码 文件名 &gt; 新文件名
Windows下有很多文本编辑器例如Notepad++可以转换文本文件编码。
<h3>HTML Head中的编码声明</h3>
显然，在&lt;head&gt;&lt;/head&gt;内加入meta标签：
[coolcode lang="html"]
meta http-equiv="Content-Type" content="text/html; charset=UTF-8" 
[/coolcode]
UTF8和UTF-8是一样的。
<h3>其他编码设置</h3>
<h4>Apache编码</h4>
Apache同样要设置成UTF8编码。例如我的Apache配置文件在 /etc/apache2/apache2.conf，但是配置文件中没有指定字符集的语句。查看配置文件发现这样一句话：Include /etc/apache2/conf.d/ 。进入到conf.d文件夹，打开charset文件，将AddDefaultCharset uft8前的#去掉。
如果你的Apache配置文件结构和我的不一样，也可以直接在你的配置文件里加入AddDefaultCharset uft8。
然后，重启Apache服务。
<h4>PHP编码</h4>
找到php.ini文件。（我的文件在 /etc/php5/apache2/php.ini），查找 default_charset = "utf8" 。如果这句话前面有分号，去掉分号后保存。如果找不到这句话，随便找个位置添加这句话即可。
phpmyadmin编码
这个就没什么好说的了。它只是一个PHP程序，只要前面的编码都设置好了，这个一般不会出问题。
<h3>参考：</h3>
<a title="mysql编码设置" href="http://goo.gl/8bJEh" target="_blank">mysql 编码设置</a>
<a title="utf8" href="http://jiangjiao.javaeye.com/blog/679093" target="_blank"> MysQL数据库中utf8_unicode_ci与utf8_general_ci的区别</a>
<a title="Linux 下GB2312编码转换UTF8方法" href="http://www.lslnet.com/linux/docs/linux-28.htm" target="_blank"> Linux下GB2312编码转换UTF-8方法</a>
