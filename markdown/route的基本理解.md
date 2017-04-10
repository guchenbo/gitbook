### route的基本理解

```linux
[root@cregu ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.28.0    0.0.0.0         255.255.255.0   U     0      0        0 eth0
169.254.0.0     0.0.0.0         255.255.0.0     U     1002   0        0 eth0
0.0.0.0         192.168.28.2    0.0.0.0         UG    0      0        0 eth0
```



其中：

destination 表示目标的网域地址（network）

gateway 网关ip

genmask 子网掩码，与destination组合成为一个网段（网域）

flags 

​	U，表示有效

​	G，表示需要经由gateway来传递

Iface	表示网络接口（网卡）