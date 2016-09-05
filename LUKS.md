# LUKS简介

# 分区加密
在Debian系的系统中使用LUKS，首先要确保你的系统中已经正确安装了*cryptsetup*这个包

```sh
sudo apt update && apt install cryptsetup -y
```

假设我们要加密*/dev/sda5*这个分区，因为这个分区中存放着一些重要的数据，我们不想让其他人可以随意访问他。

首先执行以下命令，这会为你创建一个加密的数据分区：

```sh
sudo cryptsetup -y -v luskFormat /dev/sda1
```

然后系统会提示你输入一个大写的*YES*来确认你的操作，然后会让你输入密码。完成之后，这个分区就已经被加密了。

# 全盘加密(不包括/boot)

# 使用keyfile的全盘加密(不包括/boot)

# 使用keyfile的全盘加密(包括/boot)