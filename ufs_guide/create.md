

# 创建文件系统

#### 步骤一、进入文件存储 UFS 产品

![](/images/create1.png)

#### 步骤二、在控制台页面选择创建文件存储的目标地域和项目组

目前文件存储在各地域的支持详情请参见[产品限制](/ufs/ufs_manual_instruction/limit)章节或咨询技术支持。由于文件系统的访问是基于 VPC 的，并且目前在控制台上只允许选择和文件系统实例同一个项目组下的 VPC 进行访问，请您确定需要访问文件系统的主机所在项目组，并将文件系统实例创建在同项目中。若后续希望跨项目组的主机访问文件系统，可以通过在控制台上打通主机和文件系统挂载点所在的 VPC 来实现。

![](/images/create2.png)


#### 步骤三、创建文件系统

![](/images/create3new.png)

需要注意的是，目前 UFS 支持容量型、性能型两款产品，支持NFS和SMB两种协议类型，请您根据业务的使用场景选择合适的产品类型及协议类型，详情可参考[应用场景](/ufs/ufs_manual_instruction/application)和[产品限制](/ufs/ufs_manual_instruction/limit)章节。确认产品细节后点击『确定』并进行支付确认。

#### 步骤四、创建完成或进行挂载点设置

由于挂载点也可以通过后续的『挂载点管理』操作进行，所以在创建后也可以点击『以后设置』完成创建操作，需要保证挂载点选择的子网至少有三个可用ip。

![](/images/create4new.png)

#### 步骤五、创建完成后展示实例列表

![](/images/create5new.png)

