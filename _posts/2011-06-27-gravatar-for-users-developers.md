---
layout: post
title: '使用Gravatar - 普通用户&开发者'
description: 本文介绍如何使用Gravatar的头像服务。从普通用户和开发者两个角度，介绍Gravatar头像服务的使用和开发方法。
author: 张雄
github: bearzx
tags:
  - gravatar
  - '头像服务'
  - '开发'

---

##Gravatar是什么

<a rel="attachment wp-att-860" href="http://www.pureweber.com/article/gravatar-for-users-developers/2011-05-08_121028/"><img class=" size-full wp-image-860" src="http://www.pureweber.com/wp-content/uploads/2011/06/2011-05-08_121028.png" alt="" width="530" height="345" /></a>

Gravatar是www.gravatar.com 推出的一项服务，意为“全球通用头像”。如果在gravatar上注册了账号并在gravatar服务器上放置了头像，那么当在支持gravatar的blog或留言本上发言时，只要提供email地址，就能够显示与email相关联的头像。这样就为大家提供了一个统一管理多个头像的平台，只要站点支持gravatar，就不必特意为每个站点单独上传头像，省去了麻烦。

<a rel="attachment wp-att-861" href="http://www.pureweber.com/article/gravatar-for-users-developers/1-2/"><img class="size-large wp-image-861 " src="http://www.pureweber.com/wp-content/uploads/2011/06/1-1024x384.png" alt="" width="600" /></a>

##普通用户

作为一名普通的用户，如何使用Gravatar呢？

首先到gravatar上注册账号，很简单，只要填写一个常用的email地址，填写好密码，然后到邮箱里确认，就注册好了一个gravatar账号。随后用账号登陆gravatar，就可以开始为账号添加头像了，每个email可以和一个头像关联，上传头像的方式有很多种。

<a rel="attachment wp-att-862" href="http://www.pureweber.com/article/gravatar-for-users-developers/1-3/"><img class=" size-full wp-image-862" src="http://www.pureweber.com/wp-content/uploads/2011/06/1.jpg" alt="" width="533" height="155" /></a>

选择一种，并选好准备制作成头像的图片。随后进入编辑界面。

<a rel="attachment wp-att-863" href="http://www.pureweber.com/article/gravatar-for-users-developers/2-2/"><img class=" size-full wp-image-863" src="http://www.pureweber.com/wp-content/uploads/2011/06/2.jpg" alt="" width="479" height="357" /></a>

简单编辑后，就截取好了gravatar头像，接下来为头像选择等级，不同的等级会决定你的头像是否在站点中显示，假如你的头像过于限制级，则在不支持此等级的站点中不会显示，而只会显示一个缺省头像。

<a rel="attachment wp-att-867" href="http://www.pureweber.com/article/gravatar-for-users-developers/3-3/"><img class=" size-full wp-image-867" src="http://www.pureweber.com/wp-content/uploads/2011/06/31.jpg" alt="" width="326" height="446" /></a>

在这几个步骤之后，就添加好了gravatar头像，接下来进入管理界面。

<a rel="attachment wp-att-868" href="http://www.pureweber.com/article/gravatar-for-users-developers/4-3/"><img class=" size-full wp-image-868" src="http://www.pureweber.com/wp-content/uploads/2011/06/41.jpg" alt="" width="587" height="287" /></a>

在此界面下，可以对自己的多个头像和相关联的多个email进行管理。

以上是作为普通用户的gravatar使用方法，对于开发者，gravatar同样提供了一些便利的使用方式来丰富你的站点。


##开发者

gravatar不但为普通用户提供了头像解决方案，还为开发者们提供了一些接口，方便开发者调用gravatar头像以及在用户gravatar头像中包含的简单profile。在gravatar首页中可以找到开发者文档的入口，里面有关于如何使用gravatar接口的文档。

最常用的调用方式是通过URL调用头像和用户profile。通过URL调用要经过以下几个步骤Creating the Hash将欲调用的用户的email字符串去掉空格，并将所有字母转换为小写，最后将其转换为md5码，以php语言为例：

{% highlight php %}
<?php
$email = trim(“MyEmailAddress@example.com”);
$email = strtolower($email);
echo md5($email);
?>
{% endhighlight %}

接下来便可利用得到的字符串构造URL来调用gravatar中的头像了。简单调用，将得到的hash后的字符加在http://www.gravatar.com/avatar/之后，再将其写到`<img>`标签的src属性中，便可以调用了。如hash后得到的字符串为205e460b479e2e5b48aec07710c08d51，便可按以上方法调用为：

{% highlight html %}
<img src="http://www.gravatar.com/avatar/205e460b479e2e5b48aec07710c08d51" />
{% endhighlight %}

<strong>文件格式</strong>：如果需要文件的格式，也可以在后面加上后缀，如’.jpg’。在调用的时候，也可以进行一些简单的参数设置，如大小，缺省等。

<strong>图像大小</strong>：在URL后添加 ?s=(或?size=) 一个整数，便会返回一个指定大小（长宽一样）的图像。

<strong>缺省头像</strong>：当由于头像分级或未设置头像而无法显示时，可以设置一个缺省头像.设置缺省头像使用的是 ?d= 参数，既可以使用gravatar提供的几种参数，也可以链接到其他URL指向的图片，但要经过urlencode()函数的编码。如：echo urlencode( 'http://example.com/images/avatar.jpg' )这样便可将缺省头像指向一个URL。

还有一些其他的参数设置，如强制缺省，制定分级，详细内容请参考官方文档。注册gravatar时还会填写一些个人信息（邮箱，个人主页等）这些信息也可以通过gravatar URL来调用。方法也是先将email hash一下，然后加在http://www.gravatar.com/之后，注意，和调用头像不同，向这一URL发送请求，返回信息就包含着profile中的信息。

{% highlight php %}
<?php
$str = file_get_contents( 'http://www.gravatar.com/'.$email.'.php' );
$profile = unserialize( $str );
?>
{% endhighlight %}

这样就得到了全部的profile信息，profile中包含若干键值对，其中键为信息的标题（姓名，电话等），值为信息的内容。
除此之外，gravatar还有远程调用的接口，用于在用户认证的基础上，修改用户gravatar账户中的信息，由于并不常用，所以不再赘述，有兴趣可以参考官方文档。

总之，gravatar的出现对于普通用户来说，提供了一个管理头像平台，能够为用户节省精力，对于开发者来说，在自己的站点中引入gravatar也能够为自己的网站增色不少。

## 参考资料

<ul>
<li><a href="http://gravatar.com">Gravatar.com</a></li>
<li><a href="http://en.gravatar.com/site/implement/">开发者入口</a></li>
</ul>
