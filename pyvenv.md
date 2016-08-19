# 简介
pyvenv和以前我们经常使用的virtualenv的作用基本一样,就是创建一个心的python运行环境,
这个运行环境是干净的,然后我们可以在这基础之上安装我们需要的包,不会对系统的主python库造成影响.

# 安装
在debian下安装:
```bash
sudo apt update
sudo apt -y install python3-venv
```
# 使用方法
首先创建一个新的python运行环境
```bash
pyvenv path/to/directory
```

然后source执行该目录下的`bin/active`命令
```bash
source {path-todirectory}/active
```