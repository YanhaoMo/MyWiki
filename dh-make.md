# 简介
dh-make 是 Debian 官方提供的一个包，用来根据用户指定的参数来自动生成一个用于打包debian目录。

dh\_make命令是该软件包中最常使用的一个，另外该软件包还包含用与于对字体进行打包的dh\_makefont工具。

下面的内容主要讨论 dh_make 的用法。

# 环境变量
dh_make 读取一写些环境变量来调整自己的行为：

* DEBEMAIL 打包者的 email 地址
* DEBFULLNAME 打包这的名字

# 主要参数

* -c --copyright 指定软件包使用的许可证类型，可选的有 gpl, gpl2, gpl3, lgpl, lgpl2 lgpl3, artistic, apache, bsd, mit 和 custom
* -n --native 创建 3.0(native) 格式的软件包
* -f --file 指定源代码包的位置