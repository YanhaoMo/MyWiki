鉴于Debian源里的nodejs比较坑，所以最好通过nodejs官方的源来安装nodejs

步骤如下：

以root用户执行下面的命令
```
curl -sL https://deb.nodesource.com/setup_7.x | bash -
apt-get install -y nodejs
```

使用nodejs 淘宝源：

1. 仅使用淘宝源
```
npm config set registry https://registry.npm.taobao.org
```

2. 使用cnpm
```
 npm install -g cnpm --registry=https://registry.npm.taobao.org
```