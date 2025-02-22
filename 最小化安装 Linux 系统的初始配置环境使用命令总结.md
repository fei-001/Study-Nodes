# 最小化安装 Linux 系统的初始配置环境使用命令总结

1. **重启 Linux 系统命令**

- - reboot

- - init 6

- - shutdown -r now

1. **关闭 Linux 系统命令**

- - poweroff

- - init 0

- - shutdown -h now

- - halt -p

1. **重启网络或网卡服务（使配置的网络参数生效）**

- - systemctl restart network.service

- - 或

- - ifdown ens33 （禁用或关闭网卡）

- - ifup ens33 （开启或启用网卡）

- - 或

- - ifconfig down ens33 （禁用或关闭网卡）

- - ifconfig up ens33 （启用或开启网卡）

- - **备注**：网络参数 ——ip 地址、子网掩码、默认网关、DNS 服务器地址

1. **永久配置网卡或网络参数**

```
BOOTPROTO=static      设置网卡使用的协议（静态static/动态dhcp）
ONBOOT=yes            开机启动网卡服务
IPADDR=192.168.50.12  设置网卡的IP地址
NETMASK=255.255.255.0 设置子网掩码
GATEWAY=192.168.50.2  设置默认的网关地址
DNS1=192.168.50.2     设置DNS服务器地址 
DNS2=114.114.114.114  设置DNS服务器地址2
```

- - 网卡对应的配置文件：vim /etc/sysconfig/network-scripts/ifcfg-ens33

1. **查看 Linux 系统已安装的 rpm 的总个数**

- - rpm -qa | wc -l

1. **创建挂载点目录 /media/cdrom 并挂载光盘**

- - mkdir /media/cdrom （创建挂载点目录）

- - mount /dev/cdrom /media/cdrom （挂载光盘）

1. **使用 YUM 命令安装 rpm 包 (初始化系统所需的开发工具包)**

- - yum -y install gcc make autoconf gcc-c++ glibc glibc-devel pcre pcre-devel openssl openssl-devel systemd-devel zlib-devel vim lrzsz tree lsof tcpdump net-tools bc bzip2 zip unzip nfs-utils man-pages apr* redhat-rpm-config bash-completion chrony wget psmisc yum-utils

1. **Linux 系统防火墙管理**

- - **关闭防火墙服务**：systemctl stop firewalld.service

- - **开机禁用防火墙服务**：systemctl disable firewalld.service

- - **查看防火墙的服务运行状态**：systemctl status firewalld.service

1. **Linux 内核安全机制管理**

- - **临时禁用内核安全机制**：setenforce 0

- - **永久禁用内核安全机制（必须重启系统才能生效）**：

- - - 编辑配置文件：vim /etc/sysconfig/selinux

- - - 将SELINUX=enforcing改为SELINUX=disabled

- - **查看 Linux 内核安全机制运行状态**：getenforce 

1. **查看 Linux 系统主机名**

- - hostname

1. **设置主机名称**

- - **临时设置主机名称**：hostname node01

- - **永久主机名称**：

- - - **A. 通过命令实现**：hostnamectl set-hostname node01

- - - **B. 修改主机名对应的配置文件（重启系统才能生效）**：

- - - - 编辑文件：vim /etc/hostname

- - - - 写入主机名：node02

1. **查看 Linux 系统的内核版本**

- - uname -r

- - uname -a

1. **查看 Linux 系统属性信息**

- - hostnamectl

## 学习 Linux 系统的宗旨

- 一切皆文件！！！

- 先跑通，再变通！！！（先做出来，再深入理解，采用逆向思维的学习方法。通过执行结果倒推理论 -- 实践是检验真理的唯一标准）