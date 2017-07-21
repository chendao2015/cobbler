# cobbler服务器端环境说明:
系统：CentOS6迷你安装

本实验环境为vmware虚拟机

网卡设为nat模式

## 开始前，先关闭防火墙和SELINUX
`systemctl stop firewalld.service`<br>
`systemctl disable firewalld.service`<br>
`sed -i 's/SELINUX=.*/SELINUX=disabled/' /etc/sysconfig/selinux`<br>
`sed -i 's/SELINUX=.*/SELINUX=disabled/' /etc/selinux/config`<br>
`reboot`<br>

# cobbler server install guide:
`yum -y install git bzip2`<br>
`cd /usr/src`<br>
`git clone https://github.com/chendao2015/cobbler.git`<br>
`cd cobbler`<br>
`tar xf cobbler.tar.bz2`<br>
`chmod +x cobbler*.sh`<br>
`./cobbler.sh`<br>
`./cobbler_check.sh`<br>

## 导入ISO文件
把要安装的操作系统的iso上传到/usr/src目录下，或者直接挂载到光驱中

### 安装ubuntu12.04
`mount -o loop /usr/src/ubuntu_12.04_server_x64.iso /mnt`<br>
`cobbler import --path=/mnt/ --name=ubuntu12.04 --arch=x86_64`<br>
`cobbler sync`<br>
`cobbler list`<br>

### 安装CentOS6
将CentOS6的安装光盘插入光驱中，然后执行以下命令：

`mount -r /dev/cdrom /mnt`<br>
`cobbler import --path=/mnt/ --name=CentOS6 --arch=x86_64`<br>
`cobbler sync`<br>
`cobbler list`<br>

### 安装CentOS7
将CentOS7的安装光盘插入光驱中，然后执行以下命令：

`mount -r /dev/cdrom /mnt`<br>
`cobbler import --path=/mnt/ --name=CentOS7 --arch=x86_64`<br>
`cobbler sync`<br>
`cobbler list`<br>
