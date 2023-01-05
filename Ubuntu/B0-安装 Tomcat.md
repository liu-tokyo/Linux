# Ubuntu：安装Tomcat

> 安装过程中，尽量用 指令 方式展现，因为在很多情况下，尤其是云端，是没有界面可以操作的。

## 1. 软件下载安装

Tomcat二进制发行可从[Tomcat下载页面](https://tomcat.apache.org/download-90.cgi)下载。在撰写本文时，最新的Tomcat版本是`9.0.70`。

- 设置运行权限：

  ```bash
  ## 以root运行Tomcat，具有安全风险。我们将创建普通用户运行Tomcat，配并将Tomcat用户的家目录设置为/opt/tomcat。
  sudo useradd -m -U -d /opt/tomcat -s /bin/false tomcat
  ## 设置用户口令
  ##sudo passwd tomcat
  ```

  

- 下载指令如下：

  ```bash
  VERSION=9.0.70
  wget https://dlcdn.apache.org/tomcat/tomcat-9/v${VERSION}/bin/apache-tomcat-${VERSION}.tar.gz -P /tmp
  sudo tar -xf /tmp/apache-tomcat-${VERSION}.tar.gz -C /opt/tomcat/
  ```

- 修改目录权限：

  ```bash
  ## Tomcat会定期进行更新。为了更好地控制版本和更新，我们将创建一个名为latest的符号链接，该链接指向Tomcat的安装目录。
  sudo ln -s /opt/tomcat/apache-tomcat-${VERSION} /opt/tomcat/latest
  
  ## 运行chmod命令使bin目录中的shell脚本具有可执行权限，这些脚本用于启动和停止Tomcat。
  sudo sh -c 'chmod +x /opt/tomcat/latest/bin/*.sh'
  
  ## 将/opt/tomcat目录的所有权更改为tomcat用户和tomcat组，使tomcat用户可以访问 /opt/tomcat目录。
  sudo chown -R tomcat: /opt/tomcat
  ```

## 2. 创建服务单元

我们将其设置为 `Systemd` 服务运行，而不是手动启动和停止 Tomcat 服务器。

### 2.1 创建服务文件

- 创建服务文件：

  ```bash
  sudo nano /etc/systemd/system/tomcat.service
  ```

  文件内容如下：

  ```ini
  [Unit]
  Description=Tomcat 9 servlet container
  After=network.target
  
  [Service]
  Type=forking
  
  User=tomcat
  Group=tomcat
  
  Environment="JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64"
  Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom -Djava.awt.headless=true"
  
  Environment="CATALINA_BASE=/opt/tomcat/latest"
  Environment="CATALINA_HOME=/opt/tomcat/latest"
  Environment="CATALINA_PID=/opt/tomcat/latest/temp/tomcat.pid"
  Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
  
  ExecStart=/opt/tomcat/latest/bin/startup.sh
  ExecStop=/opt/tomcat/latest/bin/shutdown.sh
  
  [Install]
  WantedBy=multi-user.target
  ```

  输入结束后，保存并且关闭文件

  ※ 如果你的 Java 安装路径不一样，请修改 `JAVA_HOME` 环境变量。可以用如下指令查询 JAVA 的安装位置：

  ```bash
  sudo update-alternatives --config java
  ```

  

### 2.2 服务控制指令

- 服务启动指令：

  ```bash
  ## 重新导入服务（通知 systemd 一个新的单元文件存在）
  sudo systemctl daemon-reload
  
  ## 允许随机启动
  sudo systemctl enable --now tomcat
  
  ## 重新启动服务
  sudo systemctl restart tomcat
  
  ## 检查服务状态
  sudo systemctl status tomcat
  ```

  输出应该显示 Tomcat 服务器已经启用，并且运行了：

  ```
  ● tomcat.service - Tomcat 9 servlet container
       Loaded: loaded (/etc/systemd/system/tomcat.service; enabled; vendor preset: enabled)
       Active: active (running) since Mon 2020-05-25 17:58:37 UTC; 4s ago
      Process: 5342 ExecStart=/opt/tomcat/latest/bin/startup.sh (code=exited, status=0/SUCCESS)
     Main PID: 5362 (java)
  ...
  ```

  你可以 像其他 systemd 服务一样 启动，停止和重启 Tomcat：

  ```bash
  sudo systemctl start tomcat
  sudo systemctl stop tomcat
  sudo systemctl restart tomcat
  ```

  

## 3. 配置防火墙

如果你的服务器被[防火墙](https://www.myfreax.com/how-to-setup-a-firewall-with-ufw-on-ubuntu-18-04/)保护，并且你想从外面访问你的 Tomcat，你需要打开 `8080` 端口。

- 网络服务端口：

  ```bash
  sudo ufw allow 8080/tcp
  ```

  通常，当在生产环境运行 `Tomcat` 时，你应该是使用一个负载均衡，或者[反向代理](https://www.myfreax.com/nginx-reverse-proxy/)服务器。这是仅仅允许从你的本地网络访问 `8080` 端口的最佳实践。

- 反向代理端口：

  如果已经配置Nginx的反向代理，请运行最后两个 `ufw` 命令打开端口 80 和 443 ：

  ```bash
  sudo ufw allow 443/tcp
  sudo ufw allow 80/tcp
  ```

  

至此，您应该能够使用Web浏览器访问Tomcat。浏览器输入如下地址，就可以确认服务已经启动。

- 确认服务状态：

  ```
  http://localhost:8080/
  ```

  通过 `ip a` 查看设备 IP，在相同网络内，用查询到的 IP 替换 localhost，也同样可以确认服务启动状态。



## 4. 配置网页管理

因为我们还没有创建一个合适用户，因此不能访问网页管理界面。  
Tomcat 用户和角色被定义在 `tomcat-users.xml`。这个文件是一个带有注释和示例的模板，展示如何创建一个用户和角色。

### 4.1 创建管理用户

- 创建管理用户

  ```bash
  sudo nano /opt/tomcat/latest/conf/tomcat-users.xml
  ```

  输入如下内容：

  ```xml
  <tomcat-users>
  <!--
      Comments
  -->
     <role rolename="admin-gui"/>
     <role rolename="manager-gui"/>
     <user username="admin" password="admin_password" roles="admin-gui,manager-gui"/>
  </tomcat-users>
  ```

  确保你将用户名和密码修改得更加安全。

### 4.2 允许远程访问

默认情况下，Tomcat 网页管理界面被配置仅仅从 localhost 访问 Manager 和 Host Manager 应用。想要从远程 IP 访问网页界面，你需要移除这些限制。  
注意：*这可能会有一些安全隐患，我们不推荐在生产系统中这么做*。

想要从任何地方都能访问网页界面，打开配置的两个文件，注释或者移除注释的部分。

- 文件修改指令：

  对于 **Manager**：

  ```bash
  sudo nano /opt/tomcat/latest/webapps/manager/META-INF/context.xml
  ```

  对于 **Host Manager**：

  ```
  sudo nano /opt/tomcat/latest/webapps/host-manager/META-INF/context.xml
  ```

- 文件修改说明：

  想要从任何地方都能访问网页界面，打开配置的两个文件，注释或者移除注释的部分。

  ```xml
  <Context antiResourceLocking="false" privileged="true" >
  <!--
  	<Valve className="org.apache.catalina.valves.RemoteAddrValve"
  		allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
  -->
  </Context>
  ```

  如果您只想从指定IP访问Tomcat Web，则无需注释这些xml片段，而是将您的外网IP添加到列表中。  
  允许的IP地址列表是用竖线`|`分隔的列表。您可以添加单个IP地址或使用正则表达式。

  假设您的公开IP为`41.41.41.41`，而您只想仅从IP访问Tomcat Web。

  ```xml
  <Context antiResourceLocking="false" privileged="true" >
  	<Valve className="org.apache.catalina.valves.RemoteAddrValve"
  		allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1|41.41.41.41" />
  </Context>
  ```

  完成后，重新启动Tomcat服务以使更改生效。

  ```bash
  sudo systemctl restart tomcat
  ```

  

## 5. 测试安装结果

### 5.1 普通网络页面

- 网址如下：

  ```
  http://<your_domain_or_IP_address>:8080
  ```

  假设安装成功，网络页面会正常显示，并且有具体的 Tomcat 版本信息。

### 5.2 应用管理网页

- 网址如下：

  ```
  http://<your_domain_or_IP_address>:8080/manager/html
  ```

  会正常出现 标头为 `Tomcat Web Applocation Manager` 的网页。中文的话，标头为 `Tomcat Web应用程序管理者` 。

### 5.3 虚拟主机管理

- 网址如下：

  ```
  http://<your_domain_or_IP_address>:8080/host-manager/html
  ```

  会正常出现 标头为 `Tomcat Virtual Host Manager` 的网页。中文的话，标头为 `Tomcat虚拟主机管理员` 。



## 结束语

至此，已经展示了如何在 Ubuntu 上安装 Tomcat 9.0，并且如何访问 Tomcat 管理界面。想要获得更多关于 Apache Tomcat 的信息，浏览[官方文档页面](https://link.zhihu.com/?target=https%3A//tomcat.apache.org/tomcat-9.0-doc/index.html)。
