---
title: 把玩VPS
categories: 
- Tool
tags: 
- vps
- ssr
- lamp
---



#### 前言

VPS厂商很多，

如果使用**vultr**厂商注册新用户的话，请戳，[vultr推广连接](https://www.vultr.com/?ref=7567014)

如果使用阿里云的话，请戳， [阿里云大使](https://promotion.aliyun.com/ntms/yunparter/invite.html?userCode=um4bcafi)

以下是vultr的官方测速服务器，你可以进行下载测试，因为运营商或是位置的不同，不同位置速度都有差异，自行选择最适合自己的。

| Location 地理位置                           | Hostname 官方测试服务器ip | Download Test File 下载测试文件                              |
| ------------------------------------------- | ------------------------- | ------------------------------------------------------------ |
| (Asia)Tokyo, Japan[日本 东京]               | hnd-jp-ping.vultr.com     | [100Mb](http://hnd-jp-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://hnd-jp-ping.vultr.com/vultr.com.1000MB.bin) |
| Singapore[新加坡]                           | sgp-ping.vultr.com        | [100Mb](http://sgp-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://sgp-ping.vultr.com/vultr.com.1000MB.bin) |
| (AU) Sydney, Australia[悉尼]                | syd-au-ping.vultr.com     | [100Mb](http://syd-au-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://syd-au-ping.vultr.com/vultr.com.1000MB.bin) |
| (EU) Frankfurt, DE[德国 法兰克福]           | fra-de-ping.vultr.com     | [100Mb](http://fra-de-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://fra-de-ping.vultr.com/vultr.com.1000MB.bin) |
| (EU) Amsterdam, NL[荷兰 阿姆斯特丹]         | ams-nl-ping.vultr.com     | [100Mb](http://ams-nl-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://ams-nl-ping.vultr.com/vultr.com.1000MB.bin) |
| (EU) London, UK[英国 伦敦]                  | lon-gb-ping.vultr.com     | [100Mb](http://lon-gb-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://lon-gb-ping.vultr.com/vultr.com.1000MB.bin) |
| (EU) Paris, France[法国 巴黎]               | par-fr-ping.vultr.com     | [100Mb](http://par-fr-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://par-fr-ping.vultr.com/vultr.com.1000MB.bin) |
| Seattle, Washington[美东 华盛顿州 西雅图]   | wa-us-ping.vultr.com      | [100Mb](http://wa-us-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://wa-us-ping.vultr.com/vultr.com.1000MB.bin) |
| Silicon Valley, Ca[美西 加州 硅谷]          | sjo-ca-us-ping.vultr.com  | [100Mb](http://sjo-ca-us-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://sjo-ca-us-ping.vultr.com/vultr.com.1000MB.bin) |
| Los Angeles, Ca[美西 加州 洛杉矶**(推荐)**] | lax-ca-us-ping.vultr.com  | [100Mb](http://lax-ca-us-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://lax-ca-us-ping.vultr.com/vultr.com.1000MB.bin) |
| Chicago, Illinois[美东 芝加哥]              | il-us-ping.vultr.com      | [100Mb](http://il-us-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://il-us-ping.vultr.com/vultr.com.1000MB.bin) |
| Dallas, Texas[美中 德克萨斯州 达拉斯]       | tx-us-ping.vultr.com      | [100Mb](http://tx-us-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://tx-us-ping.vultr.com/vultr.com.1000MB.bin) |
| New York / New Jersey[美东 新泽西]          | nj-us-ping.vultr.com      | [100Mb](http://nj-us-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://nj-us-ping.vultr.com/vultr.com.1000MB.bin) |
| Atlanta, Georgiaa[美东 乔治亚州 亚特兰大]   | ga-us-ping.vultr.com      | [100Mb](http://ga-us-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://ga-us-ping.vultr.com/vultr.com.1000MB.bin) |
| Miami, Florida[美东 佛罗里达州 迈阿密]      | fl-us-ping.vultr.com      | [100Mb](http://fl-us-ping.vultr.com/vultr.com.100MB.bin) [1000Mb](http://fl-us-ping.vultr.com/vultr.com.1000MB.bin) |

个人选择的服务器系统是centos7，所以以下shell命令都是基于centos7。

#### 基本配置

创建一个用户进行操作，当然其实也没什么必要，因为现在基本vps都可以创建镜像快照可以进行恢复操作。所以下面还是都是使用root用户进行操作。

```shell
# 创建用户
useradd wjc
passwd wjc

# 授予sudo权限
chmod u+w /etc/sudoers
vi /etc/sudoers
wjc     ALL=(ALL)       ALL

# 添加ssh公钥到vps主机，以实现免密登录
ssh-copy-id user@vpsip
```



#### SSR

身为一名程序猿，经常需要用到谷歌搜索引擎，所以来一瓶酸酸乳是很有必要的，网上很多一键安装脚本，比如[秋水逸冰](https://shadowsocks.be/9.html) 或是通过[kcptun](https://github.com/xtaci/kcptun)

现在GFW升级，如果国内SSH端口22显示关闭，说明这个ip已经被封了，只能换一个IP地址了

[全国ping测速网页](https://tools.ipip.net/ping.php)

[国内端口查看](http://coolaf.com/tool/port)

[国外端口查看](https://www.yougetsignal.com/tools/open-ports/)

```shell
# 1.ssh 到vps服务器
ssh  -o StrictHostKeyChecking=no root@vpsip

# 2.测试服务器性能
wget -qO- git.io/superbench.sh | bash

# 3.一键安装ssr脚本
wget --no-check-certificate https://freed.ga/github/shadowsocksR.sh;bash shadowsocksR.sh

vi /etc/shadowsocks.json

/etc/init.d/shadowsocks start
/etc/init.d/shadowsocks stop
/etc/init.d/shadowsocks restart
/etc/init.d/shadowsocks status

# 或安装kcptun for ssr一键脚本
wget --no-check-certificate -O kcptun_for_ss_ssr.sh https://git.io/fN2EO
chmod 700 kcptun_for_ss_ssr.sh
./kcptun_for_ss_ssr.sh install

# 4.一键开启bbr
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh

sysctl net.ipv4.tcp_available_congestion_control
# 返回值一般为：
net.ipv4.tcp_available_congestion_control = bbr cubic reno
或者为：
net.ipv4.tcp_available_congestion_control = reno cubic bbr

# 或锐速
# 更换内核yum -y install wget screen   // For CentOS / Redhat
wget http://mirrors.linuxeye.com/lnmp-full.tar.gz   // Contains the source code
tar xzf lnmp-full.tar.gz
cd lnmp    // If you need to modify the directory (installation, data storage, Nginx logs), modify options.conf file
screen -S lnmp    // if network interruption, you can execute the command `screen -r lnmp` reconnect install window
./install.sh
wget-N --no-check-certificate https://freed.ga/kernel/ruisu.sh && bashruisu.sh
# 一键安装锐速脚本
wget -N --no-check-certificatehttps://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh &&bash serverspeeder.sh
# 备用脚本
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh&& bash serverspeeder-all.sh

# 如果出现重启出现文件系统变为 read-only file system，无法执行写入操作
mount -o remount rw /
```



####  LNMP

[Git仓库地址](https://github.com/oneinstack/lnmp)

xiangm我这里采用lnmp开源项目的一键安装脚本安装，我这里只需要 **mysql5.7**，**nginx**， **redis**，**php**等，因为下面有的开源项目是php语言开发的，你可以根据自己需要安装。

这里建议建一个镜像快照。

```shell
# For CentOS / Redhat
yum -y install wget screen

# Contains the source code
wget http://mirrors.linuxeye.com/lnmp-full.tar.gz
tar xzf lnmp-full.tar.gz

# If you need to modify the directory (installation, data storage, Nginx logs), modify options.conf file
cd lnmp

# If network interruption, you can execute the command `screen -r lnmp` reconnect install window
screen -S lnmp

# Begin Install
./install.sh

# Mysql 允许远程访问
mysql -uroot -p
use mysql;
grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option;
flush privileges; 

# 配置虚拟主机
cd lnmp
./vhost.sh
```



#### Gogs 私有Git

[**Gogs**](https://gogs.io/) 的目标是打造一个最简单、最快速和最轻松的方式搭建自助 Git 服务。使用 Go 语言开发使得 Gogs 能够通过独立的二进制分发，并且支持 Go 语言支持的 所有平台，包括 Linux、Mac OS X、Windows 以及 ARM 平台。妈妈再也不用担心github被墙了。

```shell
# 下载安装包
wget https://dl.gogs.io/0.11.86/gogs_0.11.86_linux_amd64.zip
unzip gogs_0.11.86_linux_amd64.zip

# 运行项目
cd gogs
./gogs web

```

浏览器输入地址进入web安装界面 http://vpsip:3000 ，ojbk了。

如果有域名的话，可以配置下nginx的反向代理。

#### Chevereto 图床

除了使用公共的图床，也可以使用 VPS 去搭建自己的个人图床。自建图床可以存储自己收藏的图片，也可以创建一些加密的相册。Chevereto 这款超高颜值的图床程序。它可以非常简便的上传图片（支持多图上传）并自动生成代码链接供其他程序引用，支持使用外部储存，开放用户注册上传等。

```shell
# 配置虚拟主机
Your domain:                  tc.yourdomain
Virtualhost conf:             /usr/local/nginx/conf/vhost/tc.yourdomain.conf
Directory of:                 /data/wwwroot/tc
Let's Encrypt SSL Certificate:/usr/local/nginx/conf/ssl/tc.yourdomain.crt
SSL Private Key:              /usr/local/nginx/conf/ssl/tc.yourdomain.key

# 安装Chevereto
cd /data/wwwroot/tc
git clone https://github.com/Chevereto/Chevereto-Free && mv Chevereto-Free/* ./ && rm -rf Chevereto-Free

# 给www用户授权
chown -R www:www /data/wwwroot/tc

# 配置nginx图床站点信息
cd /usr/local/nginx/conf/vhost
vim tc.yourdomain.conf
# 添加如下配置
location / {
  try_files $uri $uri/ /index.php?$query_string;
}

# 重启nginx
service nginx reload

# 登录mysql，创建数据库
create database chevereto

# 打开浏览器访问进行安装
tc.yourdomain

```

#### NextCloud 在线网盘

跟上述图床类似，简单搭建一个在线的网盘系统，方便我们管理或者分享文件。当然，你也可以使用七牛云存储，之前使用过感觉还不错，请戳 [七牛云推荐]链接(https://portal.qiniu.com/signup?code=3lktqd723yd76)

```shell
# 配置虚拟主机
Your domain:                  nextcloud.yourdomain
Virtualhost conf:             /usr/local/nginx/conf/vhost/nextcloud.yourdomain.conf
Directory of:                 /data/wwwroot/nextcloud
Let's Encrypt SSL Certificate:/usr/local/nginx/conf/ssl/disk.yourdomain.crt
SSL Private Key:              /usr/local/nginx/conf/ssl/nextcloud.yourdomain.key

# 安装nextcloud
cd /data/wwwroot/
wget https://download.nextcloud.com/server/releases/nextcloud-13.0.4.zip
unzip nextcloud-13.0.4.zip 

# 给www用户授权
chown -R www:www /data/wwwroot/nextcloud

# 配置nginx图床站点信息
cd /usr/local/nginx/conf/vhost
vim nextcloud.yourdomain.conf
# 添加如下配置
location / {
  try_files $uri $uri/ /index.php?$query_string;
}

# 重启nginx
service nginx reload

# 打开浏览器访问进行安装
nextcloud.yourdomain

```

