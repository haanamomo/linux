# 查看cpu架构

```
lscpu | less
```

# ubuntu开机进入命令行

Ubuntu或者Lubuntu开机后无限重载，左上角显示闪烁的小光标。

开机直接进入命令行：

1.  选择系统界面选择`Ubuntu`，按`e`
2.  在倒数第2行的最后加上`3`, 按`F10`

# ubuntu开机黑屏

1. 选择系统界面选择`Ubuntu(Advanced)`
2. 选择`recovery mode`
3. 选择`dpkg  Repair broken packages`

# ubuntu修改终端字体

    ls /usr/share/consolefonts
    setfont Uni3-TerminusBold32x16.psf.gz
    echo 'setfont 字体名字'  >> /etc/profile
    

# ubuntu加快开机速度

检查开机速度

    systemd-analyze blame
    

禁用开机项，`.device`是挂载，不能disable

    sudo systemctl disable NetworkManager-dispatch.service
    sudo systemctl disable NetworkManager-wait-online.service
    
    sudo apt remove snapd


# 蓝牙

```sh
sudo hciconfig -a  # 列出蓝牙硬件
sudo hciconfig -a | grep HCI  # 查看蓝牙硬件版本
```

```sh
bluetoothctl
scan on
devices
quit
```