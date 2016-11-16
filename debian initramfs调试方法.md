# 简介
在进行 debian 系统开发时，如果开发工作涉及对 initramfs 定制修改，
就需要对 debian 的 initramfs 有一个详细的了解。
本文希望通过对 linux 系统普遍使用的 initramfs 和 debian 系统如何自动生成使用 initramfs
的讲解，来减轻读者在 debian 系统及其衍生版本上开发调试 initramfs 时的麻烦。

# 什么是 initramfs ？
## 为什么需要 initramfs
首先需要弄清楚，initramfs是什么东西，要回答这个问题，我们要知道 linux 系统启动时的一般流程：

系统加电 -> biso中的固件 -> bootloader -> kernel -> 真正的系统

上述过程看起来顺理成章，但实际上从 kernel 到真正的系统启动这一过程中有许多困难，
最主要的问题是：根系统可能位于不同的硬件，不同的文件系统之上，而由于内核的模块机制，
相应的硬件或者文件系统驱动当时可能并不存在于 linux 内核的二进制文件中，
因而这时在 bootloader 加载内核之后，并不能正确识别出根文件系统。

因此在这个地方我们需要一个机制来帮系统从 kernel 正确过渡到真正的根文件系统。
这也正是 initfamfs 发挥作用的地方，也就是说：initramfs 解决了这个问题。

## initramfs
initramfs是一个压缩过的cpio文档，在debian系统中，它一般位于 /boot/ 目录下，
文件名为 /boot/initrd.img-*kversion* ，在系统的根目录下还有一个 /initrd.img
文件，这个文件是指向系统中安装的最新 initramfs 的软链接。

在使用 debian 系统时，initramfs 由 initramfs-tools 程序自动生成，因此你一般不需要手动修改这个文件，
在系统启动时，内核会自动加载这个文件到内存，解压出其中的内容，然后把 initramfs 当作
rootfs 来挂载，挂载之后，会启动1号用户空间程序 /init ,接下来 /init
完成直到挂载真正的根文件系统之前的所有工作，并最后挂载根文件系统到 /root ，
这样，系统就正常过渡到了真正的系统。

## 与真正的 rootfs 的不同
可以看到，initramfs 是系统启动时第一个被挂载的 rootfs，但是它与真正的 rootfs 有很多不同，
下面是一些总结：

- initramfs 是完全存在于内存中的一个内存文件系统，而真正的 rootfs 往往都是存在于硬盘上的硬盘文件系统
- initramfs 在体积上做了很多裁剪，包括使用适合嵌入式设备的klibc和busybox来替换正真系统中的glibc和许多应用
- 内核会以 pid1 启动 initramfs 上的 /init 而在真正的系统上启动的是 /sbin/init