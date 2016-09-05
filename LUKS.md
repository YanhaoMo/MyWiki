# LUKS简介

# 分区加密

## 加密分区
在Debian系的系统中使用LUKS，首先要确保你的系统中已经正确安装了*cryptsetup*这个包
```sh
sudo apt update && apt install cryptsetup -y
```
假设我们要加密*/dev/sda5*这个分区，因为这个分区中存放着一些重要的数据，我们不想让其他人可以随意访问他。

首先执行以下命令，这会为你创建一个加密的数据分区：
```sh
sudo cryptsetup -y -v luskFormat /dev/sda5
```
然后系统会提示你输入一个大写的*YES*来确认你的操作，然后会让你输入密码。完成之后，这个分区就已经被加密了。

## 使用加密后的分区
要想使用加密过的分区，首先需要使用之前设置的密码对其解密才行。
```sh
sudo cryptsetup luskOpen /dev/sda5 crypt_data
```
该命令会提示你输入密码解密该分区，成功之后，系统的**/dev/mapper**目录下出现一个**crypt_data**块设备文件，
该文件的文件名就是上一步**luskOpen**时的最后一个参数。

然后就可以对这个快设备文件进行操作，比如建立文件系统、挂载、读写等，就像普通的快设备文件一样。
```sh
sudo mkfs.ext4 /dev/mapper/crypt_data
sudo mount /dev/mapper/crypt_data /mnt
```
**注意** 注意，这个时候**/dev/sda5**这个文件已经不能进行正常的建立文件系统，挂载等操作，而仅仅用来加解密，
相应的文件系统操作都应该对**/dev/mapper**目录下生成的文件来进行。

当进行完数据操作之后，通过以下命令来卸载分区，使分区重新回到加密状态。
```sh
sudo umount /dev/sda5
sudo cryptsetup luksClose cry_data
```
# 全盘加密(不包括/boot)

# 使用keyfile的全盘加密(不包括/boot)

# 使用keyfile的全盘加密(包括/boot)