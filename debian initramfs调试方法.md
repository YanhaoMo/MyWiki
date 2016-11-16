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

# 修改 initramfs
前面说了，debian 中的 initramfs 主要是 initramfs-tools 在管理，因此在修改调试 initramfs 时，
最好还是能直接使用 initramfs-tools 提供的现成的方法来实现。当然，如果发现有些地方直接使用
initramfs-tools，那此时可以考虑修改 initramfs-tools 的脚本来实现想要的功能，
但是一般不要尝试完全手工去产生一个 initramfs 文档。

## 安装 initramfs-tools
initramfs-tools 是 debian 系统自带的工具，所以不需要手动安装。

## 配置文件
initramfs-tools 的配置文件位于 /etc/initramfs-tools 目录下，进入该目录查看一下内容：
```bash
$ cd /etc/initramfs-tools
$ ls
conf.d/ hooks/ initramfs.conf  modules  scripts/ update-initramfs.conf
```
如果要对 initramfs 进行定制修改，需要对 hooks 和 scripts 目录下的文件和 modules 进行操作，
modules 文件中定义了在构建 initramfs 时将会被包含的内核模块，每个模块占用一行，可以使用模块参数，
`#` 开头的行为注释行。

注意: 在使用`update-initramfs`时，`-k all`命令会忽略 modules 文件而默认将所有内核模块包含到
initramfs 中。

## hooks/
可以在 hooks/ 目录下添加自定义的脚本，该脚本在`mkinitramfs`命令执行时会被自动调用，
创建的自定义脚本文件内容需要遵守一定的规则:
每个脚本文件的起始处必须包含以下几行：
```bash
#!/bin/sh
PREREQ=""
prereqs()
{
   echo "$PREREQ"
}

case $1 in
    prereqs)
        prereqs
        exit 0
        ;;
esac

. /usr/share/initramfs-tools/hook-functions
 # Begin real processing below this line
```
包含这几行的主要目的是用来确保脚本能以一定的顺序执行，比如你需要确保这个脚本在执行之前，
lvm hook脚本先被执行，那么你需要将`PREREQ=""`替换为`PREREQ="lvm"`

/usr/share/initramfs-tools/hook-functions 脚本提供了许多在写 hook 脚本时很有用的函数，
具体信息可以参考 man initramfs-tools

## scripts/
scripts/ 下有很多子目录，这些子目录分别代表了 initramfs 执行的不同阶段，
可分别在这些子目录下创建自定义的脚本，在 initramfs 被挂载后，自定义脚本会在相应的阶段被执行，
从而达到定制 initramfs 行为的目的。

- init-top 这个目录下的脚本在 initramfs 挂载了 sysfs 和 procfs 后将首先被调用，
- 这个阶段也会调用 udev 脚本来初始化 /dev 目录下的设备文件。
- init-premount 当 hooks 脚本和 /etc/initramfs-tools/modules 文件中指定的内核模块加载后被调用。
- local-top 或者 nfs-top 这些脚本被调用后，真正的 rootfs 此时已经可见或者 nfs rootfs已经可用。
- local-block 这个子目录下的脚本会和相应的块设备文件一起被调用，之后应该可以正确识别相应的块设备文件，
- 如果 local-top 或者 local-block 调用失败，则相应的脚本会被定期调用重试。
- local-premount 或者 nfs-premount 这两个子目录下的脚本在真正的 rootfs 的一切状态都已被验证后被调用。
- 