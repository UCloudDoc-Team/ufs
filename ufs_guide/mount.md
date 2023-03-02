

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

        10.8.0.1:/ /mnt nfs rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0

#### 命令中各参数含义介绍如下：
|参数/选项名称          |含义描述     |
|---------|-----------------------------------------------------------------|
|_netdev	|表示待挂载的文件系统是网络文件系统，防止在网络未准备好之前进行挂载操作导致主机启动卡死。|
|0(noresvport后第一项)	|非 0 值表示文件系统应由 dump 备份，对于 NAS 服务来说该项为 0。|
|0(noresvport后第二项)	|表示在开机后是否执行 fsck 操作，由于 UFS 产品由服务端保证数据的持久化和一致性，该选项无须打开。|


## SMB

TODO

<br/>

# 挂载文件系统(Windows)

## NFS

### 步骤一、安装NFS客户端  
1. 登录Windows云主机。
2. 点击左下角`开始`按钮，打开`服务器管理器`。  
    ![](/images/mount/windows_mount1.png)

3. 选择`添加角色和功能`。  
    ![](/images/mount/windows_mount2.png)

4. 根据提示安装NFS客户端。
    a.`开始之前`、`安装类型`、`服务器选择`保持默认选择，点击下一步即可。  
    b.在`服务器角色`选项卡中勾选`文件和存储服务->文件和iSCSI服务-> NFS服务器`，点击下一步。  
    c.在`功能`选项卡中勾选`NFS客户端`，点击下一步。  
    d.点击安装。  

5. 重启云主机。

6. 打开`命令提示符`窗口，输入命令`mount`，如果输出以下信息，则说明NFS客户端安装完成。  
    ![](/images/mount/windows_mount3.png)

<br/>

### 步骤二、挂载NFS文件系统  
1. 打开`命令提示符`窗口，输入以下命令挂载NFS文件系统。

        mount -o nolock -o mtype=hard -o timeout=10 \\mountpoint_ip\! Z:

    请根据控制台NFS文件系统挂载点信息的实际情况，替换命令中的mountpoint_ip，同时挂载到本地的盘符Z也可以根据实际需求替换。

2. 挂载成功后，再次执行`mount`命令检查挂载结果。  
    ![](/images/mount/windows_mount4.png)

    检查属性中`mount`类型是否为`hard`、`timeout`时间是否大于等于`10.0`、`locking`值是否为`no`。如果不是，说明挂载异常，请使用`umount Z:`(盘符根据实际情况修改)命令卸载文件系统，并参考上述步骤重新挂载。

3. 双击`此电脑`图标，查看共享文件系统。在共享文件系统中创建、删除文件\文件夹，确认能否正常使用。
    ![](/images/mount/windows_mount5.png)

<br/>

### 步骤三、设置自动挂载NFS文件系统  

1. 在云主机的`C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`目录下创建挂载脚本`auto_mount.bat`，脚本内容如下。

        mount -o nolock -o mtype=hard -o timeout=10 \\mountpoint_ip\! Z:

    请根据控制台NFS文件系统挂载点信息的实际情况，替换命令中的`mountpoint_ip`，同时挂载到本地的`盘符Z`也可以根据实际需求替换。

2. 创建挂载任务。  
    a.点击左下角`开始`按钮，打开`控制面板`。  
    ![](/images/mount/windows_mount6.png)

    b.点击`系统和安全`，并选择`计划任务`。  
    ![](/images/mount/windows_mount7.png)

    c.在操作选项卡点击`创建任务`。  
    在`常规`选项卡中，设置`名称`，并勾选`不管用户是否登录都要运行`(如果使用的系统是Windows Server 2016，则勾选`只在用户登录时运行`)，勾选`使用最高权限运行`。 
    ![](/images/mount/windows_mount8.png)

    在`触发器`选项卡中，点击`新建`，将`开始任务`设置为`登陆时`，并勾选`高级设置`里的`已启用`。  
    ![](/images/mount/windows_mount9.png)

    在`操作`选项卡中，点击`新建`，将`操作`设置为`启动程序`，在`程序或脚本`一栏选中步骤1创建的脚本`auto_mount.bat`，点击确定。  
    ![](/images/mount/windows_mount10.png)

    在`条件`选项卡中，勾选`只有在以下网络连接可用时才启动`，并在下拉选项中选择`任何连接`。  
    ![](/images/mount/windows_mount11.png)

    在`设置`选项卡中，取消勾选`允许按需运行任务`、`如果任务运行时间超过以下时间，停止任务`。勾选`如果请求后任务还在运行，强行将其停止`。在`如果此任务已经运行，以下规则适用`下拉框中选择`请勿启动新实例`。点击确定。
    ![](/images/mount/windows_mount12.png)

3. 重启云主机，验证结果。  
     a.查看计划任务状态，如果显示如下信息，则表示计划正常执行。  
     ![](/images/mount/windows_mount13.png)

     b.在`命令提示符`窗口执行`mount`命令，查看挂载信息。确认`mount`类型是否为`hard`、`locking`是否为`no`、`timeout`是否大于等于`10`。如果挂载正常，则参数应该如下图所示。  
    ![](/images/mount/windows_mount14.png)

## SMB

TODO