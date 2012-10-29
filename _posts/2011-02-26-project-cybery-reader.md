---
layout: post
title: '项目 - Cybery Reader'
tags:
  - cybery-reader

---

<small>这是2011年寒假进阶班的一个任务。如果你对这个任务感兴趣，欢迎参与，并与我们共享你的成果。或者你也可以报名参加我们的课程：<a href="http://www.pureweber.com/join/">报名：程序设计与实践2 – Web开发</a></small>

接下来正式进入我们的项目开发，要开发的东西是一个RSS阅读器。名字暂定为Cybery Reader。

第一阶段的任务安排如下：

<strong>一、数据库访问的封装</strong>

分配给：手套

编写一个类 CDB ，将php的mysql库进行一下封装，提供更加简单便捷的接口。需要至少提供以下几个接口：
<ul>
	<li>connect(host, user, pass, dbname) : 用user和pass连接到host上的dbname数据库</li>
	<li>close() : 关闭数据库连接</li>
	<li>fetch(table_name, field_name, value) ： 从数据表table_name中取出一条记录，满足条件：字段名为field_name的字段，其值为value</li>
	<li>get(table_name, condition) ：从数据表table_name中取出所有符合条件condition的记录</li>
	<li>insert(table_name, data) ：向数据表table_name中插入一条记录，data是一个关联数组，键名为字段名，值为字段的值</li>
	<li>update(table_name, id_value, data) ：更新数据表table_name中的id为id_value的记录，data是一个关联数组，键名为字段名，值为字段的值</li>
	<li>delete(table_name, id_value)：删除数据表table_name中的id为id_value的记录</li>
	<li>query(sql) ：执行数据库查询sql</li>
	<li>queryf(fsql, v1, v2, ...) ： 具有可变参数个数的函数，类似于sprintf，fsql定义了数据格式，v1, v2等变量定义了要替换的值，然后将替换后的字符串作为数据库查询进行执行。</li>
</ul>
<strong>二、RSS Feed爬虫 (RSS Crawler)</strong>

分配给：小雨

编写一个类 RSSCrawler ，用于读取远程的RSS Feed。需要至少提供以下几个接口：
<ul>
	<li>open(url) : 打开一个RSS Feed，返回是否打开成功</li>
	<li>read_item() : 读取下一个条目，返回一个关联数组</li>
	<li>valid() : 当前打开的Feed是否是一个有效的RSS Feed，返回true 或 false</li>
	<li>close() : 关闭</li>
</ul>
<strong>三、PSD to HTML</strong>

分配给：咸鱼

将<a href="http://www.pureweber.com/wp-content/uploads/cybery-reader-design.psd" target="_blank">PSD设计稿</a>转换为一个静态HTML页面。要求如下：
<ul>
	<li>左右两个侧边栏的宽度固定，中间部分的宽度可变</li>
	<li>上方的“这里是提示信息”一栏，用JQuery实现向下滑动的效果</li>
	<li>页面应符合web标准，并兼容IE6+, FF, Safari, Chrome</li>
	<li>最终应产出如下文件
<ul>
	<li>/main.html</li>
	<li>/css/style.css</li>
	<li>/css/images/所有样式配图</li>
	<li>/images/所有内容图片</li>
</ul>
</li>
</ul>
