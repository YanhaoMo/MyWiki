搭建Debian上的haskell开发环境：

```sh
apt install haskell-stack
```

修改stack的配置文件使其使用tuna的源：

修改~/.stack/config.yaml添加如下配置
```
setup-info: "http://mirrors.tuna.tsinghua.edu.cn/stackage/stack-setup.yaml"
urls:
  latest-snapshot: http://mirrors.tuna.tsinghua.edu.cn/stackage/snapshots.json
  lts-build-plans: http://mirrors.tuna.tsinghua.edu.cn/stackage/lts-haskell/
  nightly-build-plans: http://mirrors.tuna.tsinghua.edu.cn/stackage/stackage-nightly/
```

可以先执行一次 stack 命令使其自动生成相应的配置文件然后再进行修改

修改hackage配置到tuna的源，同样在上面的配置文件中添加如下行

```
package-indices:
  - name: Tsinghua
    download-prefix: http://mirrors.tuna.tsinghua.edu.cn/hackage/package/
    http: http://mirrors.tuna.tsinghua.edu.cn/hackage/00-index.tar.gz
```

使用stack来安装ghc编译器
```
stack setup
```

ghci  
使用`stack ghci`来启动ghci，为防止多次import导致prompt过长，可以执行以下命令来设置固定的提示符：
```sh
:set prompt "ghci> "
```

参考：
https://mirror.tuna.tsinghua.edu.cn/help/stackage/  
https://mirrors.tuna.tsinghua.edu.cn/help/hackage/