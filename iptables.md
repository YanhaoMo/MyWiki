# 清空现在的所有iptables配置
```sh
iptables -F
iptables -X
iptables -t nat -F
iptables -t nat -X
iptables -t raw -F
iptables -t raw -X
iptables -t mangle -F
iptables -t mangle -X
iptables -t security -F
iptables -t security -X
```