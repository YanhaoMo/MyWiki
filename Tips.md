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
    local ret_status="%(?:%{$fg_bold[blue]%}➜ :%{$fg_bold[red]%}➜ %s)"
else
    local ret_status="%(?:%{$fg_bold[green]%}➜ :%{$fg_bold[red]%}➜ %s)"
fi
```