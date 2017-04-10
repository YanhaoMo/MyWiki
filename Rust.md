# 搭建rust开发环境
安装rust编译器与包管理器
```
# apt install rustc cargo
```

配置cargo使用ustc的源：

在 $HOME/.cargo/config 中添加如下内容：

```
[source.crates-io]
replace-with = 'ustc'

[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"
```