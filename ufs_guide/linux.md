{{indexmenu_n>1}}

# Linux平台

UFS的容量型支持NFSv3.0协议，SSD性能型支持NFSv4.0协议。  
目前容量型产品和SSD性能型产品在UHost上挂载UFS系统存在细微的差别,下面分别演示实际操作。

## Redhat/Centos操作系统

### 容量型：

#### Step 1. 安装NFS client。

    # yum -y install nfs-utils

#### Step 2. UHost主机挂载, \<ip\>与\<file\_space\>请使用挂载信息中挂载地址的IP与文件系统ID替换。

////

    # mount -t nfs -o nolock,vers=3,tcp <ip>:/<file_space> /mnt

#### 参考例子：

![](/images/ufs_guide/linux_type_sata.png) 以上述实例为例,在 Linux
CentOS 上挂载方式为:

    # yum install -y nfs-utils
    # mount -t nfs -o nolock,vers=3,tcp 10.19.255.192:/ufs-v1mmpi /mnt

挂载成功后即可在 /mnt 目录下访问该文件系统数据。

### SSD性能型：

#### Step 1. 安装NFS client。

    # yum -y install nfs-utils

#### Step 2. UHost主机挂载, \<ip\>请使用挂载信息中挂载地址的IP替换。

////

    # mount -t nfs -o vers=4.0,tcp <ip>:/ /mnt

#### 参考例子：

![](/images/ufs_guide/linux_ufs_ssd.png)

以上述实例为例,在 Linux CentOS 上挂载方式为:

``` 
# yum install -y nfs-utils
# mount -t nfs -o vers=4.0,tcp 10.10.27.183:/ /mnt

```

<WRAP center round important 60%>

注：SSD性能型文件系统的挂载点地址不需要包含文件系统ID为后缀,这是和容量型挂载的区别。 </WRAP>

## Ubuntu/Debian操作系统

## 容量型：

#### Step 1. 安装NFS client。

    $ sudo apt-get install nfs-common

#### Step 2. UHost主机挂载, \<ip\>与\<file\_space\>请使用挂载信息中挂载地址的IP与文件系统ID替换。

    $ sudo mount -t nfs -o nolock <ip>:/<file_space> /mnt

#### 参考例子：

![](/images/ufs_guide/linux_type_sata.png) 以上述实例为例,在 Linux
CentOS 上挂载方式为:

    # sudo apt-get install nfs-common
    # mount -t nfs -o nolock,vers=3,tcp 10.19.255.192:/ufs-v1mmpi /mnt

挂载成功后即可在 /mnt 目录下访问该文件系统数据。

## SSD性能型：

#### Step 1. 安装NFS client。

    $ sudo apt-get install nfs-common

#### Step 2. UHost主机挂载, \<ip\>请使用挂载信息中挂载地址的IP替换。

    $ sudo mount -t nfs -o nolock <ip>:/ /mnt

#### 参考例子：

![](/images/ufs_guide/linux_ufs_ssd.png)

以上述实例为例,在 Linux CentOS 上挂载方式为:

``` 
# sudo apt-get install nfs-common
# mount -t nfs -o vers=4.0,tcp 10.10.27.183:/ /mnt

```

<WRAP center round important 60%>

注：SSD性能型文件系统的挂载点地址不需要包含文件系统ID为后缀,这是和容量型挂载的区别。 </WRAP>
