# 光猫桥接模式下使用openwrt路由器访问光猫配置教程 - Allen Hua 的网络博客
2021年04月23日 [Allen Hua](https://hellodk.cn/author/1/ "作者：Allen Hua") 15716 4180 字

更新
--

### 2023-04-10 13:32:46

2023年再来更新一些说明：

*   后记中的内容缺乏实践，暂时没有测试环境，暂时不去求真了
*   如果你看到本文是为标题而来，为了实现需求，请着重看 **正文** 和 `Reference` 引用部分即可，其他的不用看

### 2021-05-15 11:51:43

![](https://fastly.jsdelivr.net/gh/hellodk34/image@main/img/20210515115118.png)

如果新建 ToModem 这个接口的时候设置了 `255.255.255.0`的掩码，并且接口 ip 地址就是 `192.168.1.254` （或者其他，主机位只要不是0、1、255 这三个就行），则不需要添加静态路由了，因为从上图你可以发现，创建好这个接口（这个接口绑定物理网卡是 `eth4` 也就是 wan 那个）后这个系统中就已经存在到达 `192.168.1.0/24` 这个网络的路由表项了，所以数据包从 `10.10.10.x` 到 `192.168.1.1` 肯定是可达的。

在局域网中的电脑跟踪一下路由看看

```null
# 这是局域网中的机器，这台机器的 ip 是 10.10.10.168
# traceroute 192.168.1.1
traceroute to 192.168.1.1 (192.168.1.1), 64 hops max, 52 byte packets
 1  dkrouter.lan (10.10.10.1)  8.376 ms  1.864 ms  1.820 ms
 2  192.168.1.1 (192.168.1.1)  3.227 ms  2.668 ms  2.465 ms
```

正文
--

一般光猫的 ip 地址默认都是 `192.168.1.1`

我的局域网的 ip 地址通常设置成 `10.10.10.0/24` 这个网络，openwrt 软路由的ip地址是 `10.10.10.1`，作为 AP 使用的 K2P 的 ip 地址是 `10.10.10.2`，作为服务器一直运行着的 thinkpad t400 的地址是 `10.10.10.3`，然后其他连接到软路由或者 k2p 上的设备 ip 都是 `10.10.10.x`

现在光猫已经作为桥接模式运行了，openwrt 拨号使用，这样对于 pt 的上传会有好处。

如何不改光猫的ip(改成 10.10.10.x)实现openwrt路由器（乃至于局域网中的其他设备）访问光猫呢？

很简单

1.  新建一个接口 tomodem，接口名称随意定义，新接口协议必须是静态地址，包括的接口是路由器上的 wan 接口，比如我这里的是 `eth4`，要求ip和光猫同网段（比如说设置成192.168.1.254，不能和光猫ip冲突），子网掩码设置成 `255.255.255.0`
2.  设置使用网关跃点 `100`
3.  防火墙选择 wan tomodem

![](https://fastly.jsdelivr.net/gh/hellodk34/image@main/img/tomodem1.jpg)

> 创建接口的详细图片解释

下面创建一条静态路由

1.  接口选择刚刚创建的 tomodem
2.  对象是 192.168.1.1 也就是光猫的ip地址。由于对象是一个host 而不是network 所以掩码可以不用填
3.  IPv4 网关是 tomodem 接口的ip地址，这里是192.168.1.254
4.  跃点数填100
5.  mtu使用默认的1500
6.  路由类型使用默认的 unicast 都填好了点击下面的「保存&应用」

![](https://fastly.jsdelivr.net/gh/hellodk34/image@main/img/20210423150006.png)

到这里就设置好了。建议重启网络

```null
/etc/init.d/network restart
```

ssh 进 openwrt

我这机器上共有5个网口，eth0 到 eth3 都是桥接后的 lan，接口名称叫 `br-lan` 它的ip地址是 `10.10.10.1` 连接到家里设计的局域网的设备ip都是 `10.10.10.x`

```null
# ifconfig br-lan
br-lan    Link encap:Ethernet  HWaddr A0:36:9F:85:95:2C  
          inet addr:10.10.10.1  Bcast:10.10.10.1  Mask:255.255.255.0
          inet6 addr: fe80::a236:9fff:fe85:952c/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:49893245 errors:0 dropped:0 overruns:0 frame:0
          TX packets:51913772 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:109981699938 (102.4 GiB)  TX bytes:39671384074 (36.9 GiB)
```

看看 wan 这个接口，新增的接口 tomodem 也使用的这个物理接口。可以看到 ipv4 地址是 192.168.1.254

```null
# ifconfig eth4
eth4      Link encap:Ethernet  HWaddr 00:E0:70:2A:3F:59  
          inet addr:192.168.1.254  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:98646352 errors:0 dropped:119900 overruns:0 frame:0
          TX packets:289134781 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:47923955741 (44.6 GiB)  TX bytes:281272600802 (261.9 GiB)
```

跟踪一下路由看看。

```null
# traceroute 192.168.1.1
traceroute to 192.168.1.1 (192.168.1.1), 30 hops max, 46 byte packets
 1  192.168.1.1 (192.168.1.1)  0.831 ms  0.762 ms  0.671 ms
```

可以了耶。ping 一下看看

```null
# ping 192.168.1.1 -c 4
PING 192.168.1.1 (192.168.1.1): 56 data bytes
64 bytes from 192.168.1.1: seq=0 ttl=64 time=1.124 ms
64 bytes from 192.168.1.1: seq=1 ttl=64 time=0.941 ms
64 bytes from 192.168.1.1: seq=2 ttl=64 time=0.941 ms
64 bytes from 192.168.1.1: seq=3 ttl=64 time=0.934 ms

--- 192.168.1.1 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 0.934/0.985/1.124 ms
```

使用浏览器访问 [http://192.168.1.1](http://192.168.1.1/) 嗯，可以访问啦！这样配置的目的就是方便了桥接光猫的用户更便捷的管理/登录 光猫的配置管理系统，查看配置也是极其方便的~~~

Reference
---------

[https://www.right.com.cn/forum/thread-400002-1-1.html](https://www.right.com.cn/forum/thread-400002-1-1.html)

后记
--

因为从 wan 到光猫的线路只有一个目的地址，目标只是一台主机，而不是一个网络，所以理论上 tomodem 接口的 ipv4 不需要设置成 `192.168.1.x` 这个网段的，掩码也不需要填写，设置静态路由的时候，只需要在网关那里设置成 tomodem 的 ipv4 地址即可。

比如 tomodem 接口地址设置成 `172.16.90.1`，然后不设置掩码，关键的步骤在创建静态路由时，目标对象设置成 `192.168.1.1`，然后 ipv4 网关设置为 `172.16.90.1`，最后重启网络应该也是可行的~

end.