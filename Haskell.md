搭建Debian上的haskell开发环境：

```sh
apt install ghc haskell-stack
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
