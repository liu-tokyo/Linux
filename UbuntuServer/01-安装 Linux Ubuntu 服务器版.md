# 安装 Linux Ubuntu 服务器版

在安装Linux Ubuntu的过程中，以主体内容中英文翻译对照，方便各位小伙伴在一边安装的时候一边可以更好的学习理解。

操作说明：↑ ↓ ← →方向键进行选项选择，Spacebar (Windows)、Space (macOS) 空格键确认所选选项，Enter（Windows）、return（macOS）回车键确认并进入下一步。

### 开始安装

- 启动光盘镜像后，我们点击【*Try or Install Ubuntu Server】开始安装

  ![img](https://pic1.zhimg.com/80/v2-a6cf839ab09da9259bef1d9d0e9f228c_720w.webp)

### 加载镜像

加载镜像中的部分界面

- 加载镜像a

  ![img](https://pic2.zhimg.com/80/v2-43d3e5e30a8589afc2c14f3953cc5671_720w.webp)
  
- 加载镜像b

  ![img](https://pic1.zhimg.com/80/v2-86ddbe03d572159faca1031d7bc05284_720w.webp)

### 选择系统语言

- 可根据自己的习惯选择，默认选择【English】

  ![img](https://pic2.zhimg.com/80/v2-5d929625ac69ae52ddcaf1e15a183895_720w.webp)

  注意：选择其它语言很容易导致安装失败。

### 确认更新

- 由于官方有发布新版本，所以会提示我们是否需要更新到新版本，这里我们选择【Continue without updating】（不更新）

  ![img](https://pic1.zhimg.com/80/v2-baf24cea27e9fead85e3e5b823732b68_720w.webp)

### 配置键盘

- 一般选择默认，我们都是用的英文键盘，按【Done】继续

  ![img](https://pic2.zhimg.com/80/v2-f50eaefe637a9114d09efcf136d745c5_720w.webp)

### 安装类型

- 新手选择第一项【Choose type of install】即可，按【Done】

  ![img](https://pic1.zhimg.com/80/v2-0243d676f25b81b9a9fd4a8b104b1228_720w.webp)



### 配置网络

- 无特殊需求的话，一般选用DHCP自动分配ip，按【Done】继续

  ![img](https://pic1.zhimg.com/80/v2-555670930beac93e9ca0db118bb7710c_720w.webp)

### 配置代理

- 默认即可，按【Done】继续

  ![img](https://pic4.zhimg.com/80/v2-343240bc5d4ffe4b6002b38c02f712f3_720w.webp)

### 配置下载镜像

- 配置Ubuntu的下载镜像（一般更新时候用到的），默认即可，按【Done】继续

  ![img](https://pic2.zhimg.com/80/v2-443cd18683b245b16c05c7ace5faf761_720w.webp)

### 配置存储磁盘

- 根据图示进行配置即可

  ![img](https://pic4.zhimg.com/80/v2-25630e5403ed062e15de2709b98d060b_720w.webp)

### 磁盘信息确认

- ①（推荐新手），配置完成进入下一步的默认情况，可直接按【Done】继续

  ![img](https://pic4.zhimg.com/80/v2-aa9969ffff5199605c6f92c61c77f27b_720w.webp)

- ②（推荐有一定基础），修改挂在容量后，按【Done】继续

  ![img](https://pic4.zhimg.com/80/v2-47eacb3d558b45ea0c80d1b9ed16ef6f_720w.webp)

- 二次确认，确认是否继续安装，点击【Continue】继续

  ![img](https://pic2.zhimg.com/80/v2-d595d5b65f8333ab7963043c9d36cf35_720w.webp)

### 配置服务器及用户信息

- 配置服务器及用户信息，按【Done】继续

  ![img](https://pic2.zhimg.com/80/v2-959c5dacb5cb60f34b810d9703d8c9dd_720w.webp)

### 配置安装远程访问

- 有助于之后在真机和虚拟机之间复制代码，更方便操作，按图示【3-16】操作即可，按【Done】继续

  ![img](https://pic1.zhimg.com/80/v2-16abb42c1edda9c3a698acb37e7cba8c_720w.webp)

### 配置第三方软件源

- 什么都不选择，按【Done】继续

  ![img](https://pic3.zhimg.com/80/v2-f9205eb7815ccf76e0ea97866c387dc2_720w.webp)

### 安装完成

- 由于安装的是server版本，安装速度非常块，之后选择【Cancel update and reboot】取消更新并重新启动

  ![img](https://pic3.zhimg.com/80/v2-661d64d33e7b1b4c56012bb91be2f22a_720w.webp)

- 正在取消更新并重启，这里需要等待一段时间，之后会自动重启

  ![img](https://pic1.zhimg.com/80/v2-48a15ae0b0396b223e7b8f007cacd058_720w.webp)

- 正在重启中，重启的时候若是出现了[ FAILED ]（失败），别担心，这是我们之前加载的镜像没关闭导致的，可按Enter（Windows）、return（macOS）【回车键】继续，不影响，关闭虚拟机后把安装镜像关闭或者开机不加载光盘即可。

  ![img](https://pic1.zhimg.com/80/v2-a4bae5a2b5c11c3d48b16e8da976de4c_720w.webp)

- 正在重启

  ![img](https://pic4.zhimg.com/80/v2-66806827baf38ac4112162265505bd7f_720w.webp)

### 进入系统

- 可按Enter（Windows）、return（macOS）【回车键】继续

  ![img](https://pic2.zhimg.com/80/v2-c9dda78c047359372c234d8b55945065_720w.webp)

### 系统登录

- 登录用户名和密码，输入我们设置的用户名密码

  （注：输入密码的时候，界面不会有任何显示，这是正常现象，输入完密码之后按回车，密码输入正确会直接进入系统，反之，重新输入）

  ![img](https://pic3.zhimg.com/80/v2-dfd5fa73974be42c65b9006988128c5e_720w.webp)

- 登录成功

  ![img](https://pic3.zhimg.com/80/v2-c3c40545817130db0dadcf25acfc0b16_720w.webp)

server版本后续的操作都是这种黑底灰字界面，新手可能有些不适，不过既然选择了Linux，想必也是计算机专业人士，或者是正在往这条路上走中，习惯就好了。老江湖们都深有感慨，字符界面比图形界面方便太多，哈哈。最后，恭喜各位小伙伴们成功安装好了Linux Ubuntu server操作系统。