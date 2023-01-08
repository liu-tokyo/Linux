

# Ubuntu 上安装工具软件



## SSH 安装

桌面版安装的时候，可以选择安装该服务；我个人因为选择的是 最小安装，后期要用该服务的话，需要重新安装。  
个人用的话，也许意义不到，但是考虑到云端操作，都是没有用户界面的（可以节省至少 500MB 的内存），需要经常用到 SSH 服务。

- 安装指令

  ```bash
  sudo apt update
  sudo apt install openssh-server -y
  ```

- 查询状态

  ```bash
  sudo systemctl status ssh
  ```

- 开放防火墙

  ```bash
  sudo ufw allow ssh
  ```

- 连接到 SSH

  ```bash
  ssh username@ip_address
  
  ## 远程重启
  sudo reboot
  
  ## 远程关机
  sudo shutdown now
  ```

  需要查询 IP 的话：

  ```bash
  ip a
  ```

- 服务控制

  ```bash
  ## 禁用 SSH 服务器
  sudo systemctl disable --now ssh
  
  ## 开启 SSH 服务器
  sudo systemctl enable --now ssh
  ```

  