# image0
`image0`表示一个原始的安装好的操作系统镜像，用来快速启动一个开发或者测试环境。

## debian-sid-iamge0, deepin-server-image0

必要软件：vim、ssh

- 关闭防火墙
- 打开root用户的ssh登陆许可
- 安装vim并启用语法高亮
- 配置好bash高亮
- 配置好软件源，更新系统到最新状态
- 设置grub启动等待时间为0
- 保证设置好足够大的系统空间
- 设置root弱密码