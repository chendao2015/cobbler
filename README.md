# cobbler服务器端环境说明:
## 系统：CentOS6
## 本实验环境为vmware虚拟机
## 网卡设为nat模式

# cobbler install guide:
mkdir /usr/src/cobbler

git clone https://github.com/chendao2015/cobbler.git
cd cobbler
tar xf cobbler.tar.bz2 -C /usr/src/cobbler/
chmod +x cobbler.sh
./cobbler.sh

