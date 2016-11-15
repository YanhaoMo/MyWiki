# 初始化一个最小环境
```bash
debootstrap --include linux-image-amd64,locales,grub-efi-amd64,vim,btrfs-grops,sudo --arch amd64 sid /mnt 
```