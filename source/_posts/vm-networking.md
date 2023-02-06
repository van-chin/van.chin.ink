---
title: 虚拟机组网
date: 2023-02-06 16:49:22
tags:
cover: https://cdn.staticaly.com/gh/van-chin/pictures@main/van-chin-inkvm-networking-tp.png
---

![](https://cdn.staticaly.com/gh/van-chin/pictures@main/van-chin-ink%E7%BD%91%E7%BB%9C-%E7%AE%80%E5%9B%BE-%E5%AF%BC%E5%87%BA.png)



#### 虚拟机网络简述

在VMware虚拟机网络配置中有三种模式

- 桥接模式

- NAT模式

- 仅主机模式

![](https://cdn.staticaly.com/gh/van-chin/pictures@main/van-chin-inkSnipaste_2023-02-06_17-04-24.png)

使用NAT模式，可以和宿主机通信且虚拟机里能连接外网，仅主机模式能和宿主机通信但不能直接连接外网。本文提供一种思路让仅主机模式下的虚拟机也能连接外网。



#### 网络规划

利用`NAT模式` 和 `仅主机模式` 各自的特性，我们用一台虚拟机做路由器，里面配置一张仅主机模式的网卡做网关，另一张用NAT模式负责连通外网。

![](https://cdn.staticaly.com/gh/van-chin/pictures@main/van-chin-inkvm-networking-tp.png)

*`网络-拓扑-简图`*

#### 实操演示

下面我们通过几台虚拟机去实现一下上面我们的网络规划



##### 路由器-安装

xxxxxxxxx

- 桥接模式

- NAT模式

- 仅主机模式

- 桥接模式

- NAT模式

- 仅主机模式

- 桥接模式

- NAT模式

- 仅主机模式

##### DeepIn-安装

测试机我们安装一台deepin系统的虚拟机来进行测试

- 桥接模式

- NAT模式

- 仅主机模式桥接模式

- NAT模式

- 仅主机模式

##### 测试结果



xxxx

- 桥接模式

- NAT模式

- 仅主机模式

- 桥接模式

- NAT模式

- 仅主机模式

- 桥接模式

- NAT模式

- 仅主机模式

- 桥接模式

- NAT模式

- 仅主机模式
