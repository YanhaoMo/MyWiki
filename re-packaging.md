#对deb包重新打包
有时不可避免的会使用一些第三方的包，但是这些包一般都不怎么遵守debian的规范，所以需要对这些包手动重新打包。

方法也很简单：
首先要将这个包解包，假设这个包的名字为 foo.deb
```sh
dpkg -x foo.deb foo
dpkg -e foo.deb foot/DEBIAN
```
然后进入deb目录，进行必要的修改，最后需要重新打包foo：
```sh
dpkg foo foo.deb
```