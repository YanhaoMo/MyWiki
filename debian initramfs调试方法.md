在进行 debian 系统开发时，如果开发工作涉及对 initramfs 定制修改，
就需要对 debian 的 initramfs 有一个详细的了解。
本文希望通过对 linux 系统普遍使用的 initramfs 和 debian 系统如何自动生成使用 initramfs
的讲解，来减轻读者在 debian 系统及其衍生版本上开发调试 initramfs 时的麻烦。
# 简介
## 什么是 initramfs ？
首先需要弄清楚，initramfs是什么东西，要回答这个问题，我们要知道 linux 系统启动时的一般流程：

系统加电 -> biso中的固件 -> bootloader -> kernel -> 真正的系统

上述过程看起来顺理成章，但实际上从 kernel 到正真的系统启动这一过程中有许多困难