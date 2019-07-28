# FAQ

{{indexmenu_n>10}}

#### 每个账户可以创建多少个文件系统(UFS)? 

目前每个账号最大支持创建**5个**UCloud File System (UFS)系统。

#### 文件系统(UFS)最大容量是多少？

目前每个UCloud File System (UFS)系统，最大支持容量20T。

#### 文件系统(UFS)可跨地域访问吗？ 

不支持。目前UCloud File System(UFS)只支持跨可用区的访问。后续我们会持续关注与评估此需求。

#### 文件系统(UFS)在哪些区域可以使用？

目前UCloud File System (UFS)系统，开放了 **北京二** 。

#### 文件系统(UFS)适合什么应用场景？

  - 同一区域内高可用部署场景，用于共享存储动态文件与日志等。例如：web站点服务。
  - 需要在各种应用间，大量文本类元数据共享的场景。
  - 企业部门内，内容共享与管理场景。例如：工作文档共享。

#### 使用文件系统(UFS)，有什么需要注意的吗？ 

**有**。删除文件系统(UFS)前，您必须卸载UHost主机上的挂载分区。若未卸载会影响UHost主机使用。

#### Windows Server挂载文件系统(UFS)后没有操作权限？ 

具体报错截图如下（此处错误信息为创建文件时没有权限）：
![](/images/error_img.png) 使用命令行展示挂载点信息：
![](/images/show_mount.png)

此处在文件系统属性中的 UID, GID 数值错误；正确值应为 UID=0, GID=0。 解决办法如下：  
1\.
打开注册表找到：KEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\ClientForNFS\\CurrentVersion\\Default  
![](/images/regedit.png)

2\. 给其中增加两项：AnonymousUid，AnonymousGid
![](/images/regedit_add.png)

3\. 重启Windows Server后重新挂载文件系统即可 ![](/storage_cdn/ufs/success.png)
