#### 安装常用工具

```
apt-get install net-tools vim -y
```

#### 配置静态IP

```
vi /etc/network/interfaces
# 添加如何内容
auto  enp3s0
iface enp3s0 inet static
address 192.168.1.111 
netmask 255.255.255.0
gateway  192.168.1.1

#编辑DNS
vi /etc/resolv.conf

nameserver = 114.114.114.114 //DNS1
nameserver = 8.8.8.8  //DNS2

#重启网卡
systemctl restart networking.service
```

#### 配置国内软件源

1、cp /etc/sources.list bak_sources.list
2、vi /etc/sources.list

deb http://mirrors.163.com/debian/ stretch main non-free contrib
deb http://mirrors.163.com/debian/ stretch-updates main non-free contrib
deb http://mirrors.163.com/debian/ stretch-backports main non-free contrib
deb-src http://mirrors.163.com/debian/ stretch main non-free contrib
deb-src http://mirrors.163.com/debian/ stretch-updates main non-free contrib
deb-src http://mirrors.163.com/debian/ stretch-backports main non-free contrib
deb http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib
deb-src http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib

三、更新系统

1、apt update
2、apt upgrade 

四、更改系统时区为中国，

dpkg-reconfigure tzdata

五、debian9安装docker-ce

1、卸载旧版

apt-get remove docker docker-engine docker.io

2、添加国内镜像

deb [arch=amd64] http://mirrors.ustc.edu.cn/docker-ce/linux/debian stretch stable

3、更新系统

apt-get update

apt-get install \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common
	 
4、安装docker
apt install docker-ce

5、启动及开机启动
systemctl start docker
systemctl enable docker

6、安装portainer

docker run -d -p 9000:9000 \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    --name prtainer-test \
    portainer/portaine

7、添加国内加速镜像
microsoft
dockerhub.azk8s.cn
	 
六、修改ssh默认端口
vi /etc/ssh/sshd_config

/etc/init.d/ssh restart