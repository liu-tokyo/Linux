# Ubuntu 20.04 上安装 Gradle

> Gradle 是一个多用途工具，它主要被用来构建，自动化操作，以及发布软件。它主要被用于 Java，C++，和 Swift 工程。
>
> Gradle 是一个强大并且灵活的构建工具，主要用于 Java 项目，综合了 Ant 和 Maven 的优点。不像其他的预处理工具使用 XML，Gradle 使用 Groovy，一个动态的，面向对象的 Java 平台语言，用来定义项目和构建脚本。
>
> 本文解释了如何在 Ubuntu 20.04 上如何安装 Gradle。我们将会从它们的官方网站下载最新版本的 Gradle。

## 前提条件

- 下面的操作说明假定你以 root 或者其他拥有 sudo 权限的用户身份登录了系统。

- 已经安装了 Java SE 8 或者更新的版本。

  请参照 [A0-安装Java并配置环境变量.md](A0-安装Java并配置环境变量.md)

  或者通过如下指令安装：

  ```bash
  sudo apt update
  sudo apt install openjdk-11-jdk
  ```

  通过打印 Java 版本号来验证 Java 安装：

  ```bash
  java -version
  ```

  

## 1. 软件下载安装

Gradle 最新的版本是 `7.6`。在继续下一步之前，你应该检查 [Gradle 发布页面](https://gradle.org/releases/)，看看有没有更新的版本可用。  
因为工作中，一直使用 `6.5.1`，所以还是下载安装该版本。

- 使用 `wget`命令下载 Gradle 二进制文件到`/tmp`文件夹下：

  ```bash
  VERSION=6.5.1
  wget https://services.gradle.org/distributions/gradle-${VERSION}-bin.zip -P /tmp
  ```

- 下载完成后，解压文件到`/opt/gradle` 文件夹：

  ```
  sudo unzip -d /opt/gradle /tmp/gradle-${VERSION}-bin.zip
  ```

  如果你得到一个错误提示说`sudo: unzip: command not found`,使用`sudo apt install unzip`安装 unzip 软件包。

- 版本更新控制：

  Gradle 会定义更新，比如安全补丁和新功能。想要对版本和更新有更好的控制，我们将会创建符号连接命名为`latest`，它指向 Gradle 安装目录：

  ```bash
  sudo ln -s /opt/gradle/gradle-${VERSION} /opt/gradle/latest
  ```

  稍后，当升级 Gradle 时，解压新版本，并且修改符号链接指向它。



## 2. 设置环境变量

将 Gradle bin 目录添加到系统`PATH`环境变量中。并且在`/etc/profile.d`目录下创建一个名称为`gradle.sh`的文件：

- 设置环境变量：

  ```bash
  sudo nano /etc/profile.d/gradle.sh
  ```

  粘贴下面代码：

  ```bash
  export GRADLE_HOME=/opt/gradle/latest
  export PATH=${GRADLE_HOME}/bin:${PATH}
  ```

  保存并且关闭文件。这个脚本将会在下次 shell 启动时生效。

- 修改脚本权限：

  ```bash
  sudo chmod +x /etc/profile.d/gradle.sh
  ```

- 加载环境变量：

  ```bash
  source /etc/profile.d/gradle.sh
  ```

  

## 3. 验证安装结果

- 显示安装版本：

  ```bash
  gradle -v
  ```

  你可以看到类似下面的信息：

  ```
  Welcome to Gradle 6.5.1!
  
  Here are the highlights of this release:
   - Experimental file-system watching
   - Improved version ordering
   - New samples
  
  For more details see https://docs.gradle.org/6.5.1/release-notes.html
  
  
  ------------------------------------------------------------
  Gradle 6.5.1
  ------------------------------------------------------------
  
  Build time:   2020-06-30 06:32:47 UTC
  Revision:     66bc713f7169626a7f0134bf452abde51550ea0a
  
  Kotlin:       1.3.72
  Groovy:       2.5.11
  Ant:          Apache Ant(TM) version 1.10.7 compiled on September 1 2019
  JVM:          11.0.7 (Ubuntu 11.0.7+10-post-Ubuntu-3ubuntu1)
  OS:           Linux 5.4.0-26-generic amd64
  ```

  

## 安装总结

如上，已经在 Ubuntu 系统上安装了最新的 Gradle，你可以开始使用它了。你现在可以浏览 [Gradle 官方文档页面](https://docs.gradle.org/current/userguide/userguide.html) 并且学习 Gradle 快速入门。