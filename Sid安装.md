# 安装sid
首先使用stable的安装镜像来安装一个最小系统，系统镜像可以去下面下载：

- 中科大镜像源： [http://mirrors.ustc.edu.cn/debian-cd/current/amd64/iso-cd/](http://mirrors.ustc.edu.cn/debian-cd/current/amd64/iso-cd/)
- 清华镜像源： [https://mirrors.tuna.tsinghua.edu.cn/debian-cd/current/amd64/iso-cd/](https://mirrors.tuna.tsinghua.edu.cn/debian-cd/current/amd64/iso-cd/)

## 安装设置
- 语言： 英文
- 时区： 中国
- locales： locales
- 键盘布局： 美国英语
- hostname： pc-sid  
- 普通用户： hao

## 分区设置
- 一个efi分区：1G
- 一个swap分区：10G
- 一个根分区：余下的所有硬盘空间，挂载参数为noatime

安装系统组件： standard system utilities

**安装完系统之后，重启**

# 更新到sid
然后修改/etc/apt/source.list文件为sid的源，然后更新系统到sid。

```bash
sudo echo deb http://mirrors.ustc.edu.cn/debian sid main contrib non-free > /etc/apt/sources.list
sudo apt update
sudo apt full-upgrade
sudo apt autoremove
```

```sh
sudo apt install xorg lightdm i3
```