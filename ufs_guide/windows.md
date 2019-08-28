{{indexmenu_n>4}}

# 挂载文件系统(Windows)

由于当前文件存储 (UFS) 还未支持 SMB 协议，需要在 Windows 上使用文件存储的用户需要使用 NFS 协议。需要注意的是 Windows 上的 NFS 客户端默认只支持 NFSv3(第三方商业软件支持 NFSv4)，所以在 Windows 上目前默认只能使用文件存储容量型产品。

推荐使用的系统版本是 Windows 2012 及以上版本，低于该版本的系统对吞吐支持不够(Windows 2008 最大支持的rsize/wsize 仅为 32KB)。

#### 步骤一、准备 NFS 服务
在『Server Manager』中点击『Add roles and features』进入到 特性安装页面。

![](/images/windows1.png)

在『Features』标签下勾选 『Client For NFS』特性，点击下一步进行安装。

![](/images/windows2.png)
![](/images/windows3.png)

#### 步骤二、挂载文件系统
下面以挂载点地址为 10.19.255.192:/ufs-tfpexm 为例展示文件系统挂载命令，实际操作时请用您要使用的文件系统的挂载点信息替代示例中的相关参数。

首先打开终端(cmd),执行如下命令:

    mount -o sec=sys -o nolock 10.19.255.192:/ufs-tfpexm z:

![](/images/windows4.png)

挂载成功后终端会给出提示。

#### 步骤三、调整客户端参数
首先执行 mount 命令查看 rsize、wsize 是否已经默认设置为 1048576，低于该值将影响客户端的 IO 吞吐。

![](/images/windows5.png)

由于默认挂载后 UID、GID=-2，此时如果向文件系统内进行写入、创建目录等操作将被拒绝，如下图：

![](/images/windows6.png)

请按照 [FAQ](https://docs.ucloud.cn/storage_cdn/ufs/faq)中『Windows 系统挂载后无法写入数据』一节进行设置，以获取写入权限。

