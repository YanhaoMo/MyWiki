# LUKS简介

# 数据分区加密

## 加密分区
在Debian系的系统中使用LUKS，首先要确保你的系统中已经正确安装了**cryptsetup**这个包
```sh
sudo apt update && apt install cryptsetup -y
```
假设我们要加密**/dev/sda5**这个分区，因为这个分区中存放着一些重要的数据，我们不想让其他人可以随意访问他。

首先执行以下命令，这会为你创建一个加密的数据分区：
```sh
sudo cryptsetup -y -v luskFormat /dev/sda5
```
然后系统会提示你输入一个大写的**YES**来确认你的操作，然后会让你输入密码。完成之后，这个分区就已经被加密了。

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
**注意，**这个时候**/dev/sda5**这个文件已经不能进行正常的建立文件系统，挂载等操作，而仅仅用来加解密，
相应的文件系统操作都应该对**/dev/mapper**目录下生成的文件来进行。

当进行完数据操作之后，通过以下命令来卸载分区，使分区重新回到加密状态。
```sh
sudo umount /dev/sda5
sudo cryptsetup luksClose cry_data
```
# 根分区加密(不包括/boot)

# 使用kyefile的普通系统分区加密

# 使用keyfile的根分区加密(不包括/boot)
假设你已通过上一节的方法安装了全盘加密(不包括/boot)的Debian系统，那么接下来介绍如何使用keyfile来进行全盘加密的自动解密。
用来解密的keyfile被存储在initramfs中。下面是具体步骤。

假设下面是现在的系统布局状况：

* /dev/sda1 /boot 不加密
* /dev/sda2 / 加密

### 生成keyfile
首先生成一段随机的二进制数据来作为我们的keyfile
```sh
sudo dd if=/dev/urandom of=/root/autounlock.key bs=512 count=4
sudo hmod 0400 /root/autounlock.key
```
### 使用keyfile加密根分区
然后将使用这个keyfile来加密系统分区
```sh
sudo cryptsetup luksAddKey /dev/sda2 /root/autounlock.key --key-slot 1
```
可以通过以下命令来进一步查看系统分区的加密状况
```sh
sudo cryptsetup luksDump /dev/sda2
```
### initramfs中加载keyfile的脚本
创建一个新的脚本，用来在initramfs中将这个keyfile导入系统。
```sh
sudo touch /lib/cryptsetup/scripts/getinitramfskey.sh
```
以下是`getinitramfskey.sh`文件的内容
```sh
#!/bin/busybox ash
# File : /lib/cryptsetup/scripts/getinitramfskey.sh
# Description : 
#   This script is called by initramfs using busybox ash. 
#   The script is added to initramfs as a result of /etc/crypttab option
#       "keyscript=/lib/cryptsetup/scripts/getinitramfskey.sh", && update-initramfs.
#   This script prints the contents of a key file to stdout using cat or dd. 
#   The key file location is supplied as $1 from the third field 
#       in /etc/crypttab, or can be hard-coded in this script.
#   If using a key embedded in initrd.img-*, a hook script in /etc/initramfs-tools/hooks/ 
#       is required by update-initramfs. The hook script copies the /root/autounlock.key 
#       file into the initramfs {DESTDIR}.
KEY="${1}"
if [ -f "${KEY}" ]; then
  cat "${KEY}"
else
  PASS=/bin/plymouth ask-for-password --prompt="Key not found. Enter LUKS Password: "
echo "${PASS}"
fi
```
给这个文件加上可执行权限：
```sh
sudo chmod +x /lib/cryptsetup/scripts/getinitramfskey.sh
```
### 创建`update-initramfs`hook脚本
然后再创建一个新的shell脚本，这个脚本在系统创建initramfs时被调用，作用是加载keyfile到initramfs中。
```sh
sudo /etc/initramfs-tools/hooks/loadinitramfskey.sh
```
`loadinitramfskey.sh`的内容：
```sh
#!/bin/sh
# File : /etc/initramfs-tools/hooks/loadinitramfskey.sh
# Description : This hook script is called by update-initramfs. The script checks for the existence of the key file loading script getinitramfskey.sh and copies it to initramfs if it's missing.
# This script also copies the key file autounlock.key to the /root/ directory of the initramfs. This file is accessed by getinitramfskey.sh, as specified in /etc/crypttab.
PREREQ=""
prereqs() {
  echo "$PREREQ"
}
case "$1" in
  prereqs)
    prereqs
    exit 0
  ;;
esac
. "${CONFDIR}/initramfs.conf"
. /usr/share/initramfs-tools/hook-functions
if [ ! -f "${DESTDIR}/lib/cryptsetup/scripts/getinitramfskey.sh" ]; then
  if [ ! -d "${DESTDIR}/lib/cryptsetup/scripts" ]; then
  mkdir -p "${DESTDIR}/lib/cryptsetup/scripts"
  fi
  cp /lib/cryptsetup/scripts/getinitramfskey.sh ${DESTDIR}/lib/cryptsetup/scripts/
fi
if [ ! -d "${DESTDIR}/root/" ]; then
  mkdir -p ${DESTDIR}/root/
fi
cp /root/autounlock.key ${DESTDIR}/root/
```
同样地，给这个文件加上可执行权限：
```sh
sudo chmod +x /etc/initramfs-tools/hooks/loadinitramfskey.sh
```

### 修改`/etc/crypttab`配置
修改`/etc/crypttab`文件，使之看起来像下面的样子
```text
sda2_crypt UUID=a8604976-269b-4ab1-8ecc-63960f60f008 /root/autounlock.key luks,discard,noearly,keyscript=/lib/cryptsetup/scripts/getinitramfskey.sh
```
### 重新生成initramfs
最后，需要执行命令来重新生成initramfs，
```sh
sudo update-ininramfs -u
```
这样，重启系统之后，你会发现，此时已经不再需要输入密码了，系统已经使用initramfs中存储的keyfile文件来自动解密了系统分区。

# 使用keyfile的全盘加密(包括/boot)