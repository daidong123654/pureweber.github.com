---
layout: post
title: 'PHP开发框架浅析'
description: 使用框架进行应用程序的开发能够有效的提高效率，但通常不建议初学者使用，因为框架隐藏了底层实现细节，不利于初学者夯实基础。本文简要介绍PHP开发框架的原理，并教你自己实现一个简单的PHP框架。
author: 李洪祥
tags:
 - php框架
 - 'php framework'
 - '教程'
 - '实现'
 - '开发php框架'

---


###PHP开发框架是什么

开发框架的定义我没有找到很准确的描述，下面几句话基本概括了开发框架的的功能和用途
<ul>
	<li>框架是一种应用程序的半成品；</li>
	<li>框架就像是人的骨骼一样；</li>
	<li>框架是一组可复用的组件；</li>
	<li>框架是一个可复用的设计构件……</li>
</ul>
简而言之，框架就是制定一套规范或者规则（思想），大家（程序员）在该规范或者规则（思想）下工作。或者说就是使用别人搭好的舞台，你来做表演。

###PHP开发框架有哪些优缺点

<strong>优点：</strong>上面说过，框架其实就是别人把一些基础的代码给封装成库，让程序员来调用，例如表单验证、文件上传、验证码之类的基础功能；框架还把程序的设计架构给确定了，所以程序员只需按照框架规定的方法来写上自己的核心代码，程序就能基本成型了。所以应用PHP开发框架可以使程序员只需专注于应用的核心代码，基础代码可直接调用框架的类库，而且框架的设计架构可以保证团队开发时代码的一致性，所以可以大大提高WEB应用开发的效率。

<strong>缺点：</strong>这世界什么东西都不是完美的，所以利用框件架开发有利也有弊。PHP框架缺点就是过分封装了PHP的基础函数，对与一个PHP新手来说，他可能不需要学习PHP的任何基础函数，仅靠翻阅框架的说明文档和调用框架封装好的接口就能完成一个完整的PHP应用程序，从某方面说这样可以降低PHP应用开发的技术要求，但是这样对于学习来说是不利的，最后会导致过于依赖开发框架。在一个论坛里看到这样一句话评论PHP开发框架：
<blockquote>学之者生，用之者死</blockquote>

##MVC架构


###什么是MVC架构

MVC是软件工程中的一种软件架构模式，MVC把软件系统分成三个基本部分：模型（Model）、视图（View）和控制器（Controller）。

<strong>模型（Model）“</strong>数据模型”（Model）用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法。“模型”有对数据直接访问的权力，例如对数据库的访问。“模型”不依赖“视图”和“控制器”，也就是说，模型不关心它会被如何显示或是如何被操作。但是模型中数据的变化一般会通过一种刷新机制被公布。为了实现这种机制，那些用于监视此模型的视图必须事先在此模型上注册，从而，视图可以了解在数据模型上发生的改变。

<strong>视图（View）</strong> 视图层能够实现数据有目的的显示（理论上，这不是必需的）。在视图中一般没有程序上的逻辑。为了实现视图上的刷新功能，视图需要访问它监视的数据模型（Model），因此应该事先在被它监视的数据那里注册。

控制器（Controller） 控制器起到不同层面间的组织作用，用于控制应用程序的流程。它处理事件并作出响应。“事件”包括用户的行为和数据模型上的改变。

![WEB程序中的MVC架构](http://www.pureweber.com/wp-content/uploads/2012/04/mvc-300x240.png)


###MVC架构在WEB开发中的应用


MVC在WEB应用程序中应用较广泛，右图是一个基于MVC的WEB请求处理过程。

首先，用户发送一个请求给控制器（Controller），控制器根据用户的请求向数据模型（Model）发送数据需求，数据模型根据需求进行相应的数据处理（如访问数据库、进行相应的计算等）后，把数据结果传回控制器，控制器得到数据后，就可以调用视图（View），生成一个页面，返回给用户。

##开发一个简单的PHP框架

上面说了那么多，下面我们动手开发一个简单的PHP框架程序，框架听起来好像挺复杂的，其实还是很简单的，只要弄懂了它的思想就没有问题。我们框架的名字就叫small-framework吧。

###粗略的分析用户请求的处理过程

我们知道PHP每次接收到请求时都要初始化全部资源，处理完毕后再释放全部的资源，PHP框架也是如此。框架接收到用户的请求后，需要一个初始化的过程，在初始化时实例化框架的核心模块，然后在把请求传送给框架的相应模块进行处理。因为不可能所有的请求都使用同一个控制器，除非程序功能非常简单，所以在初始化完成后，我们还需要根据用户的请求来调用相应的控制器，所以我们需要一个分发器（Dispatcher）来对用户的请求进行分发。在控制器里，我们就可以调用数据模型和视图来处理用户的请求了。

![粗略的分析请求的处理过程](http://www.pureweber.com/wp-content/uploads/2012/04/Screenshot.png)

###细致的分析用户请求的处理过程

上面粗略的分析了用户请求的处理流程，下面进行更加精细的分析

从上面的分析可以知道，要处理用户的请求需要先初始化框架的核心模块，如分发器模块，所以用户的请求首先需要被重定向至一个初始化页面，重定向可以使用.htaccess文件来实现，在我们这个框架里，我们首先把所有的请求都重定向至index.php里，在index.php里面完成初始化操作：初始化核心模块，我们还可以在初始化时读入框架的配置文件信息，然后调用分发器把请求分发到相应的控制器，实例化这个控制器，并调用控制器中的方法来处理用户的请求。在控制器里，我们可以获取用户的输入，判断用户的请求，然后调用相应的数据模型进行数据处理，控制器得到数据后，把数据传给视图，视图根据得到的数据返回一个页面给用户，请求结束。

![细致的分析用户请求的处理过程](http://www.pureweber.com/wp-content/uploads/2012/04/Screenshot-3.png)

###框架的文件结构

根据上面的分析，我们可以列出small-framework的文件结构
<ul>
	<li>Core/                    框架的核心模块
<ul>
	<li>Dispatcher.php</li>
	<li>Controller.php</li>
	<li>Model.php</li>
	<li>View.php</li>
</ul>
</li>
	<li>Controller/          自定义的控制器</li>
	<li>View/                   自定义的视图</li>
	<li>Model/                自定义的数据模型</li>
	<li>index.php           框架的单一入口</li>
	<li>config.php          框架的配置文件</li>
	<li>.htaccess             将请求重定向至index.php</li>
</ul>

###开始编码

有了以上的分析，框架工作的基本流程我们基本清楚了，下面我们就按照请求的处理顺序来开始编码

首先是.htaccess文件，

	<IfModule mod_rewrite.c>
		RewriteEngine On
		RewriteBase /small-framework                  #基于框架的根目录进行重定向
		RewriteCond %{REQUEST_FILENAME} !-f    #如果用户请求的不是一个文件
		RewriteCond %{REQUEST_FILENAME} !-d   #如果用户请求的不是一个目录
		RewriteRule . index.php [L]                       #则重定向至index.php
	</IfModule>

现在如果用户不是在请求js，css或者图片等静态文件时，用户的请求都会被重定向至index.php，下面我们编写index.php

{% highlight php %}
<?php
define('ROOT_PATH', str_replace('\\', '/', dirname(__FILE__)));//定义根目录 
/* 加载核心模块 */ 
require ROOT_PATH.'/config.php';//主要设置 
require ROOT_PATH.'/core/Dispatcher.php';//分发器模块 
$dpt = new Dispatcher();//实例化请求分发器 
$return_status = $dpt->run();

echo $return_status;

exit(0);
?>
{% endhighlight %}


用户的请求在框架初始化完成后被传送到分发器中，分发器其实就是确定对用户请求分发的依据，我们可以根据URI分段来确定控制器，例如用户请求http://www.example.com/aaa/bbb，那么分发器就认为需要调用控制器aaa里面bbb方法来处理用户请求；还可以通过查询串的方式，例如对于请求http://www.example.com?controller=aaa&amp;method=bbb，分发器就知道需要调用aaa控制器里面的bbb方法。在我们的small-framework里，我们采用URI分段的形式来对请求进行分发。分发器的代码如下：


{% highlight php %}
<?php
class Dispatcher {
	private $path; 

	public function __construct() 
	{
		//实例化分发器时得到用户请求的URI 
		$this->path = $_SERVER['PATH_INFO'];
	}

	public function run()
	{
		//分析URI，得到相应的控制器和方法
		$this->path = trim($this->path, '/');
		$paths = explode('/', $this->path);

		//得到控制器类名和方法名
		$control = array_shift($paths);
		$method = array_shift($paths);

		//如果控制器类名和方法名为空，则默认为“index”
		if($control == '') $control = 'index';
		if($method == '') $method= 'index';

		//根据框架的文件结构，得到控制器类的文件路径
		$control_file_name = ROOT_PATH.'/controller/'.$control.'.php';

		if(file_exists($control_file_name))
		{
			include_once($control_file_name);

			$controller_name = $control.'_Controller';
			if(class_exists($controller_name))
			{
				//实例化控制器
				$control = new $controller_name();
				if(method_exists($controller_name, $method))
				{
					//如果用户请求的方法存在，则调用之
					$control->$method();
					return OK_200;
				}
				else return ERROR_404';
			}
			else return ERROR_404;
		}
		else return ERROR_404;
	}
};
?>
{% endhighlight %}


分发器通过`$contorl->$method()`调用了请求指定的控制器方法，现在我们就可以试验一下，在controller/下面建立一个aaa.php，在里面声明一个名为aaa_Controller的类和名为bbb的访问权限为public的方法，就可以通过 `[你的测试地址]/aaa/bbb` 来访问这个控制器了。

现在我们的small-framework实际上还不能被称作是一个框架，因为它还没有定义一些基本的操作，如调用数据模型、视图等，这些基本操作我们定义在core/下的Controller.php、Model.php、View.php里，用户自定义的控制器、模型和视图需要继承自这三个父类。我们需要在index.php中加载者三个父类。

在index.php中，除了加载核心模块以外，我们还加载了用户自己写的Model、Controller和View需要继承的父类，在父类里面我们需要定义一些框架的基本操作供用户调用


{% highlight php %}
<?php
/* 加载Controller需要继承的父类 */
require ROOT_PATH.'/core/Controller.php';

/* 加载Model需要继承的父类 */
require ROOT_PATH.'/core/Model.php';

/* 加载View需要继承的父类 */
require ROOT_PATH.'/core/View.php';
?>
{% endhighlight %}


首先是Controller.php，我们默认在实例化Controller时就实例化View，用户在控制器中可直接使用View中的函数；当然也可以让用户来手动载入View。代码如下


{% highlight php %}
<?php
class Controller{

	protected $view = NULL;
	protected $model = NULL;

	public function __construct()
	{
		//默认实例化Controller时就实例化View
		$this->view = new View();
	}

	//用户通过model_name来手动载入相应的模型
	protected function load_model($model_name)
	{
		$model_file_name = ROOT_PATH.'/model/'.$model_name.'.php';
		require_once($model_file_name);
		$this->model = new $model_name();
	}
};
?>
{% endhighlight %}


在View里我们定义了show方法，show方法的参数是视图文件名和传给视图文件的数据，用户在控制器里可以调用show方法来输出指定的视图


{% highlight php %}
<?php
class View{
	public function show($view_file, $data=array())
	{
		$view_file_name = ROOT_PATH.'/view/'.$view_file.'.php';
		if(!file_exists($view_file_name)) return FALSE;

		//把数组展开，键名做变量名，键值做变量值
		extract($data);

		//引入view文件
		include($view_file_name);
		return TRUE;
	}
};
?>
{% endhighlight %}


在Model.php里面我们可以封装一些数据库查询，在所有的查询之前对sql语句进行过滤，以保证数据库的安全


{% highlight php %}
<?php
class Model{

	//数据库连接
	protected $link = NULL;

	public function __construct()
	{
		$this->link = mysql_connect(MYSQL_HOST, MYSQL_USER, MYSQL_PASS);
		mysql_select_db(MYSQL_DB, $this->link);
		mysql_query("SET NAMES ".MYSQL_CHARSET);
	}

	/** 检查输入的sql语句，过滤敏感字符*/
	private function _check($sql)
	{
		/*此处添加对$sql的过滤*/
		return $sql;
	}

	/** 执行sql命令，成功返回结果集和TRUE，失败返回FALSE	 */
	protected function query($sql)
	{
		return mysql_query($this->_check($sql));
	}

	/** 执行sql查询，返回结果数组，查询失败返回false*/
	protected function fetch_array($sql)
	{
		$res = $this->query($sql);
		return mysql_fetch_array($res);
	}

	/** 还可以添加其他的数据处理操作*/
};
?>
{% endhighlight %}


到现在，我们的small-framework的就基本完成了，small-frame的很简单，但是作为学习软件的mvc架构和php框架的入门应该足够了，而且其他的大型PHP框架（这里的大型是相对于small-framework来说的）的工作原理于small-framework也都是大同小异的，大型框架中的分发器设置的会更加合理，还会有很多使用的类库供用户调用，有时间的话建议看看大型框架的源代码，学习其中的思想，大型框架里面还有许多代码优化可供学习。所以不要被某一种框架约束了思想，对于php框架来说

> 学之者生，用之者死
