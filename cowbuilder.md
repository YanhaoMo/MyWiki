# 简介
cowbuilder 是 debian 官方提供的一个软件打包工具，它的作用是创建出一个独立的环境，
然后将 Debian 软件源码包导入这个环境中打包。这样做有很多好处，首先这将软件打包环境独立出来，
使得软件打包不会弄乱你的机器实际的运行环境，其次，这样做有助于检查软件包的依赖关系是否正确，
因为 cowbuilder 创建出的独立环境通常是一个最小化环境，此时如果写错了依赖，在 cowbuilder 打包时就立刻能发现。

# 安装
```bash
sudo apt install cowbuilder
```

# 使用方法
使用 cowbuilder 打包之前，首先需要创建一个基础环境，以后的打包环境便是基于这个基础环境来构建
```bash
cowbuilder --create --distribution sid --basepath /var/cache/pbuilder/base-sid.cow --mirror http://mirrors.163.com/debian
```

我们依次来讲解上面命令中各个参数的意义：

* --create 表示要从头开始创建一个新的基础环境，你可以创建很多基础环境，比如为debian的三个分支分别创建不同的基础环境
* --distribution 表示该环境所对应的代号(codename)
* --basepath 表示该基础环境的位置，注意该参数是一个目录(不必事先创建)
* --mirror 表示本次构建基础环境所使用的源站地址

创建完该基础环境，以后如果需要更新该环境，直接执行一下命令就可以了
```bash
cowbuilder --update --basepath /var/cache/pbuilder/base-sid.cow
```

**注意** cowbuilder 命令需要使用root权限来运行。

## 软件包构建
创建完基础打包环境之后，就可以使用该环境来进行软件打包：
```bash
cowbuilder --build --basepath /var/cache/pbuilder/base-sid.cow *.dsc
```

最后的一个参数是软件包的 dsc 文件，注意dsc文件必须和准备好的软件源代码在同一目录下。