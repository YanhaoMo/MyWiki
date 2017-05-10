# 安装
```
apt install golang
```

# 配置go get 使用代理
这个比较麻烦，由于go语言的包管理器不支持切换源站，而且想golang.org这种网站的内容也不好做同步
因此国内并没有什么go软件包的镜像站。

这种情况我们只能使用http代理来访问被墙的golang.org 

首先安装polipo，它可以将socks5代理转为http代理，debian中的polipo弱依赖dnsmasq，但是其实我们并不需要它，所以：

```
# apt —no-install-recommends install polipo
```

##　然后配置polipo
/etc/polipo/config
```
socksParentProxy = "127.0.0.1:1080"
socksProxyType = socks5
proxyAddress = "::0"
logSyslog = true
logFile = /var/log/polipo/polipo.log
proxyPort = 1081
```

之后使用
```
env https_proxy=127.0.0.1:1081 go get
```

来安装包就可以了
