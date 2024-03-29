

# 产品概述

文件存储 (UFS) 是一款分布式文件系统产品，它能够为运行于 UCloud 公有云、物理云、托管云上的各类主机提供高可用、高可靠、易拓展的文件存储功能。通过 UFS 产品提供的共享存储功能，可以方便地为各类数据备份、serverless、AI 数据分析、高性能 web 站点等应用场景提供强有力的支撑。

文件存储产品分为两种类型：容量型、性能型。容量型文件存储使用普通 SATA 介质，具有低价格、高容量的特点。性能型文件存储使用 SSD 介质，提供低延迟的 IO 访问。

文件存储产品采用可用区内多副本机制，并保证跨机柜物理机容灾，数据持久性为 99.999999%。目前支持基于 TCP 的 NFS和SMB 协议。单文件系统容量可达百 PB 级别并支持在线扩容，业务对于扩容无感知，具体限制请见[产品限制](/ufs/ufs_manual_instruction/limit)一节。

文件存储产品在传输层基于 VPC 虚拟网络设计，保证数据在网络传输中的安全可靠。

