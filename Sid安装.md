# 安装sid
首先使用stable的安装镜像来安装一个最小系统，系统镜像可以去下面下载：

- 中科大镜像源： http://mirrors.ustc.edu.cn/debian-cd/current/amd64/iso-cd/
- 清华镜像源： https://mirrors.tuna.tsinghua.edu.cn/debian-cd/current/amd64/iso-cd/

安装设置为：英文语言，中国地区，
en_US.UTF8 locales，英文键盘。


hostname: pc-sid  
user: hao

分区设置：
一个efi分区，一个swap分区，一个/分区，挂载参数为noatime

安装 standard system utilities

然后修改/etc/apt/source.list文件为sid的源，然后更新系统到sid。

# 安装桌面
```sh
sudo apt install xorg lightdm i3
```