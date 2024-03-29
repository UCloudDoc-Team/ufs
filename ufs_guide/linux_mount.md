# 挂载文件系统(Linux)

## NFS

### 步骤一、安装 NFS 客户端

1. 在安装 NFS 客户端之前，请先根据[Linux NFS 客户端内核缺陷](/ufs/faq?id=linux-nfs-客户端内核缺陷)一节中的信息，确认使用建议的内核版本，否则主机可能会发生 IO 卡死的现象。

    如果是 CentOS 系统的主机，请执行以下命令安装 NFS 客户端：

        sudo yum install nfs-utils

    如果是 Ubuntu 系统的主机，请执行以下命令安装 NFS 客户端：

        sudo apt-get install nfs-common

2. 由于 NFS 客户端默认对同时能够发起的 NFS 请求数进行了限制，默认允许的并发请求数为 2，对于性能影响较大，可以参考[如何修改 NFS 并发请求数](/ufs/faq?id=如何修改-nfs-请求并发数？)一节进行修改，以提升性能。

### 步骤二、挂载文件系统
1. 请您根据『管理挂载点』操作中显示的挂载点信息进行操作。下面以文件系统 ID 为 ufs-dh6tds 的文件系统为例展示挂载操作，假设其挂载点 IP 为 10.8.0.1(实际操作时请用您要使用的文件系统 ID 和挂载点 IP 替代示例中的相关参数)。

    nfsv3协议执行以下命令进行挂载

        sudo mount -t nfs -o rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport,nfsvers=3,proto=tcp,mountproto=tcp,nolock,noacl 10.8.0.1:/ /mnt

    nfsv4协议执行以下命令进行挂载

        sudo mount -t nfs -o rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 10.8.0.1:/ /mnt

#### 挂载命令中各参数含义介绍如下：

|参数/选项名称          |作用描述     |
|---------|-----------------------------------------------------------------|
|挂载点	|访问文件系统的入口，UFS 挂载点由一个 IPv4 地址表示。|
|rsize,wsize	|用于指定在和文件存储服务端交互数据时的数据块大小(单位Byte)，建议设置为 1048576。|
|hard	|指示 NFS 客户端在远端文件存储临时不可服务时，继续向远端进行操作重试，而不是返回错误给上层应用，建议开启该选项，对于一些运行时间长、中断操作成本高的任务能够提升其对网络等方面临时故障的容错性。|
|timeo	|NFS 客户端在等待向远端文件存储重试请求前等待的时间，单位是 0.1 秒，建议设置值为 600。|
|retrans	|NFS 客户端对一次请求重试的次数，建议设置为 2。|
|noresvport	|在网络中断重连时使用新端口，可以降低重连失败的概率，建议开启。|

### 步骤三、查看挂载结果
1. 挂载命令执行完成后，可以通过执行 mount -l 或者 nfsstat -m 列出当前挂载的文件系统列表，如果有包含需要挂载的文件系统则表示挂载成功。

### 步骤四、设置自动挂载
1. 我们可以通过在 Linux 系统中配置 /etc/fstab 文件的方式来实现 NFS 文件系统的自动挂载。
    v4协议自动挂载

        10.8.0.1:/ /mnt nfs rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0

    v3协议自动挂载

        10.8.0.1:/ /mnt nfs rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,nfsvers=3,proto=tcp,mountproto=tcp,nolock,noacl,_netdev,noresvport 0 0

#### 命令中各参数含义介绍如下：
|参数/选项名称          |含义描述     |
|---------|-----------------------------------------------------------------|
|_netdev	|表示待挂载的文件系统是网络文件系统，防止在网络未准备好之前进行挂载操作导致主机启动卡死。|
|0(noresvport后第一项)	|非 0 值表示文件系统应由 dump 备份，对于 NAS 服务来说该项为 0。|
|0(noresvport后第二项)	|表示在开机后是否执行 fsck 操作，由于 UFS 产品由服务端保证数据的持久化和一致性，该选项无须打开。|


## SMB

### 步骤一、安装 CIFS 客户端

1. 在安装 CIFS 客户端之前，请先根据[Linux CIFS 客户端内核缺陷](/ufs/faq?id=linux-smb-客户端内核缺陷)一节中的信息，确认使用建议的内核版本，否则主机可能会发生 IO 卡死的现象。

    如果是 CentOS 系统的主机，请执行以下命令安装 CIFS 客户端：

        sudo yum install cifs-utils

    如果是 Ubuntu 系统的主机，请执行以下命令安装 CIFS 客户端：

        sudo apt-get install cifs-utils

### 步骤二、挂载文件系统
1. 请您根据『管理挂载点』操作中显示的挂载点信息进行操作。下面以文件系统 ID 为 ufs-dh6tds 的文件系统为例展示挂载操作，假设其挂载点 IP 为 10.8.0.1(实际操作时请用您要使用的文件系统 ID 和挂载点 IP 替代示例中的相关参数)。

        sudo mount -t cifs  -o guest,uid=0,gid=0,rsize=1048576,wsize=1048576 //10.8.0.1/share /mnt

#### 挂载命令中各参数含义介绍如下：

|参数/选项名称          |作用描述     |
|---------|-----------------------------------------------------------------|
|guest |只支持基于ntlm认证协议的客户端挂载 |
|rsize,wsize	|用于指定在和文件存储服务端交互数据时的数据块大小(单位Byte)，建议设置为 1048576。|
|uid	|挂载成功后，文件所属的用户。如果未设置uid，则默认uid=0。|
|gid	|挂载成功后，文件所属的用户组。如果未设置gid，则默认gid=0。|

### 步骤三、查看挂载结果
1. 挂载命令执行完成后，可以通过执行 mount -l 列出当前挂载的文件系统列表，如果有包含需要挂载的文件系统则表示挂载成功。

### 步骤四、设置自动挂载
1. 我们可以通过在 Linux 系统中配置 /etc/fstab 文件的方式来实现 SMB 文件系统的自动挂载。

        //10.8.0.1/share /mnt cifs guest,uid=0,gid=0,rsize=1048576,wsize=1048576 0 0

<br/>