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

#安装 express 开发环境
```
# npm install express-generator -g
```

# 一些学习js时碰到的问题
- 既然有了let和const关键字，那么何时还需要var关键字？
- 箭头函数的词法作用域什么意思？
