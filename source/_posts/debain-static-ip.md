---
title: Debain 系统配置
date: 2023-01-28 14:32:56
tags:
---



## 常用配置


### 网络设置

编辑配置文件 `/etc/network/interfaces`

``` bash


# nano 打开配置文件
nano /etc/network/interfaces

# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug ens33

# 设置为 static, dhcp 动态获取
iface ens33 inet static
# 静态IP地址
address 192.168.227.180
# 子网掩码
netmask 255.255.255.0
# 网关
gateway 192.168.227.2


```



### 主机名配置

``` bash 

# 设置主机名为 k8s-cm-master-01
hostnamectl set-hostname k8s-cm-master-01 
# 查看 设备后的 hostname
hostname

```