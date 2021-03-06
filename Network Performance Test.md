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

**启动`netserver`：**
```bash
sudo netserver -4 -p 12345
```

`-4`表示使用`ipv4`协议，`-p 12345`表示在`12345`端口上监听请求。

**运行`netperf`**

```bash
sudo netperf -4 -H hostname|ip -p 12345 -l 100 -t TCP_STREAM
```

`-4`表示使用`ipv4`协议，`-H`指定要测试的系统的hostname或者ip地址，`-p`指定对端端口号，`-l`表示总共测试多长时间（以秒为单位），`-t`指定测试类型，总共有以下
几种类型可选。

* TCP_STREAM
* TCP_SENDFILE
* TCP_MAERTS
* TCP_RR
* TCP_CRR
* UDP_STREAM
* UDP_RR
* DLCO_STREAM
* DLCO_RR
* DLCL_STREAM
* DLCL_RR
* STREAM_STREAM
* STREAM_RR
* DG_STREAM
* DG_RR
* SCTP_STREAM
* SCTP_STREAM_MANY
* SCTP_RR
* SCTP_RR_MANY
* LOC_CPU
* REM_CPU

### 利用 `netperf` 可以得到的测试信息
* 单个长TCP连接的最大网络吞吐量。（TCP_STREAM）
* 单个TCP连接多个连续请求和响应时的最大网络吞吐量。（TCP_RR）
* 系统建立&关闭一个tcp连接所有的时间。（TCP_CC）

**注意** `netperf`对并发请求的支持很不好，不建议使用netperf来测试网络并发性能。

## iperf[^2]

iperf 是一款可以用来测试网络（TCP或UDP）最大吞吐量的工具，可以进行并行测试，iperf也工作在C/S模式。

iperf启动服务器端：

```bash
sudo iperf -s -p 12345 -D
```

`-s`表示启动服务器程序，`-p`指定在特定端口监听请求，`-D`表示以守护进程方式运行。

客户端启动测试程序：

```bash
sudo iperf -c hostname|ip -p 12345 -t 120 -P 1000 -i 1
```

`-c`表示以客户端方式运行，后面跟着服务器的hostname或者ip地址，`-p`表示服务器端的端口号，`-t`表示测试总共运行时间，`-P`表示并发请求数量。
`-i`指定每隔多长时间报告测试结果。

## tcpkali[^3]

tcpkali是一种可以模拟数百万tcp请求的工具，也可以作为一种ddos工具。

# 参考连接

[^1]: [http://www.netperf.org/netperf/](http://www.netperf.org/netperf/)
[^2]: [https://iperf.fr/](https://iperf.fr/)
[^3]: [https://github.com/machinezone/tcpkali](https://github.com/machinezone/tcpkali)