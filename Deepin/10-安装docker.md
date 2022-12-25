# deepin下docker安装



## 安装方法1

1. 首先终端输入 

   ```
   sudo apt install docker.io
   ```

2. 然后添加docker的源

   ```bash
   sudo deepin-editor /etc/docker/daemon.json
   ```

   ```bash
   sudo nano /etc/docker/daemon.json
   ```

   然后在json中添加

   ```json
   {
   "registry-mirrors": ["https://pee6w651.mirror.aliyuncs.com"]
   }
   ```

3. 把docker命令拉进管理员

   ```
   sudo groupadd docker
   sudo gpasswd -a $USER docker
   newgrp docker
   ```

4. 启动`docker`服务

   ```
   systemctl start docker.service
   ```

   注：关闭`docker`服务

   ```
   systemctl stop docker.service
   ```

5. 测试

    ```
    sudo docker run hello-world
    ```



## 安装方法2

1. 打开深度Deepin系统的终端，然后运行以下命令：

   ```
   sudo apt install docker-ce
   ```

   也可以直接运行

   ```
   sudo apt install docker*
   ```

   或者切换到root用户，执行

   ```
   curl https://get.docker.com | bash
   ```

2. 把docker命令拉进管理员

   ```
   sudo gpasswd -a $USER docker
   newgrp docker
   ```

3. 状态确认

   ```
   sudo systemctl status docker
   ```

4. 测试

   ```
   sudo docker run hello-world
   ```

   
