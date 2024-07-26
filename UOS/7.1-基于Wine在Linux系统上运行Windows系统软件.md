# 基于Wine在Linux系统上运行Windows系统软件

## 起因：
　　在知网上下载了一些硕士论文，都是caj格式的文件，需要安装CAJViewer软件进行浏览。而自己的工控机使用的系统为Ubuntu18.04，CAJVewer软件并没有linux版本。

## 一、Wine简介
　　Wine是一个在x86、x86-64上容许类Unix操作系统在Window System下运行Microsoft Windows程序的软件。虽然Wine有另一个非官方名称，"Windows Emulator"，即Windows模拟器，但Wine其实为"Wine Is Not anEmulator"的递归缩写，即Wine不是模拟器。Wine的正确名称是"Wine"，不是全大写或全小写。Wine不是Windows模拟器，而是运用API转换技术实做出Linux对应到Windows相对应的函数来调用DLL以运行Windows程序。Wine是自由软件，在GNU宽通用公共许可证（LGPL） 下发布。

　　Wine支持数量众多的应用程序，但并非全部都得到同样的支持。可以访问Wine应用数据库，看看你常用的Windows应用程序与Wine之间的兼容性有多好。AppDB由社区维护;你也可以添加自己发现的应用程序。AppDB定义了如下几种级别类型：

- 白金：如果某应用程序在“即开即用”状态下可以顺畅无阻地安装和运行，它可以被评为白金级。Wine配置文件不需要进行更改。

- 黄金：应用程序与一些DLL覆盖文件、其他设置或第三方软件可以顺畅无阻地协同运行。

- 白银：就“平常”使用而言，应用程序可以出色地运行。比如说，游戏在单人玩家模式下运行很好，但在多人玩家模式下不行;Windows Media Player作为插件和独立播放器运行很好，但无法处理数字版权管理(DRM)等。

- 青铜：应用程序可以运行，但存在一些问题，哪怕是平常使用。比如说，游戏无法正确地重新绘图或者用错误的颜色显示字体，速度比平常慢得多，等等。

- 垃圾：如果应用程序无法用于原本的用途，就会得到这个评级。如果这样，通用软件缺陷跟踪系统Bugzilla中应该至少有一个软件缺陷报告。应用程序无法安装、无法启动，或者就算能启动，也有好多错误，以至于几乎没法使用。

## 二、Wine安装

在Ubuntu18.04上安装Wine，打开终端输入如下指令即可完成安装。

```bash
shell>sudo apt install wine-stable

```

**非常不像Linux的文件夹路径：**

Linux不像Windows那样含有C驱动器。但在~/.wine文件夹下会有一个名为drive_c的文件夹。该文件夹里面有三个熟悉的子文件夹：

- Program Files

- users

- windows

接下来安装的软件就会存放在这文件夹下。

## 三、安装CAJViewer

官网下载CAJViewer，在保存的CAJViewer.exe文件的文件夹下启动终端输入指令，全部安装Ｃ盘。

```bash
shell> wine CAJViewer\ 7.2.0.115.self.exe 

```

成功



**参考链接：**

https://www.cnblogs.com/mo-wang/p/5183286.html

https://blog.csdn.net/u014597198/article/details/79611409