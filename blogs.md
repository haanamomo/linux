## ubuntu/lubuntu开机进入命令行

Ubuntu或者Lubuntu开机后无限重载，左上角显示闪烁的小光标。

开机直接进入命令行：

1.  选择系统界面选择`Ubuntu`，按`e`
2.  在倒数第2行的最后加上`3`, 按`F10`

## ubuntu/lubuntu修改终端字体

    ls /usr/share/consolefonts
    setfont Uni3-TerminusBold32x16.psf.gz
    echo 'setfont 字体名字'  >> /etc/profile
    

## ubuntu/lubuntu加快开机速度

检查开机速度

    systemd-analyze blame
    

禁用开机项，`.device`是挂载，不能disable

    sudo systemctl disable NetworkManager-dispatch.service
    sudo systemctl disable NetworkManager-wait-online.service
    
    sudo apt remove snapd