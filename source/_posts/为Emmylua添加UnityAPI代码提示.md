---
title: 为Emmylua添加UnityAPI代码提示
date: 2019-11-07 10:11:28
tags: [unity,Emmylua]
---
&emsp;最近从之前的cocos creator前端开始转做unity前端，刚刚接触公司的项目。在环境搭建中遇到一些问题在此记录一下  

&emsp;我接到的项目不算复杂，Lua开发使用了IDEA系列编辑器(之前些golang的时候也用的他们家的GoLand)，插件使用了Emmylua。关于Emmylua的使用心得随后我会再写一篇文章来记录，暂时理解不太深不适合此时来介绍。家常唠完了，进正题叭。  

&emsp;关于EmmyLua插件的安装我就不在赘述了，毕竟IDEA家的插件安装直接搜索and安装就ok了。这里主要说一下UnityAPI的代码提示问题。毕竟对于我这样的新手玩家来说，像lua这种脚本语言没有强类型的情况下想通过"."来查看类型有哪些方法是很难受的，而且也不利于学习的过程。所以我就去网上找添加UnityAPI提示的方法，然而找到了如下的添加方法:  
![image](http://jiemogancuimian.com/pictures/blogs/2019-11-07/01.png)  
[截图博客源地址]("https://www.cnblogs.com/sanyejun/p/9673198.html")  

&emsp;然而我发现现在的编辑器里并没有**Lua Net Library**这个选项  
![image](http://jiemogancuimian.com/pictures/blogs/2019-11-07/02.png)

&emsp;后来我从EmmyLua的[github项目](https://github.com/EmmyLua)上顺藤摸瓜加到官方群里，在群里找到了答案  

&emsp;首先需要为IDEA编辑器添加EmmyLua-Unity插件，这个插件在官方的插件库里是没有，要去群里或者[这个地址](https://ci.appveyor.com/project/EmmyLua/emmylua-unity/build/artifacts)去下载，然后通过本地安装插件的方法安装到编辑器(直接选中zip包就行，不用解压操作)：  
![image](http://jiemogancuimian.com/pictures/blogs/2019-11-07/03.png)  

&emsp;安装完之后点*ok*会提示你重启编辑器，重启即可，然后再去添加的时候就会看到有**Lua Net Library**这个选项了  
![image](http://jiemogancuimian.com/pictures/blogs/2019-11-07/04.png)  

&emsp;但是在群里发现这种添加dll的方法被标记了一个过时，并提供了一种新的添加UnityAPI提示的方法:  
&emsp;在安装了上面的IDEA插件后，将一个[EmmyLuaService.cs](https://github.com/EmmyLua/EmmyLua-Unity/blob/master/Unity/Assets/Editor/EmmyLuaService.cs")的文件([提取码: wgi9](https://pan.baidu.com/s/16d9hhkwUi67BB4naJHuxKQ"))放到Unity项目的**Assets/Editor**文件夹下，如果没有的话可以自己创建一个Editor文件夹，之后Unity编辑器菜单栏上会多出一个EmmyLua的菜单项，选中Enable  

![image](http://jiemogancuimian.com/pictures/blogs/2019-11-07/04.png)  

&emsp;然后就会发现在IDEA编辑器中已经有UnityAPI的代码提示了。由于这种方法相当于是在Unity编辑器中启动了一个server，所以需要在Unity编辑器打开的情况下才能有提示，不过考虑到正常开发中Unity编辑器是常驻打开的也没什么问题。

&emsp;其实群内还有很多工具和小技巧，而且还能跟大家交流学习，如果有需要不妨也加入官方群，方便更好的学习
