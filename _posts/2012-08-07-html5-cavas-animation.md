---
layout: post
title: HTML5-Canvas动画原理
tags:
  - canvas
  - html5
  - javascript
  - '%e5%88%86%e4%ba%ab%e4%bc%9a'
  - '%e5%8a%a8%e7%94%bb'

---

大二下学期，学校里开设了《软件设计与开发实践I》课程，要求利用所学《数据结构》的知识，独自开发一个应用。我做的是<a href="http://jade.freepanda.me/" target="_blank">数据结构的交互式动画</a>，在开发过程中，我用JavaScript创建了一个简单的HTML5-Canvas动画库。

下面我将利用“矩形”作为一个特例来讲解:
<ul>
	<li>JavaScript实现canvas动画的基本原理</li>
	<li>如何创建一个简单的动画控制器</li>
</ul>
此外，我还写了一个此文的<a href="http://jade.freepanda.me/bootstrap/" target="_blank">国际版本</a>，较本文，其代码和样例比较多，且为英文撰写。
<h3>一、在canvas上绘制一个矩形</h3>
首先，通过var ctx = document.getElementById("canvas").getContext("2d")获取canvas的2d上下文对象，可以把ctx看做是一只神奇的画笔，如果你想绘制一个实体矩形，那么调用它的fillRect(x,y,width,height)方法，如果你想绘制一条直线，可以调用lineTo(x, y)......

<coolcode lang="javascript">
var context = document.getElementById("canvas").getContext("2d");

//Set location coordinates
var x = 100;
var y = 50;

//Set size
var width = 50;
var height = 80;

//Set colors
var backColor = "Red";
var edgeColor = "Black";

//Set backColor as pen color
ctx.fillStyle = backColor;
//Draws a filled rectangle
ctx.fillRect(x,y,width,height);
//Set edgeColor as pen color
ctx.strokeStyle = edgeColor;
//Draws a rectangular outline
ctx.strokeRect(x,y,width,height); 
</coolcode>

<h3>二、构建矩形类</h3>
在一个动画中，矩形肯定不止有一个。如果想绘制多个矩形，而且它们各自有不同的样式，那么最好的方法就是：将矩形抽象为一个类。

<coolcode lang="javascript">
Rectangle = function(cfg)  //cfg is a object of customize parameters
{
    //Set default parameters
    this.width = 50;   
    this.height = 80;       
    this.x = 100;    
    this.y = 50;
    this.backColor = "Red";  
    this.edgeColor = "Black"; 

    //Set customize parameters
    this.setArguments(cfg);  
}
//Set customize parameters
Rectangle.prototype.setArguments = function(cfg) 
{
    for(var x in cfg)
        this[x] = cfg[x];
}
Rectangle.prototype.draw = function() //Draw method
{
    //Set backColor as pen color 
    ctx.fillStyle = this.backColor;
    //Draws a filled rectangle
    ctx.fillRect(this.x,this.y,this.width,this.height);
    //Set edgeColor as pen color
    ctx.strokeStyle = this.edgeColor;
    //Draws a rectangular outline
    ctx.strokeRect(this.x,this.y,this.width,this.height);
}
</coolcode>
<h3>三、移动一个矩形</h3>

很可惜ctx只能绘制静态的图形。所以需要我们自己编码实现动画效果。先看看下面这两幅图片：

<img class="alignnone size-medium" src="http://www.pureweber.com/wp-content/uploads/2012/09/static-picture.jpg" alt="" width="450" />

<img class="alignnone size-medium" src="http://www.pureweber.com/wp-content/uploads/2012/09/dynamic-picture.gif" alt="" width="450" />

第二张动态的图片是由4张静态图片组成的，由于人眼的视觉残留效应．所以当多张静态的图片快速切换时，我们便看到了动画。将此原理代码化，来实现矩形的移动动画。

<coolcode lang="javascript">
function move()
{
    moveShape.animationStatus["Move"] = "new";
    timer = setInterval(function()   //Run once every 24ms
    {   
        if(moveShape.animationStatus["Move"] == "new")
        {                   
            ctx.clearRect(0,0,600,400);  //Clear the canvas
            moveShape.nextPosition();   //Set new (x,y) 
            moveShape.draw();   //Draw the rectangle
        }
        else
            clearInterval(timer);  //Stop setInterval() when it arrives
    }, 24);
}
</coolcode>

<h3>四、丢失的红色矩形</h3>
根据之前的三步内容，我编写了一个Demo：
[iframe src="/works/demos/canvas/4.html" frameborder="0" width="100%" scrolling="no" height="466px"][/iframe]
在黄色矩形移动时，红色矩形不见了，问题出在哪呢？回到之前第三步代码的第10行moveShape.draw()，由于重绘canvas时，只调用了黄色矩形的draw()，红色矩形自然就消失了。正确的做法是：在第10行后增加一行代码调用红色矩形的draw()，但是这并不是最好的解决方法。如果canvas上有100个矩形呢？难道要增加100行？比较好的方法是：将画板上的所有图形保存到一个ShapeOnCanvas数组里，把第10行代码替换成：

<coolcode lang="javascript">
for(var i=0;i<ShapeOnCanvas.length;i++)  
    ShapeOnCanvas[i].draw();  //Draw all shapes that on canvas
</coolcode>

<h3>五、构建动画控制器</h3>
通常的情况是，在同一时刻，有些图形在移动、有些图形在淡入、有些图形在旋转......人都是懒惰的，所以我的目标是一行代码就能实现这些功能，当然这行代码肯定是一个函数调用的接口。

函数调用接口：<code>cmd ({ a1,b1,c1, a2,b2,c2, a3,b3,c3, ... });</code>

<ul>
	<li>a* is a string such as "Move","Draw"</li>
	<li>b* is an object of shape</li>
	<li>c* is an object of animation parameters such as {aim_x:10,aim_y:10,moveSpeed:2}</li>
</ul>

<coolcode lang="javascript">
cmd = function()
{
    command = arguments;  //"command" is a long array that save animation commands
    //"command[i]" is a string such as "Move","Draw"
    //"command[i+1]" is an object of shape
    //"command[i+2]" is an object of animation parameters such as {aim_x:10,aim_y:10,moveSpeed:2} 

    //Do the preparation before start animation(refresh canvas)
    for(var i=0; i<command.length; i+=3)  
    {
        //init all animation status as "new"
        command[i+1].animationStatus[command[i]] = "new";  
        //Set animation parameters
        command[i+1].setArguments(command[i+2]);
        //Push it into the stack
        ShapeOnCanvas.push(command[i+1]);  
    }

    timer = setInterval(function()   //Run once every 24ms
    {
        var j = 0;
        var allStop = true;  //"allStop" is the flag of all animations have been stopped
        for(var j=0; j<command.length; j+=3)
            if(command[j+1].animationStatus[command[j]] == "new")
            {
                switch(command[j])
                {
                    case "Draw":
                        command[j+1].draw();
                        break;
                    case "Move":
                        command[j+1].nextPosition();
                        break;
                }   
                allStop = false;
            }

            //Clear the canvas
            ctx.clearRect(0,0,600,400);

            for(var i=0;i<ShapeOnCanvas.length;i++){
                //Draw all shapes that on canvas
                ShapeOnCanvas[i].draw();
            }
            if(allStop){
                //Stop setInterval() when all animations stop
                clearInterval(timer);
            }
    }, 24);
}
</coolcode>

如果你想扩充其他动画效果，例如添加“旋转”，只需要在switch添加：

<coolcode lang="javascript">
case "Rotate"：
    command[j+1].rotate(); //rotate()应该是根据旋转参数设置图形新的坐标位置
    break;
</coolcode>

<h3>六、串行动画</h3>
上一步的动画控制器只能处理并行的动画，现在我们把它扩展一下，实现串行动画。
其最终效果是：如下代码能实现Demo中的动画效果。

<coolcode lang="javascript">
cmd("Setup");
cmd
(
    "Draw",staticShape,{},
    "Move",moveShape,{aim_x:400,aim_y:300,moveSpeed:3},
    "Move",fastMoveShape,{aim_x:100,aim_y:300,moveSpeed:6}
);
cmd("Move",staticShape,{aim_x:300,aim_y:100,moveSpeed:5});
cmd("End");
</coolcode>

[iframe src="/works/demos/canvas/6.html" frameborder="0" width="100%" scrolling="no" height="466px"][/iframe]

解决方案：创建一个cmdQueue队列，按照调用cmd()的顺序，将传入cmd()的参数(一条并行动画命令)入队，启动一个setInterval()，每隔10ms检测一下之前一条并行动画命令是否执行结束，如果结束，则从队列出队下一条动画命令去执行。

<coolcode lang="javascript">
cmd = function()
{
    if(arguments[0] == "Setup")  //setup animation
    {
        //"cmdQueue" is a queue to save animation commands
        this.cmdQueue = new Array();
        //init the rear and front of the cmdQueue                   
        this.rear = 0;
        this.front = 0;
        cmdRun = false;

        var me = this;

        //run once every 10ms
        cmdTimer = setInterval(function()  
        {
            //All previous animation commands have been stopped 
            //and there are remaining animation commands
            if(me.cmdRun == false && me.front < me.rear) 
            {
                if(me.cmdQueue[me.front][0] == "End")
                    clearInterval(cmdTimer);  //Stop cmdTimer
                else
                {
                    //Run one animation command
                    refresh(me.cmdQueue[me.front]);
                    me.front++;
                }
            }
        }, 10);
    }
    else{
        //Enqueue animation commands to cmdQueue
        this.cmdQueue[this.rear++] = arguments;
    }
}

refresh = function(command)
{
    cmdRun = true;                  

    //Do the preparation before start animation(refresh canvas)
    for(var i=0; i<command.length; i+=3)  
    {
        //init all animation status as "new"
        command[i+1].animationStatus[command[i]] = "new";
        //Set animation parameters
        command[i+1].setArguments(command[i+2]);
        //Push it into the stack
        ShapeOnCanvas.push(command[i+1]);
    }

    timer = setInterval(function()   //Run once every 24ms
    {
        var j = 0;

        //"allStop" is the flag of all animations have been stopped
        var allStop = true;
        for(var j=0; j<command.length; j+=3)
        if(command[j+1].animationStatus[command[j]] == "new")
        {
            switch(command[j])
            {
                case "Draw":
                    command[j+1].draw();
                    break;
                case "Move":
                    command[j+1].nextPosition();
                    break;
            }   
            allStop = false;
        }
        //Clear the canvas
        ctx.clearRect(0,0,600,400);
        for(var i=0;i<ShapeOnCanvas.length;i++){
            //Draw all shapes that on canvas
            ShapeOnCanvas[i].draw();
        }
        if(allStop)
        {
            cmdRun = false;
            //Stop setInterval() when all animations stop
            clearInterval(timer);  
        }
    }, 24);
}
</coolcode>
