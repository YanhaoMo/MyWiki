# 在Linux中将新用户添加到组之后立即生效
比如要将普通用户`hao`添加到`docker`组使其能够操作docker容器,首先需要执行命令将`hao`添加到该组:
```bash
sudo gpasswd -a hao docker
```

# 修改Oh-My-Zsh `robbyrussell` 主题分辨root和普通用户
