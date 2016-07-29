# 虚拟内存相关的参数（vm开头）

## vm.page-cluster

这个参数控制着当系统从swap区来读取数据时，每次连续读多少页面数，从swap读到的是页面缓存的预读副本。

实际系统的设置为vm.page-cluster的以2为底的幂。也就是说实际的值为2^vm.page-cluster^，当vm.page-cluster为0时表示关闭从swap的预读。

一般默认的vm.page-cluser为3，也就是说默认每次预读2^3^=8个页面，如果你的任务是swap密集型的，那么调节这个值应该会小幅优化系统性能。

调小这个值意味着可以更早地发现页面初始化错误，但是同时可能会引入其他的错误和io延迟。

## vm.swappiness

这个值定义了内核将页面置换到swap区的概率大小，也就是说，这个值越大，内核越倾向于将内存中的页面换出。0值意味着内核不会使用swap区，直到系统的空闲页面已经低于“警戒线”。

默认值是60。

## vm.dirty\_background\_bytes

当系统中的脏页数量达到vm.dirty\_background\_bytes时，内核开始启动flusher线程进行脏页回写。

## vm.dirty\_background\_raio

当系统中可用的内存（包括空闲页和可回收页）的数量低于vm.dirty\_background\_ratio（这是一个百分比）时，系统开始启动flusher内核线程将脏页进行回写。

## vm.dirty\_bytes

当系统内存的脏页达到这个数量时，向硬盘写数据的进程开始自己回写内存脏页。

vm.dirty\_bytes的最小合法值是两个页面的大小（以byte为单位）；任何低于这个值的设置会被忽略，同时系统会继续使用上一个旧的配置。

## dirty\_ratio

当系统中可用的内存（包括空闲页和可回收页）的数量低于vm.dirty\_ratio（这是一个百分比）时，向硬盘写数据的进程开始自己回写内存脏页。。

## vm.dirty\_expire\_centisecs

这个参数定义了：多老的内存页才会有资格被内核的flusher线程回写。这个值每100表示1秒。内存中符合这个值所规定的条件的脏页会在下一次flusher线程启动时被写到硬盘上。

## vm.dirty\_writeback\_centisecs

内核的fulsher线程会定期地启动来将旧的数据写到硬盘上，dirty\_writeback\_centisecs定义了fulsher线程启动的时间间隔。每100表示1秒。

将这个值设置为0会关闭系统定期回写旧数据这个功能。

## vm.min\_free\_kbytes

这个值被用来设置系统的最小空闲内存空间，以kb为单位。linux的虚拟内存子系统会使用这个
值来为每一个低内存空间计算一个警戒线。每个地内存空间所对应的保留的空闲内存空间的大小与他本身的内存空间大小成比例。

# NET CORE相关参数

## bpf\_jit\_enable

这个参数用来开启或者关闭 Berkeley Packet Filter[^1]
在当前对x86\_64的支持上，bpf\_jit提供了一个加速包过滤的框架，tcpdump/libpcap
就使用了这个功能。

不同值的意义：

-   0 - 关闭 JIT 功能
-   1 - 开启 JIT 功能
-   2 - (没看懂)

## bpf\_jit\_harden

这个参数用来加固 Berkeley Packet Filter JIT compiler。它使用 eBPF
后端。开启这个功能会稍微降低系统性能，但是可以（可以干啥？没看懂）

各个值的意义：

-   0 - 关闭 JIT hardening （默认行为）
-   1 - 仅对root开启 JIT hardening
-   2 - 对所有用户都开启 JIT hardening

## rmem\_default

默认的socket接受缓存大小，以byte为单位。

## rmem\_max

系统的接受缓存上限，以byte为单位。

## wmem\_default

默认的发送缓存大小，以byte为单位

## wmem\_max

发送缓存的上限，以byte为单位。

# TCP相关参数


## forwarding

在这个网络接口上开启IP包转发。

## net.ipv4.tcp\_window\_scaling

设置为1使能tcp窗口缩放（在RFC1323文档中定义），开启该项有利于提高网络性能。

## tcp\_slow\_start\_after\_idle

如果使能这个参数，那么系统会在tcp连接在空闲一定时间之后重置连接的拥塞窗口（RFC2861），这样做的原因是在连接空闲一定时间之后，网络状态可能发生系统无法预料的改变。如果不设置这个参数，系统便不会在空闲一定时间之后重置拥塞窗口。

使能这个参数有利于拥塞控制，但是对性能会有一些不利影响，特别是在系统有很多长时间的tcp连接的时候。

## tcp\_fastopen

tcp快速打开可以使tcp连接在第一次握手的时候就开始发送数据。

## icmp\_echo\_ignore\_all

当值为非0时内核会无视所有发送来的 ICMP ECHO 消息。

## icmp\_echo\_ignore\_broadcasts

当这个值为非0时，内核会素食所有以广播方式发来的 ICMP ECHO 和 ICMP
TIMESTAMP 请求。

## net.ipv4.ip\_forward

开启包转发功能，这个功能在普通主机上应该关闭，而在需要路由转发的场合比如路由器上应该开启。

## arp\_filter

-   0 -
    这个是默认值，此时系统会响应别的网络接口的arp请求，这在一些情况下是很有用的。因为这样可以增大通信成功的概率。在Linux系统中，ip地址的所有者是操作系统，而不是某个特定的网络接口。只有在一些特别复杂的配置，比如负载均衡中，这个值才会导致出现一些问题。
-   1 -
    允许你在同一个网段中拥有多个网络接口，并且对于每一个arp接口的请求都会被响应（这取决于内核会不会。\#\#\#\#\#\#也就是说这个设置允许你来控制此时哪一个网卡会对arp请求进行应答。

当至少一个conf/{all，interface}arp\_filter为TRUE时，arp\_filter会被开启，其他情况下会被关闭。

## arp\_ignore

这个参数定义了不同的模式来发送arp应答：

-   0 - 默认值，回应任何网络接口上对任何本地IP地址的arp查询请求。
-   1 - 只回应目标ip地址是本地地址的arp查询请求。
-   2 -
    只回应目标ip地址是本地地址的arp查询请求，并且源ip地址必须和目的ip地址处在同一个网段内。
-   3 - do not reply for local addresses configured with scope host,only
    resolutions for global and link addresses are replied
-   4-7 - 保留未使用
-   8 - 对所有arp请求都不回应。

## arp\_notify

定义了不同模式来广播发送地址和设备变动。

-   0 - 不做任何事情。
-   1 - 当ip或设备变动时发送arp请求。

# 参考链接

[^1]: [<https://en.wikipedia.org/wiki/Berkeley_Packet_Filter>](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter)