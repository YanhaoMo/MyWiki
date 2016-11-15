# 简介
sbuild 同 pbuilder 功能类似，是 debian 官方软件包构建服务 buildd 的底层工具

# 使用
## 安装
使用 sbuild ,首先需要安装相应的软件包
```bash
apt install sbuild
```

## 初始化基础chroot环境

```bash
mkdir -p /root/.gnupg
sbuild-update --keygen
sudo sbuild-adduser $LOGNAME
sbuild-createchroot --include=gnupg,ccache sid /srv/chroot/unstable-amd64-sbuild http://httpredir.debian.org/debian
```