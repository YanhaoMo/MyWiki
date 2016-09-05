# 简介
Schroot允许用户在一个特殊的chroot环境中执行命令或者运行交互式shell程序。

如非特殊说明，本页中的所有命令都需要root权限来执行

# 安装
schroot存在于官方源中，所以直接使用保管理器来安装即可：
```sh
apt update && apt install schroot -y
```
schroot需要使用debootstrap来初始化一个运行环境，所以debootstrap这个包也是必需的：
```sh
apt update && apt install debootstrap -y
```
# 配置文件
schroot的配置文件位于`/etc/schroot/schroot.conf`文件和`/etc/schroot/schroot.d`目录中。