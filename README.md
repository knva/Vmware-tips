# Vmware-tips

## 1:ubuntu安装tools后,无法进行虚拟机内外的复制粘贴 
```
    需要使用最新版本虚拟机. 
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
    sudo apt-get install g++-multilib
    sudo apt-get install libncurses5:i386
    sudo apt-get install libc6:i386 libgcc1:i386 gcc-4.6-base:i386 libstdc++5:i386 libstdc++6:i386
```

## 4:文件权限修改
```
    新版本ubuntu 禁止使用root用户登录到界面中,所以大部分文件夹管理员用户操作需要使用sudo命令操作.
    如文件只读,可以使用sudo chown 用户名 文件名 进行修改所有者
    如文件运行权限不足,可以使用sudo chmod 777 文件名 进行权限修改
```
