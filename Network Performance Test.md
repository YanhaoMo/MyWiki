# 测试目标
## 希望得到的信息
### 对于TCP连接
* 服务器最大可同时接受多少并发请求
* 服务器的网络吞吐率是多少
* 服务器的延迟性能如何

上面三个需求，其中后两个需要的是个变化的趋势，随着系统各种因素的变化，性能如何变化。

# 可用工具及相关用法
## netperf[^1]

netperf 以 C/S 模式来工作，需要在被测试的系统上用`netserver`启动服务器端，然后在客户端使用netperf来对其进行性能测试。

启动`netserver`：
```bash
sudo netserver -4 -p 12345
```

`-4`表示使用`ipv4`协议，`-p 12345`表示在`12345`端口上监听请求。

## iperf[^2]

# 参考连接

[^1]: [http://www.netperf.org/netperf/](http://www.netperf.org/netperf/)
[^2]: [https://iperf.fr/](https://iperf.fr/)