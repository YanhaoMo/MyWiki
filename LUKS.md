# LUKS简介

# 分区加密
在Debian系的系统中使用LUKS，首先要确保你的系统中已经正确安装了*cryptsetup*这个包

```sh
sudo apt update && apt install cryptsetup -y
```

# 全盘加密(不包括/boot)

# 使用keyfile的全盘加密(不包括/boot)

# 使用keyfile的全盘加密(包括/boot)