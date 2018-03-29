# Vmware-tips

## 1:ubuntu安装tools后,无法进行虚拟机内外的复制粘贴 
```
    需要使用最新版本虚拟机. 
    安装步骤：

1 更新下系统源

sudo apt update

2 安装open-vm-tools

sudo apt install open-vm-tools

3 如果要实现文件夹共享，需要安装 open-vm-tools-dkms

sudo apt install open-vm-tools-dkms

4 桌面环境还需要安装 open-vm-tools-desktop 以支持双向拖放文件

sudo apt install open-vm-tools-desktop

最后在虚拟机的设置→显示器里面开启 3D 加速。

在虚拟机设置里设置好共享文件夹，启动虚拟机后，如果Ubuntu中没有设置的共享文件。可以通过下面的两种方法解决：

1 可以使用vmhgfs-fuse命令，比如在虚拟机里有个目录 ~/share,终端中切换到家目录，然后：

vmhgfs-fuse share

此方法适合不是每次都使用共享文件的状况，可以编写一个脚本share.sh放到家目录

#!/bin/bash

vmhgfs-fuse share

2 如果要在开机是自动挂载共享文件夹，则需更改/etc/fstab文件。打开文件后在最后添加：

.host:/         /mnt/hgfs               fuse.vmhgfs-fuse allow_other,defaults   0       0
```
## 2:共享文件夹
```
    检查tools版本,需要使用当前虚拟机软件内的tools 工具,若只安装open-vm-tools ,可能导致无法使用共享文件夹
```
## 3:运行程序提示未找到
```
    使用 file 运行文件名  进行查看,如果其中带有 32bit 关键字,说明系统库版本不匹配.
    需要安装32位libc库,使用命令sudo apt install libc6:i386 安装32位libc库即可.
    更多32位库的安装(64位机上编译编译32位程序)
    sudo apt install g++-multilib
    sudo apt install libncurses5:i386
    sudo apt install libc6:i386 libgcc1:i386  libstdc++5:i386 libstdc++6:i386
    sudo apt install lib32z1
```

## 4:文件权限修改
```
    新版本ubuntu 禁止使用root用户登录到界面中,所以大部分文件夹管理员用户操作需要使用sudo命令操作.
    如文件只读,可以使用sudo chown 用户名 文件名 进行修改所有者
    如文件运行权限不足,可以使用sudo chmod 777 文件名 进行权限修改
```

## 5:powerpc linux sdk 从source安装交叉编译工具链的方法
```
    下载sdk source  然后挂载并安装
    按照文档说明进行安装
    所有操作需要使用user权限,不能使用root
    安装完成后使用$CC 命令进行编译hello world 测试.
```

## 6:iptables nat删除
```
首先使用这条命令查看当前nat表的防火墙规则：iptables -t nat -L -n --line-numbers，然后确定你要删除的是哪一条规则，并且看一下它是第几条规则，规则最前面有序号。接下来删除，使用命令：iptables -t nat -D PREROUTING 1，这里假如它的序号是1。
```
