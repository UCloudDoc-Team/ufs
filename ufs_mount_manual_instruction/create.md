# 创建文件系统

{{indexmenu_n>1}}

本章目的在于指导初次使用的用户如何快速上手使用文件存储。

#### Step 1. 选择具有文件存储资源的地域

**\[注\]目前文件存储UFS已在北京二、上海二、广州地域部署。**

![](/images/area.png)

#### Step 2. 选择文件存储UFS服务

![](/images/choose_ufs.jpg)

#### Step 3. 点击<创建文件系统>按钮创建文件存储。

**\[注\]每个账户最多可以创建5个文件系统。** ![](/storage_cdn/ufs/create_ufs.jpg)

#### Step 4.

每个文件系统会对应一个全局唯一的实例 ID(以ufs-为前缀的一个字符串),用户通过控制台创建文件系统实例,如下图:  
创建文件系统实例时的选项有:  
  * 选择文件系统类型为容量型 or 性能型

  * 选择需要使用的协议,包括 NFSv3/NFSv4，但目前 NFSv3 只支持容量型，NFSv4
    则只支持性能型，请选择适合业务的协议类型。

**\[注\]需要注意的是，目前 UFS 实现的 NFSv3 协议并不支持 lock 功能。**

![](/images/ufs_mount_manual_instruction/create_ufs2.png)

#### Step 5. 创建文件系统完成后，继续设置挂载点

详细添加挂载点方法请参考[添加挂载点](/storage_cdn/ufs/ufs_mount_manual_instruction/add_mount)
![](/images/confirm_ufs.jpg)

#### Step 6. 不继续设置挂载点，展示创建成功后的文件列表

![](/images/ufs_mount_manual_instruction/create_success.png)
