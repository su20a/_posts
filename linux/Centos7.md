---
title: Centos7常用命令
categories: 
- Linux
tags: 
- shell
---

## 前言

因为公司服务器都是centos7 服务器系统，所以这里对centos 7 的常规配置做一个简要的记录，方便后期维护。这里我用vmware 简单安装一个centos7 简单的演示。

## 基础知识

### 安装基础软件

```shell
# 使用ifconfig等命令
yum -y install net-tools

# 下载文件相关
yum -y install wget

# 测试网页交互
yum -y install curl

# 编辑配置文件
yum -y install vim

# ssh and sftp
yum -y install openssh-server

vim /etc/ssh/sshd_config # 配置sshd

service sshd start or systemctl start sshd  # 启动sshd服务

ps -e | grep sshd # 检查sshd服务是否启动

netstat -an | grep 22 # 检查22端口是否监听

systemctl enable sshd # 开启自启动sshd



```



### 配置镜像源

```shell

# 列出默认镜像源
[root@localhost ~]# ll /etc/yum.repos.d
total 32
-rw-r--r--. 1 root root 1664 Apr 29 00:35 CentOS-Base.repo
-rw-r--r--. 1 root root 1309 Apr 29 00:35 CentOS-CR.repo
-rw-r--r--. 1 root root  649 Apr 29 00:35 CentOS-Debuginfo.repo
-rw-r--r--. 1 root root  314 Apr 29 00:35 CentOS-fasttrack.repo
-rw-r--r--. 1 root root  630 Apr 29 00:35 CentOS-Media.repo
-rw-r--r--. 1 root root 1331 Apr 29 00:35 CentOS-Sources.repo
-rw-r--r--. 1 root root 4768 Apr 29 00:35 CentOS-Vault.repo

# 备份
[root@localhost yum.repos.d]#  mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup


# 下载 163 or aliyun yum 镜像源配置文件
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo 
or 
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

# yum makecache
yum makecache

# yum update
yum -y update
```



### 常用命令



#### 系统命令

```shell
# 查看系统内核
cat /proc/version or uname -a
 
# su
su - # 切换到root权限（与su有区别）

# shutdown
shutdown -h now	# 关机
shutdown -r now	# 重启

# top
top	# 罗列使用CPU资源最多的linux任务 （输入q退出）

# pstree
pstree	# 以树状图显示程序

# man
man ping	# 查看参考手册（例如ping 命令）

# cal
cal -3	# 显示前一个月，当前月以及下一个月的月历
cal 10 1988	# 显示指定月，年的月历

```



#### 磁盘管理

```shell

# df
df -h	# 显示磁盘的使用情况

# du
du -h file # 查看文件容量
du -h --max-depth=1 # 查看当前目录大小

# fdisk
fdisk -l # 显示所有分区信息

# mkfs
mkfs -t ext3 /dev/hdc6 # 对分区格式化系统

# fsck
fsck -C -f -t ext3 /dev/hdc6 # 强制检测/dev/hdc6分区

# mount
mount /dev/hdc6 /mnt/hdc6 # 将分区/dev/hdc6挂载到/mnt/hdc6目录
umount /dev/hdc6 # 卸载



```



#### 文件目录

```shell
# cd
cd /home	# 进入 /home 目录
cd ..		# 返回上一级目录
cd ../.. 	# 返回上两级目录
cd -		# 返回上次所在目录
cp file1 file2	# 将file1复制为file2
cp -a dir1 dir2	# 复制一个目录
cp -a /tmp/dir1 .	# 复制一个目录到当前工作目录（.代表当前目录）

# ls
ls		# 查看目录中的文件
ls -a	# 显示隐藏文件
ls -l	# 显示详细信息
ls -lrt	# 按时间显示文件（l表示详细列表，r表示反向排序，t表示按时间排序）

# pwd
pwd		# 显示工作路径

# mkdir
mkdir dir1	# 创建 dir1 目录
mkdir dir1 dir2	# 同时创建两个目录
mkdir -p /tmp/dir1/dir2	# 创建一个目录树
mv dir1 dir2	# 移动/重命名一个目录
rm -f file1	# 删除 ‘file1’
rm -rf dir1	# 删除 ‘dir1’ 目录及其子目录内容
```



#### 文本操作

```shell
# cat
cat file1	# 从第一个字节开始正向查看文件的内容

# tac
tac file1	# 从最后一行开始反向查看一个文件的内容

# head
head -2 file1	# 查看一个文件的前两行

# tail
tail -3 file1	# 查看一个文件的最后三行

# more
more file1	# 查看一个长文件的内容

```



#### 文本处理

```shell
# grep
grep str /tmp/test	# 在文件 /tmp/test 中查找 str
grep ^str /tmp/test	# 在文件 /tmp/test 中查找以 str 开始的行
grep [0-9] /tmp/test	# 查找 /tmp/test 文件中所有包含数字的行
grep str -r /tmp/*	# 在目录 /tmp 及其子目录中查找 str

# diff
diff file1 file2	# 找出两个文件的不同处

# sdiff
sdiff file1 file2	# 以对比的方式显示两个文件的不同
```



#### 文件查询

```shell

# find
find / -name file1	# 从 / 开始进入根文件系统查找文件和目录
find / -user user1	# 查找属于用户 user1 的文件和目录
find /home/user1 -name *.bin	# 在目录 / home/user1 中查找以 .bin 结尾的文件
find /usr/bin -type f -atime +100	# 查找在过去100天内未被使用过的执行文件
find /usr/bin -type f -mtime -10	# 查找在10天内被创建或者修改过的文件

find -name '*.[ch]' | xargs grep -E 'expr'	# 在当前目录及其子目录所有.c和.h文件中查找 expr
find -type f -print0 | xargs -r0 grep -F 'expr'	# 在当前目录及其子目录的常规文件中查找 expr
find -maxdepth 1 -type f | xargs grep -F 'expr'	# 在当前目录中查找 expr

# locate
locate *.ps	寻找以 .ps 结尾的文件，先运行 updatedb 命令
```



#### 文件权限

```shell

# chown
chown -R user1 /usr/meng # 将/usr/meng下的所有目录文件归属为user1

# chmod
chmod 777 -R dir/ # 修改dir目录下所有文件权限未777
chmod u+x,g+w f01　　# 为文件f01设置自己可以执行，组员可以写入的权限
chmod u=rwx,g=rw,o=r f01
chmod 764 f01
chmod a+x f01　　# 对文件f01的u,g,o都设置可执行属性
```





#### 压缩解压

```shell
# bzip2
bzip2 file1	# 压缩 file1
bunzip2 file1.bz2	# 解压 file1.bz2

# gzip
gzip file1	# 压缩 file1
gzip -9 file1	# 最大程度压缩 file1
gunzip file1.gz	# 解压 file1.gz

# tar
tar -cvf archive.tar file1	# 把file1打包成 archive.tar（-c: 建立压缩档案；-v: 显示所有过程；-f: 使用档案名字，是必须的，是最后一个参数）
tar -cvf archive.tar file1 dir1	# 把 file1，dir1 打包成 archive.tar
tar -tf archive.tar	# 显示一个包中的内容
tar -xvf archive.tar	# 释放一个包
tar -xvf archive.tar -C /tmp	# 把压缩包释放到 /tmp目录下
tar -xzf archive.tar.gz # 解压并释放
tar -xjf archive.tar.bz2 # 解压并释放

# zip
zip file1.zip file1	# 创建一个zip格式的压缩包
zip -r file1.zip file1 dir1	# 把文件和目录压缩成一个zip格式的压缩包
unzip file1.zip	# 解压一个zip格式的压缩包到当前目录
unzip test.zip -d /tmp/	# 解压一个zip格式的压缩包到 /tmp 目录
```



#### 软件安装

```shell
# rpm
rpm –i file.rpm	# 安装软件包
rpm –q	rpm # 查询软件包
rpm -e rpm # 移除软件包

# yum
yum -y install [package]	# 下载并安装一个rpm包
yum localinstall [package.rpm]	# 安装一个rpm包，使用你自己的软件仓库解决所有依赖关系
yum -y update	# 更新当前系统中安装的所有rpm包
yum update [package]	# 更新一个rpm包
yum remove [package]	# 删除一个rpm包
yum list	# 列出当前系统中安装的所有包
yum search [package]	# 在rpm仓库中搜寻软件包
yum clean [package]	# 清除缓存目录（/var/cache/yum）下的软件包
yum clean headers	# 删除所有头文件
yum clean all	# 删除所有缓存的包和头文件
```



#### 网络管理

```shell
# ifconfig
ifconfig eth0	# 显示一个以太网卡的配置
ifconfig eth0 192.168.1.1 netmask 255.255.255.0	#配置网卡的IP地址

# ifup
ifdown eth0	# 禁用 eth0 网络设备
ifup eth0	# 启用 eth0 网络设备

# iwconfig
iwconfig eth1	# 显示一个无线网卡的配置
iwlist scan		# 显示无线网络

# ip
ip addr show	# 显示网卡的IP地址

# traceroute 
traceroute # 路由追踪

# netstat
netstat -ap | grep ssh # 找出进程运行的端口

netstat -an | grep ':80' # 找出运行在指定端口的进程

netstat -i # 显示网络接口列表


# wget
wget downloadurl # 下载文件

# curl
curl www.baidu.com # 显示百度网页信息
```



#### 进程管理

```shell
# ps
ps -e | grep sshd # 检查sshd服务是否启动

# pidof
pidof nginx	# 查看nginx的进程号

# kill
kill -9 pid # 强制杀死进程

# pkill
pkill java # 杀死java进程
```



#### 系统服务

```shell


# 使某服务自动启动

chkconfig --level 3 httpd on

systemctl enable   httpd.service


# 使某服务不自动启动

chkconfig --level 3 httpd off

systemctl disable httpd.service


# 检查服务状态

service httpd status

systemctl status httpd.service （服务详细信息） systemctl is-active   httpd.service （仅显示是否   Active)

# 显示所有已启动的服务

chkconfig --list

systemctl list-units --type=service  

# 启动某服务

service httpd start

systemctl start httpd.service


# 停止某服务

service httpd stop

systemctl stop httpd.service


# 重启某服务

service httpd restart

systemctl restart httpd.service

# 防火墙
systemctl start firewalld

systemctl stop firewalld



```



