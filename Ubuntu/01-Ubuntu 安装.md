

# Ubuntu 上安装工具软件

## 1. 更新 snap-store

- 从 22.04 开始，Ubuntu 的系统软件采用 SNAP 方式，系统更新使用如下指令：  

  ```bash
  sudo snap refresh
  ```

- 然而，snap-store 却无法更新自身，按照如下指令进行更新：  

  ```bash
  ## 终端输入如下指令，无法更新的话，会显示 snap-store 的进程号
  sudo snap refresh snap-store
  ## 若显示“正在运行”，则杀死该进程
  kill `进程号`
  ## 再次执行，就能够正确更新
  sudo snap refresh snap-store
  ```

## 2. SSH 安装

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

  

## 3. 邮箱 - ThunderBird

Linux 上比较流行的邮箱服务工具，我个人也在用。

- 官方下载

  https://www.thunderbird.net/zh-CN/

- 安装手册

  https://support.mozilla.org/zh-CN/kb/linux-thunderbird

- 安装指令

  ```bash
  ## 打开终端并找到下载文件路径，比如：
  cd ~/Downloads
  # 直接在下载文件的目录下，打开 终端 更简单。
  
  ## 使用命令解压文件：
  tar xjf thunderbird-*.tar.bz2
  
  ## 将解压后的文件放到 /opt：
  sudo mv thunderbird /opt
  
  ## 创建 Thunderbird 可执行文件的链接：
  sudo ln -s /opt/thunderbird/thunderbird /usr/local/bin/thunderbird
  
  ## 下载一份桌面文件：
  sudo wget https://raw.githubusercontent.com/mozilla/sumo-kb/main/installing-thunderbird-linux/thunderbird.desktop -P /usr/local/share/applications
  ```

- 软件卸载

  直接在 Ubuntu软件中心，点击右键卸载软件。

  或者参考如下指令：
  
  ```bash
  ## 删除libreoffice
  sudo apt-get remove libreoffice-common
  
  ## 删除其他不必要的软件
  sudo apt-get remove thunderbird totem rhythmbox simple-scan gnome-mahjongg aisleriot gnome-mines cheese transmission-common gnome-sudoku
  ```
  
  
  
  
  
  
  
  
  
  