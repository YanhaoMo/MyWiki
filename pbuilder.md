# 简介
pbuiler用于在debian上创建一个新的运行环境，类似与docker，但是主要是为了进行软件打包而创建的。

pbuilder的参数比较多，使用起来稍微有些复杂

# 安装
```bash
sudo apt install pbuilder
```

# 构建一个初始化环境
```bash
pbuilder create --basetgz ./base.tgz --distribution sid --mirror http://mirrors.163.com/debian --architecture amd64 --components main contrib non-free 
```

分别介绍一下上面的几个参数：  
* `--basetgz` 指定存储这个基础环境的文件，这个基础环境被存储为一个压缩文件
* `--buildresult` 指定用这个基础环境创建的deb包等文件最后会被存储到哪儿，默认是`/var/cache/pbuilder/result/`

# 构建一个deb包
```bash
pubilder build dsh_*dsc
```