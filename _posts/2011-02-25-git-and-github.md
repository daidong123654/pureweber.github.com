---
layout: post
title: Git与Github的使用(ubuntu)
tags:
  - git
  - github
  - '%e5%8d%8f%e4%bd%9c'
  - '%e6%95%99%e7%a8%8b'
  - '%e7%ae%80%e4%bb%8b'

---

<h3>Git的简介</h3>
<p style="padding-left: 30px">Git是2005年Linus Torvalds 为了帮助管理 Linux(R) 内核开发而开发的一个开放源码的版本控制软件，正如所提供的文档中说的一样，"Git 是一个快速、可扩展的分布式版本控制系统，它具有极为丰富的命令集，对内部系统提供了高级操作和完全访问。"</p>

<h3>Git的安装与配置</h3>
<h4 style="padding-left: 30px">安装Git</h4>
<p style="padding-left: 60px">ubuntu 10.04源里有Git，直接用yum,apt-get安装即可。安装后直接使用即可，一些初始化的信息在下面有介绍。</p>

<h4 style="padding-left: 30px">配置ssh-key</h4>
<p style="padding-left: 60px">Github使用ssh tunnel(加密通道，不做介绍了)。因此要先产生一枚ssh-key 上传到Github上。</p>
<p style="padding-left: 60px">[coolcode]$ ssh-keygen -C 'your@email.address' -t rsa[/coolcode]</p>
<p style="padding-left: 60px">然后确认默认路径，再连续输入2次密码(直接回车则密码为空)即可。 (备注1)</p>

<h3>Github注册及Git的简单操作</h3>
<p style="padding-left: 30px"><a href="http://github.com/" target="_blank">http://github.com</a>(支持汉语),注册后帐号右上角有"Your Repositories",选择"Create One"。在"Project name"处输入名字后，它会显示出一个创建新项目的小教程。</p>
<p style="padding-left: 30px">说一下在本地的一些操作，假设你的代码文档已经存在了 ～/work文件夹中，那么:</p>

<h4 style="padding-left: 30px">Git的初始设置</h4>
<p style="padding-left: 60px">
[coolcode]
$ git config --global user.name "Your Real Name"
$ git config --global user.email  you@email.address
[/coolcode]</p>
<p style="padding-left: 60px">这些是要在以后版本信息里面出现的东西。</p>

<h4 style="padding-left: 30px">初始化Git仓库（init）</h4>
<p style="padding-left: 60px">
[coolcode]
$ cd ~/work
$ git init
# 然后会显示：
Initialized empty Git repository in $PROJECT/ .git/
[/coolcode]</p>
<p style="padding-left: 60px">表示在当前目录下闯将了一个.git的隐藏目录，这个就是所谓的Git仓库了。此时的～/work文件夹，我们也改名称之为工作树。</p>

<h4 style="padding-left: 30px">生成快照(take a snapshot)</h4>
<p style="padding-left: 60px">将工作树中的一些文档存至Git仓库中，并且变成Git仓库能够识别的数据格式。</p>
<p style="padding-left: 60px">
[coolcode]
$ cd ~/work
$ git add .
[/coolcode]</p>
<p style="padding-left: 60px">注意：add 与后面的"."是有一个空格的，这个"."表示所有的文档。如果只生成一个文档，则将"."改为文档名即可。</p>

<h4 style="padding-left: 30px">提交(commit)</h4>
<p style="padding-left: 60px">所生成的快照被存放到一个临时的存储区域, 称该区域为索引。Git的每次更新都需要提交一次。</p>
<p style="padding-left: 60px">
[coolcode]
$ git commit
# 一般来说都需要对跟新的版本进行说明，则上述命令应为
$ git commit -m "你的版本更新信息"
[/coolcode]</p>

<h3>提交密钥</h3>
<p style="padding-left: 30px">还记得刚刚生成的密钥吧，现在我们要把它放到github上了</p>
<p style="padding-left: 30px">
[coolcode]
$ cd ~/.ssh
$ ls
[/coolcode]</p>
<p style="padding-left: 30px">会显示"id_rsa     id_rsa.pub" 两个文件，前一个是私钥，.pub的是公钥。将公钥粘贴到你github帐号中的</p>
<p style="padding-left: 30px">SSH Public Keys处即可。 (备注2)</p>

<h3>文档忽略</h3>
<p style="padding-left: 30px">提供了文档忽略机制,Git可以将工作树中你不希望接受 Git 管理的文档信息写到同一目录下的 .gitignore 文件中。以文件"dust"为例：</p>
<p style="padding-left: 30px">$ cd ~/work</p>
<p style="padding-left: 30px">$ echo "dust" &gt; .gitignore</p>
<p style="padding-left: 30px">$ git add .</p>
<p style="padding-left: 30px">先叙述这么多，有更多的需要可以到git官网上去查<a href="http://git-scm.com/" target="_blank">http://git-scm.com</a></p>

<h3>PULL/PUSH</h3>
<p style="padding-left: 30px">git-pull：从远端仓库取回版本更新</p>
<p style="padding-left: 30px">git-push：可将本地版本更新推送到远端仓库中。</p>

<h3>团队开发流程</h3>
<p style="padding-left: 30px">$ git clone  用户名@IP:目标路径</p>

<h4 style="padding-left: 30px">修改文件</h4>
<p style="padding-left: 60px">$ git add 改动的文件</p>
<p style="padding-left: 60px">$ git commit</p>
<p style="padding-left: 60px">$ git pull</p>

<h4 style="padding-left: 30px">解决合并问题</h4>
<p style="padding-left: 60px">$ git push</p>
<p style="padding-left: 60px">push命令只能将代码push到你的分支上。</p>

<h4 style="padding-left: 30px">合并&amp;分支</h4>
<p style="padding-left: 60px">分支的作用有很多，并行开发多版本，并行开发新功能，测试某个独立功能点等。而这些总结起来，本</p>
<p style="padding-left: 60px">目的就是为了避免不同版本的代码之间互相影响而当这种影响已经不存在了，就需要合并了</p>

<h5 style="padding-left: 60px">1.产生新分支(名为local)：</h5>
<p style="padding-left: 90px">[coolcode]$ git branch local[/coolcode]</p>

<h5 style="padding-left: 60px">2.查看存在多少分支</h5>
<p style="padding-left: 90px">
[coolcode]
$ git branch
    local
    * master
[/coolcode]</p>

<h5 style="padding-left: 60px">3.切换到分支/主文件夹</h5>
<p style="padding-left: 90px">[coolcode]$ git checkout local[/coolcode]</p>

<h5 style="padding-left: 60px">4.分支的合并</h5>
<p style="padding-left: 90px">
[coolcode]
$ git checkout master # 将当前分支切换为master
$ git merge local # 将local分支与当前分支合并
[/coolcode]</p>

<h5 style="padding-left: 60px">5.删除分支</h5>
<p style="padding-left: 90px">[coolcode]$ git branch d local[/coolcode]</p>

<h4>备注1：</h4>
<p style="padding-left: 30px">关于ssh命令：</p>
<p style="padding-left: 30px">-keygen:产生公开钥 (pulib key) 和私人钥 (private key)。</p>
<p style="padding-left: 30px">-c:要 求压缩所有资料(包含 stdin, stdout,stderr 和 X11 和 TCP/IP 连接) 压缩演算规则与 gzip 相同</p>
<p style="padding-left: 30px">-t:强制配置 pseudo-tty。</p>

<h4>备注2：</h4>
<p style="padding-left: 30px">注意：复制的时候要一点不差的拿过去，一个符号一个空格都可能会导致密钥不能使用，其中</p>
<p style="padding-left: 30px">Permission denied (publickey).</p>
<p style="padding-left: 30px">fatal: The remote end hung up unexpectedly</p>
<p style="padding-left: 30px">这个问题就是因为不能识别密钥而没有权限导致的。</p>

<h4>链接：</h4>
<p style="padding-left: 30px">1. 一个很直观的git命令表：</p>
<p style="padding-left: 30px"><a href="http://www.cnblogs.com/1-2-3/archive/2010/07/18/git-commands.html" target="_blank">http://www.cnblogs.com/1-2-3/archive/2010/07/18/git-commands.html</a></p>
