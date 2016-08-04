# TCP 协议

# 拥塞控制

拥塞控制的几个关键词

慢开始，拥塞避免，快恢复，快重传

下面的几个变量是用来配置拥塞控制的。

* snd_cwnd          设置拥塞窗口大小
* snd_ssthresh      慢开始门限
* snd\_cwnd_cnt
* snd\_cwnd_clamp
* snd\_cwnd_stamp
* snd\_cwnd_used