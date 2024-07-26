# Ubuntu 20.04上安装Eclipse IDE

> [Eclipse](https://www.eclipse.org/)是使用最广泛的[Java](https://www.myfreax.com/install-java-on-ubuntu-18-04/)集成开发环境（IDE）。它可以通过插件扩展，也可以用于其他编程语言的开发，例如C ++，JavaScript和[ PHP ](https://www.myfreax.com/how-to-install-php-on-ubuntu-18-04/)。  
> Ubuntu存储库中可用的Eclipse安装包（版本3.8.1）已过时。最简单的方法是使用[ snappy ](https://snapcraft.io/)打包系统在Ubuntu 18.04上安装最新的Eclipse IDE。  
> 在本教程中，我们将向您展示如何在Ubuntu 18.04计算机上安装最新的Eclipse IDE。



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



## 1. 安装 Eclipse

- 在系统上下载并安装Eclipse snap软件包，指令如下：

  ```bash
  sudo snap install --classic eclipse
  ```

  成功安装Eclipse时，您应该看到以下输出：

  ```
  eclipse 2019-03 from Snapcrafters installed
  ```

## 2. 启动 Eclipse

您可以通过单击Eclipse图标（`Activities -> Eclipse`）启动它：

首次启动Eclipse时，将出现如下所示的窗口，要求您选择工作区目录：

默认目录应该可以。点击`Launch`继续：



## 安装总结

您已经了解了如何在Ubuntu 18.04计算机上安装Eclipse。您现在可以开始处理Java项目。

要查找有关如何开始使用Eclipse的更多信息，请访问 [Eclipse文档](https://www.eclipse.org/getting_started/) 页面。
