# cobbler服务器端环境说明:
系统：CentOS7迷你安装

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
`chmod +x cobbler.sh`<br>
`./cobbler.sh`

## 导入ISO文件
把要安装的操作系统的iso上传到/usr/src目录下，或者直接挂载到光驱中

### 安装ubuntu12.04
`mount -o loop /usr/src/ubuntu_12.04_server_x64.iso /mnt`<br>
`cobbler import --path=/mnt/ --name=ubuntu12.04 --arch=x86_64`<br>
`cobbler sync`<br>
`cobbler list`<br>

### 安装CentOS7
将CentOS7的安装光盘插入光驱中，然后执行以下命令：

`mount -r /dev/cdrom /mnt`<br>
`cobbler import --path=/mnt/ --name=CentOS7 --arch=x86_64`<br>
`cobbler sync`<br>
`cobbler list`<br>

### 配置kickstart
`cp /usr/src/cobbler/*.cfg /var/lib/cobbler/kickstarts/`<br>
`cobbler profile edit --name=CentOS7-x86_64 --kickstart=/var/lib/cobbler/kickstarts/centos7.cfg`<br>
`sed -ri '/MENU TITLE/s/(MENU TITLE Cobbler).*/\1 \| QQ:1470044516/g' /etc/cobbler/pxe/pxedefault.template`<br>
`cobbler sync`<br>

### 根据客户端mac地址实现自动化安装
`cobbler system add --name=zabbix --mac=00:50:56:2E:88:1D --profile=centos7 --ip-address=192.168.1.200 --subnet=255.255.255.0 --gateway=192.168.1.2 --interface=eth0 --static=1 --hostname=zabbix --name-servers="192.168.1.2"`<br>
`cobbler system list`<br>
`cobbler sync`
#### 说明
--name  表示给客户端定义一个名字<br>
--mac 表示客户端的mac地址<br>
--profile 表示客户端使用哪个kickstart文件进行系统安装，ks文件后的.cfg必须省略（比如centos7.cfg必须写为--profile=centos7）
