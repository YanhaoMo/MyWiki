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

## 更新基础chroot环境
```bash
sbuild-update -udcar unstable-$arch
```

# 使用sbuild构建软件包
### 构建本地软件包
```bash
sbuild -d kui *.dsc
```

### 构建源里的软件包
```bash
sbuild -d kui PACKAGENAME
```
此操作会将自动下载软件源里的源代码，然后尝试进行构建。

注意，在jessie之前版本中包含的sbuild在执行此操作时需要保证参数形式为 packagename_version，
jessie 之后的版本无此要求，当省略 version 部分时，sbuild将自动尝试最新版的软件源代码。
