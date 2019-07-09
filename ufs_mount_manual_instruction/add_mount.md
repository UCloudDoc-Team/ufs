# 添加挂载点

{{indexmenu_n>2}}

创建文件系统完成后，需要为文件系统添加挂载点，用于云主机（或物理云主机、私有专区）挂载文件系统。

挂载点方式支持VPC2.0。

#### Step 1. 在文件系统列表中点击对应的文件系统\<添加挂载点\>按钮。

![](/images/ufs_mount_manual_instruction/new_add_mount.png)

#### Step 2. 在设置挂载点弹出框中，输入挂载点名称。

**\[注\] 请输入长度为6\~63位名称，只能包含字母数字和 - \_ 且 - 不能作为第一个字符**
![](/images/ufs_mount_manual_instruction/new_add_mount_name.png)

#### Step 3. 在设置挂载点弹出框中，选择云主机（或物理云主机、私有专区）所在的VPC网络和子网。

![](/images/ufs_mount_manual_instruction/new_add_mount_vpc.png)

#### Step 4. 点击\<确认\>，挂载成功，可以在文件系统列表查看挂载点数目

**\[注\] 目前最多只能添加5个挂载点**
![](/images/ufs_mount_manual_instruction/new_add_mount_confirm.png)
![](/images/ufs_mount_manual_instruction/new_add_mount_number.png)

#### Step 5. 选择\<管理挂载\>，可以在挂载信息列表查看挂载点详情

![](/images/ufs_mount_manual_instruction/new_add_mount_manage.png)
![](/images/ufs_mount_manual_instruction/new_add_mount_list.png)

#### Step 6. 完成添加挂载点后，请通过挂载点将云主机（或物理云主机、私有专区）挂载至文件系统

详细挂载方法请参考[操作指南](/storage_cdn/ufs/ufs_guide)
