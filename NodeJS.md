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

# react开发
## 使用create-react-app
```
# npm install -g create-react-app
```

创建一个初始开发环境
```
$ create-react-app new hello
```

## 手动布置react开发环境
```
mkdir hello && cd hello
npm init
npm i -s react react-dom
npm i -S babel-core babel-preset-es2015 babel-preset-react babel-preset-env
npm i -S webpack babel-loader
```

## 配置babel
创建.babelrc文件，写入如下内容
```
{
    "presets": ["env", "es2015", "react"]
}
```

## 配置webpack
下面是一个webpack配置的例子：
创建文件`webpack.config.js`,写入如下内容：
```
var path = require('path');

var BUILD_DIR = path.resolve(__dirname, 'public');
var APP_DIR = path.resolve(__dirname, 'src');

var config = {
    entry: APP_DIR + '/index.jsx',
    output: {
        path: BUILD_DIR,
        filename: 'bundle.js'
    },
    module : {
        rules : [
        {
            test : /\.jsx?/,
            include : APP_DIR,
            loader : 'babel-loader'
        }
        ]
    },
    devServer : {
        contentBase: path.join(__dirname, "/public"),
        compress: true,
        port: 8080
    }
};
```