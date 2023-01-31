---
title: Kubernetes 安装
date: 2023-01-28 15:02:12
tags:
---

## 目标

本文介绍一下k8s 的裸机安装（Bare Metal），操作环境为 VMware® Workstation 下的虚拟机 Debain 11 系统
目标是在三台Debain 11 服务器上安装一个最小化的Kubernetes 集群

| 主机名              | 作用       | IP              |     |     |
|:----------------:|:--------:|:---------------:| --- | --- |
| k8s-cm-master-01 | master节点 | 192.168.227.180 |     |     |
| k8s-cm-worker-01 | 工作节点1    | 192.168.227.183 |     |     |
| k8s-cm-worker-02 | 工作节点2    | 192.168.227.184 |     |     |

## 准备工作

### 服务器通用配置

- 设置主机名

- 设置静态IP

- 禁用交换分区

#### 修改主机名

```bash
# 设置主机名 k8s-cm-master-01
hostnamectl set-hostname k8s-cm-master-01

# 设置主机名 k8s-cm-worker-01
hostnamectl set-hostname k8s-cm-worker-01

# 设置主机名 k8s-cm-worker-02
hostnamectl set-hostname k8s-cm-worker-02
# 查看 当前主机名
hostname
```

#### 设置静态IP

```bash
# 设置master节点的IP 为 192.168.227.180
nano /etc/network/interfaces

# 设置为 static, dhcp 动态获取
iface ens33 inet static
# 静态IP地址
address 192.168.227.180
# 子网掩码
netmask 255.255.255.0
# 网关
gateway 192.168.227.2


# 设置worker-01节点的IP 为 192.168.227.183

# 设置worker-02节点的IP 为 192.168.227.184
```

#### 修改hosts 文件



```bash

nano /etc/hosts
# 三台服务器 hosts 文件中增加同样的配置
192.168.227.180  k8s-cm-master-01
192.168.227.183  k8s-cm-worker-01
192.168.227.184  k8s-cm-worker-02
```

#### 禁用交换分区

```bash
# 临时禁用 swap
swapoff -a 
# 禁用 swap 重启后生效
sed -i 's/.*swap.*/#&/' /etc/fstab


```



```bash

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables=1
net.bridge.bridge-nf-call-ip6tables=1
net.ipv4.ip_forward=1
EOF
————————————————
版权声明：本文为CSDN博主「大能嘚吧嘚」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_30818545/article/details/127036230



kubeadm join 192.168.227.180:6443 --token j2nn1t.t6708xt4gwhrw80s \
        --discovery-token-ca-cert-hash sha256:513e71d412614fb56c351993abaafc747fc7279d0e3903ebf0a9649bd5f26c2dysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables=1
net.bridge.bridge-nf-call-ip6tables=1
net.ipv4.ip_forward=1
EOF




mkdir -p /etc/containerd 

containerd config default > /etc/containerd/config.toml









sudo kubeadm init \
    --kubernetes-version v1.26.0 \
    --image-repository registry.aliyuncs.com/google_containers \
    --apiserver-advertise-address 192.168.227.180 \
    --service-cidr 10.245.0.0/12 \
    --pod-network-cidr 10.244.0.0/16


kubeadm join 192.168.227.180:6443 --token j2nn1t.t6708xt4gwhrw80s \
        --discovery-token-ca-cert-hash sha256:513e71d412614fb56c351993abaafc747fc7279d0e3903ebf0a9649bd5f26c2d



```
