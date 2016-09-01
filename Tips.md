# 在Linux中将新用户添加到组之后立即生效
比如要将普通用户`hao`添加到`docker`组使其能够操作docker容器,首先需要执行命令将`hao`添加到该组:
```bash
sudo gpasswd -a hao docker
```
此时`hao`已经被添加到docker组中了,但是对当前会话并没有生效,正常情况下需要重新登录才能使用docker命令.

可以使用`newgrp`命令来暂时将`hao`的主用户组切换为docker,这样`hao`就可以立即拥有执行docker命令的权限,
当然不要忘记用完再换回来.
```bash
newgrp docker
# 用完再换回原来的主组
newgrp hao
```

# 修改Oh-My-Zsh `robbyrussell` 主题分辨root和普通用户
修改文件`${ZSH}/themes/robbyrussell.zsh-theme` 添加如下内容:
```bash
if [ $(whoami) = "root" ]; then
    local ret_status="%(?:%{$fg_bold[red]%}➜ :%{$fg_bold[yellow]%}➜ %s)"
else
    local ret_status="%(?:%{$fg_bold[green]%}➜ :%{$fg_bold[yellow]%}➜ %s)"
fi
```
这样,普通用户的箭头会显示为绿色,而root用户的箭头显示为红色,错误的返回状态一律显示为黄色.

# debian系统静默安装软件
使用debconf-get-selections 查到对应的包需要回答的问题，然后用debconf-set-selections来设置改问题。

# image0
`image0`表示一个原始的安装好的操作系统镜像，用来快速启动一个开发或者测试环境。

## image0 的修改

- 关闭防火墙
- 打开root用户的ssh登陆许可
- 安装vim并启用语法高亮
- 配置好bash高亮
- 配置好软件源，更新系统到最新状态
- 设置grub启动等待时间为0
- 保证设置好足够大的系统空间