{{indexmenu_n>2}}

# Windows平台

nfs客户端建议使用windows 2012及其以上：

<WRAP center round important 60%> 注：SSD性能型不支持windows平台。 </WRAP>

#### Step 1. 打开服务器管理器，选择添加角色。

![](/images/mount.png)

#### Step 2. 选择文件服务。

![](/images/file_service_windows.png)

#### Step 3. 选择网络文件系统，进行安装。

![](/images/nfs.png)

#### Step 4. 打开命令行工具执行挂载命令, <ip>与<file_space>请使用挂载信息列表中挂载地址的IP与文件系统ID替换。

*\[注\]由于部分windows主机命令行存在差异,请尝试以下2条命令。*

``` 
mount -o sec=sys,nolock <ip>:/<file_space> z:    
mount -o sec=sys –o nolock <ip>:/<file_space> z:   
```

#### 参考例子：

![](/images/ufs_guide/windows_sample.png) 以上述实例为例,执行到Step 4.
打开命令行工具执行挂载命令为:

``` 
mount -o sec=sys,nolock 10.19.255.192:/ufs-v1mmpi z:    
mount -o sec=sys –o nolock 10.19.255.192:/ufs-v1mmpi z:   
```

连接成功后展示：

![](/images/ufs_guide/windows_ufs.png)
