---
layout: post
title: 'PHP include/require路径问题'
tags:
  - include
  - include_path
  - path
  - php

---

include/require语句用于包含并运行指定文件。具体用法见PHP手册。

使用这两条语句时要十分注意路径的使用。一些人会习惯使用相对路径（比如我），如果不对PHP进行任何配置就直接使用相对路径，那肯定会撞南墙。例如如下目录结构：
[coolcode]
/
/common/
/lib/
[/coolcode]
/index.php 需要require /common/header.php 则直接 require 'common/header.php'; 即可。这种语句是不会出错的，PHP会从当前目录向下层目录寻找header.php。问题来了，如果 /common/header.php 需要require /lib/config.php 怎么办？直接的想法是这样做：
<p style="padding-left: 30px">[coolcode lang="php"]require '../lib/config.php';[/coolcode]</p>
我第一次就是怎么做的，然后执行脚本的时候PHP抛出了找不到这个文件的错误。解决办法有二（或更多）：
<h4>方法一：使用绝对路径</h4>
<p style="padding-left: 60px">[coolcode lang="php"]require dirname(__FILE__).'/../lib/config.php';[/coolcode]</p>
<p style="padding-left: 30px">使用dirname(__FILE__)将获得当前文件所在的绝对路径。这种方法也即使用绝对路径来指定文件位置。</p>

<h4>方法二：设定include_path</h4>
<p style="padding-left: 30px">指定include_path。参考自PHP文档，include_path string：指定一组目录用于 require()，include() 和 fopen_with_path() 函数来寻找文件。格式和系统的 PATH 环境变量类似：一组目录的列表，在 UNIX 下用冒号分隔，在 Windows 下用分号分隔。 既然这样，只要修改PHP配置文件，将脚本所在的根目录加入到include_path就可以使用相对目录了。例如项目脚本根目录在 /var/www/project 则编辑PHP配置文件，在include_path中加入 /var/www/project 。这样，我们首先想到的相对目录办法就可以使用了。</p>
实际上在执行include / require等语句的时候，PHP会首先查找include_path中指定的目录内是否有对应文件，如果没有则将path置成当前文件所在的目录，认为当前目录为根目录并不支持相对路径。除非使用绝对路径，否则不能查找同级其他目录的文件。
