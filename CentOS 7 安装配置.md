## CentOS 7 安装配置
### yum源
	https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
### 基本命令配置
1. \# yum install -y net-tools  ----网络工具，包含 ifconfig,netstat 
2. \# yum install -y vim   ----vi增强工具

### 网络配置
1. vim /etc/sysconfig/network-scripts/ifcfg-eth0 修改网卡配置文件（网卡名如果不一样，找到对应的文件就行
）

		TYPE="Ethernet"
		PROXY_METHOD="none"
		BROWSER_ONLY="no
		BOOTPROTO="dhcp"
		DEFROUTE="yes"
		IPV4_FAILURE_FATAL="no"
		IPV6INIT="yes"
		IPV6_AUTOCONF="yes"
		IPV6_DEFROUTE="yes"
		IPV6_FAILURE_FATAL="no"
		IPV6_ADDR_GEN_MODE="stable-privacy"
		NAME="eth0"
		UUID="c6ff9557-ad44-46be-924e-a0dc0dcfca04"
		DEVICE="eth0"
		ONBOOT="yes"
		

2. 主要修改的位置  
		
		BOOTPROTO="static"          默认的dhcp是由路由器分配，改成静态，由手工分配
		ONBOOT="yes"                系统启动时加载
		IPADDR=172.16.13.X          IP地址
		NETMASK=255.255.255.0       子网掩码
		GATEWAY=172.16.13.254       网关的IP地址
		DNS1=114.114.114.114        DNS的IP地址
		
3. \# service network restart  修改后，重启网络使用配置生效

### 防火墙设置

\# systemctl status firewalld.service ----查看firewalld服务的状态,active是启动状态，inactive是关闭状态

\# systemctl stop firewalld.service ----关闭此服务


\# systemctl list-unit-files |grep firewalld --查看firewalld是否开机自动启动
firewalld.service enabled ----为自动启动 

\# systemctl enable firewalld.service --类似以前的chkconfig xxx on，开启开机自动启动
\# systemctl disable firewalld.service --类似以前的chkconfig xxx off，关闭开机自动启动

\# systemctl list-unit-files |grep firewalld
\# firewalld.service disabled ----不自启动

查看已经开放的端口：

firewall-cmd --list-ports
开启端口

firewall-cmd --zone=public --add-port=80/tcp --permanent
命令含义：

–zone #作用域

–add-port=80/tcp #添加端口，格式为：端口/通讯协议

–permanent #永久生效，没有此参数重启后失效

取消开放的端口
firewall-cmd --remove-port=80/tcp --permanent

重启防火墙

firewall-cmd --reload #重启firewall
systemctl stop firewalld.service #停止firewall
systemctl disable firewalld.service #禁止firewall开机启动
firewall-cmd --state #查看默认防火墙状态（关闭后显示notrunning，开启后显示running）

### 关闭selinux 

\# sed -i 7s/enforcing/disabled/ /etc/selinux/config ----改完后，在后面重启系统生效

### 安装Oracle JDK
\# wget --header "Cookie: oraclelicense=accept-securebackup-cookie"  http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz
替换header 意为同意安装协议，可直接下载jdk文件

tar -zxvf jdk-8u181-linux-x64.tar.gz 得到 jdk1.8.0_181 目录
mv jdk1.8.0_181 /opt/java/
vim /etc/profile  在文件末尾追加
	
	export JAVA_HOME=/opt/java/jdk1.8.0_181 
	export CLASSPATH=$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
	export PATH=$PATH:$JAVA_HOME/bin
source /etc/profile

			

### MySql 8 安装配置
#### repo 模式
1. \# wget https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm 下载repo文件
2. \# rpm -Uvh mysql80-community-release-el7-1.noarch.rpm  安装repo源文件 
3. \# yum repolist all | grep mysql 查看安装情况 
4. \# vim /etc/my.cnf 查看MySQL配置文件
5. \# systemctl start mysqld.service 启动 
6. \# systemctl status mysqld.service  查看启动状态
7. \# grep 'temporary password' /var/log/mysqld.log 查看系统分配的root账号临时密码
8. \# mysql -uroot -p 输入密码 登录
9. msyql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';  修改root密码，密码格式有要求
10. 设置可远程访问

		mysql>use mysql
 		mysql>update user set host='%' where user='root' limit 1;
		mysql>flush privileges;   ---刷新权限



### 二进制包模式
1. 下载 https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.11-linux-glibc2.12-x86_64.tar.gz
2. tar -zxvf mysql-8.0.11-linux-glibc2.12-x86_64.tar.gz  解压缩
3. yum search libaio  查看是否已安装需要的依赖 如果没有安装，则安装
4. 设置用户有数据库初始化

		shell> groupadd mysql
		shell> useradd -r -g mysql
		shell> cd /opt
		shell> tar zxvf /path/to/mysql-VERSION-OS.tar.gz
		shell> ln -s full-path-to-mysql-VERSION-OS mysql
		shell> cd mysql
		shell> mkdir mysql-files
		shell> chown mysql:mysql mysql-files
		shell> chmod 750 mysql-files
		shell> bin/mysqld --initialize --user=mysql
		shell> bin/mysql_ssl_rsa_setup
5. vim /etc/my.cnf  设置配置文件 

		[mysqld]
		default_password_lifetime=0 #设置密码永不过期
		basedir=/opt/mysql
		datadir=/opt/mysql/data
		socket=/tmp/mysql.sock
		
		[mysqld_safe]
		log-error=/opt/mysql/log/mysql-err.log
		pid-file=/var/lib/mysql/mysql.pid
		log=/opt/mysql/log/mysql.log
		
		!includedir /etc/my.cnf.d
6. 启动数据库 

		shell> bin/mysqld_safe --user=mysql &
		
		shell> cp support-files/mysql.server /etc/init.d/mysql.server

### MongoDB  安装配置
1. \# wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.6.5.tgz  下载
2. \# tar -zxvf mongodb-linux-x86_64-rhel70-3.6.5.tgz -C /opt/mongodb  解压到指定位置
3. \# groupadd mongo
4. \# useradd -r -g mongo  添加用户和组
5. \# su mongo  切换用户
6. $ cd /opt/mongodb
7. $ mkdir data log
8. $ vim mongodb.conf 

		dbpath=/opt/mongodb/data
		logpath=/opt/mongodb/log/mongodb.log
		port=27017
		fork=true
		bind_ip=127.0.0.1,192.168.3.110   绑定内网IP即可，无需在外网访问
9. $ /opt/mongodb/bin/mongod -f /opt/mognodb/mongodb.conf   ---启动服务
10. 可以写一个启动脚本文件，配置到/etc/rc.local 下，来启用开机自启

### Redis 安装配置
1. \# wget http://download.redis.io/releases/redis-4.0.10.tar.gz 下载
2. \# tar -zxvf  redis-4.0.10.tar.gz  解压
3. \# yum -y install gcc gcc-c++  安装编译用到的依赖
4. \# cd redis-4.0.10
5. \# make   编译安装
6. \# 之后在src目录下会生成redis-server,redis-cli的可执行文件，根目录下会生成redis.conf文件
7. 可以写一个启动脚本文件，配置到/etc/rc.local 下，来启用开机自启

### Docker CE 安装配置
1. \# yum remove docker docker-common docker-selinux   删除旧版
2. \# yum install -y yum-utils device-mapper-persistent-data lvm2  安装需要的依赖包
3. \# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
3. \# yum install docker-ce
4. \# yum list docker-ce --showduplicates | sort -r  列出可选版本
5. \# system start docker  启动
6. \# yum remove docker-ce   卸载docker
7. \# rm -rf /var/lib/docker  卸载后需要手动删除所有图像，容器，卷
8. 修改容器时区 进入容器  执行 ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime


### RabbitMQ 安装配置

安装 erlang
安装 rabbitmq
配置文件  /etc/rabbitmq/rabbitmq.config

#### 用户管理
1. 添加用户  用户名，密码不用加引号

		#  rabbitmqctl add_user  username  password
2. 删除用户  系统不会警告 与用户相关的访问控制条目也会一并删除，所以需谨慎操作

		#  rabbitmqctl delete_user username
3. 查看用户

		# rabbitmqctl list_users

4. 修改用户密码  直接给新密码，不用旧密码

		# rabbitmqctl change_password username newpassword
		
#### 权限管理
1. 查看权限   -p后面接的是vhost的名字，带/字符，如 /toilet，如果不加-p 默认查看的是/这个默认vhost ， 也可以查看指定用户的权限  

		# rabbitmqctl list_permissions -p vhost
		# rabbitmqctl list_user_permissions username
		
2. 设置权限  指定用户在指定vhost上的权限，三个参数分别为 配置、写、读 权限 用正则表示，如果不授权则用 "" 空字符串表示

		# rabbitmqctl set_permissions -p vhost username ".*" ".*" ".*"
		
3. 删除权限   删除指定用户在指定vhost上的权限 
		
		# rabbitmqctl clear_permissions -p vhost username
		
#### 列出队列和消息数目
1. 列出指定vhost上的队列

		 rabbitmqctl list_queues -p /toilet
2. 列出指定vhost上的队列名，消息数量，消费者数量，占用内存

		#  rabbitmqctl list_queues -p /toilet name messages consumers memory

#### 列出交换机和绑定
1. 指定交换机
		
		# rabbitmqctl list_exchanges -p /toilet
		
2. 列出绑定信息

		# rabbitmqctl list_bindings -p /toilet

设置镜像集群策略
rabbitmqctl -n rabbit1 set_policy  ha-all "^" '{"ha-mode":"all"}'

vhost 相当于数据库，以/开头


### PostgreSQL 10 安装
1. 从官网安装 repo yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm
2. 安装服务端和客户端  yum install postgresql10 postgresql10-server
3. 切换到postgres用户  su postgres
4. 指定路径 初始化数据库 initdb -E UTF-8 --lc-collate=en_US.UTF-8 --lc-ctype=en_US.UTF-8
5. 启动数据库服务  pg_ctl -D /var/lib/pgsql/10/data -l /var/lib/pgsql/10/log start 或者 systemctl start postgresql10
6. 修改默认 postgres数据库用户的密码  postgres/postgres
		
		# su postgres
		$ psql
		\password  输入两次postgres的新密码
		
7. 创建用户
		
		create user toilet with password 'T0ilet@Zh0ngShengPG$?';  创建用户
		create database itoilet owner toilet;                      创建用户数据库
		grant all privileges on database itoilet to toilet;        授权
		
		在主机上创建同步账号
		create role pgrepuser replication login password 'pgreppass';  
		
8. psql -U dbuser -d mydb -h localhost -p 5432 登录数据库
9. systemctl status postgresql-10  查看状态