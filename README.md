# cobbler服务器端环境说明:
系统：CentOS6

本实验环境为vmware虚拟机

网卡设为nat模式

# cobbler server install guide:
`mkdir /usr/src/cobbler`<br>
`git clone https://github.com/chendao2015/cobbler.git`<br>
`cd cobbler`<br>
`tar xf cobbler.tar.bz2 -C /usr/src/cobbler/`<br>
`chmod +x cobbler.sh`<br>
`./cobbler.sh`<br>

## 导入ISO文件
把要安装的操作系统的iso上传到/usr/src目录下，或者直接挂载到光驱中，假设这里是安装ubuntu12.04<br>

`mount -o loop /usr/src/ubuntu_12.04_server_x64.iso /mnt`<br>
`cobbler import --path=/mnt/ --name=ubuntu12.04 --arch=x86_64`<br>
`cobbler sync`<br>
`cobbler list`<br>
