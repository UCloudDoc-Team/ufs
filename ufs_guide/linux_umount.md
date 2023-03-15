# 卸载文件系统(Linux)

## NFS

### 步骤一、查看挂载信息

1. 在linux云主机上使用`df -h`命令查看NFS文件系统挂载情况，如下图所示。  
![](/images/umount/linux_umount1.png)


### 步骤二、卸载文件系统

1. 使用以下命令卸载NFS文件系统。

        umount /data
    
    请根据实际挂载的文件路径替换实例中的/data路径。

## SMB

### 步骤一、查看挂载信息

1. 在linux云主机上使用`df -h`命令查看NFS文件系统挂载情况，如下图所示。 
![](/images/umount/linux_umount2.png)

### 步骤二、卸载文件系统

1. 使用以下命令卸载NFS文件系统。

        umount /media
    
    请根据实际挂载的文件路径替换实例中的/media路径。