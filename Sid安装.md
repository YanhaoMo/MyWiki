# 安装sid
首先使用stable的安装镜像来安装一个最小系统，安装设置为：英文语言，中国地区，
en_US.UTF8 locales，英文键盘。


hostname: pc-sid  
user: hao

然后修改/etc/apt/source.list文件为sid的源，然后更新系统到sid。

# 安装桌面
```sh
sudo apt install xorg lightdm i3
```