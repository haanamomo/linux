## 查看cpu架构

```
lscpu | less
```

## ubuntu开机进入命令行

Ubuntu或者Lubuntu开机后无限重载，左上角显示闪烁的小光标。

开机直接进入命令行：

1.  选择系统界面选择`Ubuntu`，按`e`
2.  在倒数第2行的最后加上`3`, 按`F10`

## ubuntu开机黑屏

1. 选择系统界面选择`Ubuntu(Advanced)`
2. 选择`recovery mode`
3. 选择`dpkg  Repair broken packages`

## ubuntu修改终端字体

    ls /usr/share/consolefonts
    setfont Uni3-TerminusBold32x16.psf.gz
    echo 'setfont 字体名字'  >> /etc/profile
    

## ubuntu加快开机速度

检查开机速度

    systemd-analyze blame
    

禁用开机项，`.device`是挂载，不能disable

    sudo systemctl disable NetworkManager-dispatch.service
    sudo systemctl disable NetworkManager-wait-online.service
    
    sudo apt remove snapd


## 蓝牙

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

## 无线网卡

```sh
# 查看有没有无线网卡
iwconfig
```

## apt

换源

```sh
cd /etc/apt
mv sources.list sources.list.bak
sudo vim sources.list
```

> [unrecoverable fatal error, aborting: files list file for package 'linux-generic' is missing final newline](https://askubuntu.com/questions/909719/dpkg-unrecoverable-fatal-error-aborting-files-list-file-for-package-linux-ge)


```
sudo rm /var/lib/dpkg/info/linux-generic.list
sudo dpkg --configure -a
sudo apt update
sudo apt upgrade
sudo apt install --reinstall linux-generic
```

## awk

awk是一种批量行操作的工具

```sh
awk [option] 'lineFilter {action}' file
# 或者
stdout | awk [option] 'lineFilter {action}'
```

option:
* `-F ','`      指定分隔符. 默认的分隔符是空格
* `-f xx.awk`   执行awk脚本

lineFilter：
* 无：对每一行
* `/some/`：对包含some的行

action: 
* print: 操作完一行后自动换行
* printf: 操作完一行后不自动换行

内置变量:
* `$0`: 整行
* `$n`: 第n个字段
* `"%-8s", $1`：第1个字段长度为8左对齐
* `"% 8s", $1`：第1个字段长度为8右对齐
* `NR`: 行号
* `NF`: 字段数
* `FS`: 字段分隔符，默认为空格
* `OFS`: 输出时的字段分隔符, 用`\t`会自动对齐
* `FILENAME`: 当前输入文件的名字
* `FNR`: 当前行数

例子：
* `awk '{ print $1 }'`: 对每一行，打印第一个字段
* `awk '{printf "%-10s %-10s\n", $1, $2}'`：对每一行，打印第一个字段和第二个字段，长度为都为10，左对齐
* `awk 'NR > 1 { print $1 }'`: 跳过第一行
* `awk '$3 > 0 { print $1 }'`：只对第三个字段大于0的行进行操作


```
awk 'BEGIN{FS=":"} {print $1, $3, $6}' OFS="\t" /etc/passwd
```

* 输入的字段分隔符为`:`
* 打印第1, 3, 6个字段
* 用tab自动对齐

### 拼接markdown

```sh
awk  'FNR==1 {gsub(/.md/,"",FILENAME);print "\n\n##", FILENAME, "\n"} 1' *.md > all.md; echo -e "# ${PWD##*/}$(cat all)" > all.md ; mv all.md ../${PWD##*/}.md
```
