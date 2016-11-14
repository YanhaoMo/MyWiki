# 简介
cowbuilder 是 debian 官方提供的一个软件打包工具，它的作用是创建出一个独立的环境，
然后将 Debian 软件包源代码导入这个环境中打包。这样做有很多好处，首先这将软件打包环境独立出来，
使得软件打包不会弄乱你的机器实际的运行环境，其次，这样做有助于检查软件包的依赖关系是否正确，
因为 cowbuilder 创建出的独立环境通常是一个最小化环境，此时如果写错了依赖，在 cowbuilder 打包时就立刻能发现。

# 使用方法
使用 cowbuilder 打包之前，首先需要创建一个基础环境，以后的打包环境便是基于这个基础环境来构建
```bash
cowbuilder --create --distribution sid --basepath /var/cache/pbuilder/base-sid.cow --mirror http://mirrors.163.com/debian
```