---
title: 网络存储系统 NFS
date: 2023-01-31 17:44:56
tags:
cover: https://cdn.staticaly.com/gh/van-chin/pictures@main/van-chin-inkStorage-By-NFS.png
---

![](https://cdn.staticaly.com/gh/van-chin/pictures@main/van-chin-inkStorage-By-NFS.png)



### 简介

NFS 是Network File System的简称，是由SUN公司研制的UNIX表示层协议(presentation layer protocol)，能使使用者访问网络上别处的文件就像在使用自己的计算机一样。



作为一个经典的网络存储系统，NFS 有着近 40 年的发展历史，基本上已经成为了各种 UNIX 系统的标准配置，Linux 自然也提供对它的支持。



NFS 采用的是 Client/Server 架构，需要选定一台主机作为 Server，安装 NFS 服务端；其他要使用存储的主机作为 Client，安装 NFS 客户端工具。



### 安装

我们在 **Debain 11** 系统环境下安装及使用NFS。

#### NFS-Server

```bash
# 更新软件源，保证安装版本的软件包
sudo apt-get update


# 安装 nfs-kernel-server
sudo apt-get install nfs-kernel-server 
```

安装好之后，需要给 NFS 指定一个存储位置，也就是**网络共享目录**。一般来说，应该建立一个专门的 `path/to/data` 目录，本文使用 `/data/nfs/tests` 为网络共享目录。

```bash
sudo mkdir -p /data/nfs/tests
```

然后，需要修改NFS Server 的配置文件 `/etc/exports` 指定目录名、允许访问的网段，还有权限等参数。

```bash
nano /etc/exports


# 增加 如下配置

/data/nfs/tests *(rw,sync,no_subtree_check,no_root_squash,insecure)
```



#### NFS-Client



配置好NFS Server之后，需要安装 `nfs-common` 做为客户端使用NFS服务端提供的服务。

```bash
sudo apt-get install nfs-common
```

只需要简单安装即可，无需额外的配置。