# 安装DEBIAN

> 感觉同样的内核，Debian 要比 Ubuntu 的运行速度更快。

## 1. 安装DEBIAN

先版本安装比较简单，按照提示即可。

## 2. 系统调整

## 3. 工具软件

## 4. 拼音输入法

中文版默认是 `智能拼音`，不是最新的输入法。

- 一般来说系统都带有多种输入法，如下指令调整

  ```bash
  im-config
  ```

### 4.1 Debian 12.6

- 卸载旧版输入法

  ```bash
  sudo apt purge fcitx* ibus*
  ```

- 安装fcitx5中文拼音输入法

  ```bash
  sudo apt install fcitx5 fcitx5-chinese-addons
  ```

- 重启系统

- 打开fcitx配置，查看信息

  保持默认配置即可，无需调整。可以看到启用fcitx中文输入法快捷键是“Ctrl+空格键”，英文输入法与fcitx中文拼音输入法之间切换键：“左Shift键”。

安装之后，在保持日文键盘的情况下，`CTRL + 空格`，就可以方便输入中文汉字，要比原有的输入法方便。